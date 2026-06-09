# Automation Builders — Website Handoff

Everything an engineer needs to run, edit, deploy, and finish this site.
Last updated: 2026-06-09.

---

## 1. What this is

The marketing site for Automation Builders (automationbuilders.ai). It is a
**single static `index.html`** — vanilla HTML, CSS, and JS in one file. No build
step, no framework, no bundler. The only runtime dependency is Lenis (smooth
scroll), loaded from a CDN `<script>` tag.

- **Repo:** https://github.com/Automation-Builders/Website-update (branch `main`)
- **Host:** GitHub Pages, published by GitHub Actions (see §4).
- **Live:** https://automationbuilders.ai (custom domain, cut over 2026-06-09).
- **Pages URL:** https://automation-builders.github.io/Website-update/ now
  301-redirects to the custom domain.

### Repo layout
```
index.html                     ← the entire site (HTML + CSS + JS)
CNAME                          ← custom domain (automationbuilders.ai) for Pages
.nojekyll                      ← tells Pages to serve files as-is (no Jekyll)
.github/workflows/deploy.yml   ← GitHub Actions: publishes to Pages on push to main
llms.txt                       ← AI-search index, served at /llms.txt
privacy-policy.html
terms-of-service.html
square_logo.png, hyein.jpg, noah.jpg
n8n/                           ← lead-capture workflow + setup guide
  lead-capture-workflow.json   ← importable n8n starter
  README.md                    ← n8n build/setup steps + payload shape
aeo/                           ← AEO/SEO audit artefacts (reference, not shipped logic)
demo/                          ← invoice-automation demo assets (n8n flow + script)
CHANGES.md                     ← running changelog
index-v1-backup.html           ← original pre-redesign site (backup)
index-pre-feedback-backup.html ← backup before the v2.3 feedback pass
```

> Note: the whole repo root is published, so the backups and the `n8n/`, `aeo/`,
> `demo/` folders are reachable on the live domain (e.g. `/HANDOFF.md`). This
> matches the previous behaviour. If you want them off the public site, build a
> trimmed publish directory in the workflow instead of uploading `.`.

---

## 2. Run it locally

No install needed. From the repo root:

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Edit `index.html`, refresh. That's the whole loop.

> Note: the lead form POSTs directly to the n8n webhook (see §3/§5). From
> localhost that is a cross-origin call, so it only succeeds if the n8n workflow
> is active and its CORS allowed-origins include your local origin. Otherwise the
> POST fails gracefully and the UI shows the honest fallback.

---

## 3. Editable config (top of the `<script>` block in `index.html`)

| Constant | What it does |
|---|---|
| `CALENDLY_URL` | Booking link. Currently `calendly.com/noah-automationbuilders/30min`. |
| `LEAD_WEBHOOK` | The n8n **Production** webhook URL. The browser POSTs to it directly (no proxy, because Pages is static). To change the destination, edit this line. The n8n Webhook node must allow this origin via its "Allowed Origins (CORS)" option (see §5). Leave `''` to disable network calls. |
| `DEMO_VIDEO` | Set `.embedUrl` (Loom/Vimeo) or `.fileUrl` (mp4) to replace the animated demo with a real video. Both empty = animated demo (default). |
| `SCARCITY` | The "We onboard 2 clients/month, June is full…" line above the final CTA. Edit monthly. |
| `COUNTER_START_AUD` / `COUNTER_TICK_MS` | Hero live counter start value and tick speed. |

---

## 4. Deploy

**Automatic.** Every push to `main` triggers `.github/workflows/deploy.yml`, which
uploads the repo root as a Pages artifact and publishes it. No manual step.

- The Pages "build and deployment" source is set to **GitHub Actions** (not the
  legacy branch build).
- The workflow needs `pages: write` + `id-token: write` permissions (already set
  in the workflow file) and the repo's Pages feature enabled (it is).
- To deploy without a code change, re-run the workflow from the Actions tab
  (it also has a `workflow_dispatch` trigger).
- Check a deploy: GitHub → **Actions → Deploy to GitHub Pages**.

---

## 5. Lead capture — how it works

Two CTAs send leads: **"Email me this report"** and **"Book a call"**.

```
Browser  ──POST (cross-origin)──►  n8n webhook
```

- The site POSTs JSON straight to `LEAD_WEBHOOK`
  (`https://n8n.automationbuilders.ai/webhook/5e644b5e-d54e-4a7e-83ea-ea1666b199f6`).
- Because the page (automationbuilders.ai) and n8n (n8n.automationbuilders.ai)
  are **different origins**, the browser makes a CORS request. The n8n **Webhook
  node** must set **"Allowed Origins (CORS)"** to `https://automationbuilders.ai`
  (or `*`). Without it the browser blocks the call.
- The workflow must also be **Active** for the Production URL to respond.
- `postLead()` returns true only on a real 2xx, so the success toast is honest.
- Booking always proceeds to the Calendly iframe regardless of the webhook.

> History: the site used to be on Vercel, where `vercel.json` rewrote a
> same-origin `/api/lead` path to the n8n webhook (no CORS needed). On GitHub
> Pages there is no server-side proxy, so the call goes directly to n8n and CORS
> must be configured there. `vercel.json` has been removed.

### Payload the site sends
```json
{
  "kind": "email-report",          // or "booking"
  "ts": "2026-06-03T05:00:00.000Z",
  "name": "Sarah Chen",
  "email": "sarah@acme.com.au",
  "urgency": "ASAP",               // booking only
  "calculator": {
    "tasks": [{ "name": "...", "owner": "", "people": 2, "hrs": 6, "rate": 55 }],
    "assumptions": { "weeksPerYear": 48, "oncostMultiplier": 1.3, "annualGrowthPct": 10, "automatablePct": 80 },
    "results": { "threeYearValue": "A$123,456", "fteLine": "...", "hoursPerYear": "1,234",
                 "costPerYear": "A$41,184", "fiveYearCost": "A$205,000", "processCount": "1" }
  }
}
```
In n8n these are under `{{ $json.body.* }}`.

---

## 6. Finish the n8n workflow  ← MAIN OUTSTANDING TASK

Full steps + the importable workflow are in **`n8n/README.md`** and
**`n8n/lead-capture-workflow.json`**. Summary:

1. Import `n8n/lead-capture-workflow.json` (or build the 5 nodes by hand).
   Its webhook path matches the URL in `index.html`, so no URL change is needed.
2. On the **Webhook** node, set **"Allowed Origins (CORS)"** to
   `https://automationbuilders.ai` (required now that the call is cross-origin).
3. Add credentials to the nodes marked `REPLACE_ME`:
   - **Email report to prospect** (Gmail node) — only the **Credential** needs setting.
     Gmail OAuth2 needs a Google Cloud OAuth client (client ID + secret). In Google
     Cloud Console: enable Gmail API → OAuth consent screen (set **Internal** since
     support@ is on the Workspace) → create **OAuth client ID (Web application)** →
     add n8n's redirect URL
     `https://n8n.automationbuilders.ai/rest/oauth2-credential/callback` → paste
     client ID + secret into n8n → Sign in with Google.
     *(Or swap this node for the Microsoft Outlook node to send via M365.)*
   - **Notify team (report)** and **Notify team (booking)** (Slack nodes) — set the
     Slack credential and channel, or delete these two nodes if you don't want Slack.
4. **Activate** the workflow (toggle, top-right). Production URLs only run when active.
5. **Test:** on the live site, submit "Email me this report" → confirm an entry in
   n8n **Executions**, the email in the prospect's inbox, and the Slack ping.

The report email's HTML and the Slack text are built in the **"Build report"** Code
node — edit copy there.

---

## 7. Decisions already locked (don't re-open)

- **Calendly** = `noah-automationbuilders`.
- **Lead backend** = n8n, called directly from the browser (CORS on the n8n side).
- **Testimonials** parked until there are 3 real ones; trust currently carried by the
  founder cards + principles row + an *illustrative* (clearly labelled) case study.
- **Demo** = the animated HTML player; a real Loom can drop in via `DEMO_VIDEO`.
- **Voice/copy:** no em dashes anywhere in visible copy (use commas/colons). Founder
  bios are author-written — don't rewrite them.

---

## 8. Domain (done 2026-06-09)

`automationbuilders.ai` was moved off the old Figma Sites build and onto this site
on GitHub Pages. DNS is managed at **GoDaddy**. The records that point the site:

| Type | Name | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | automation-builders.github.io |

The custom domain is set in **Pages settings** and pinned by the `CNAME` file.

**Do not touch** the rest of the zone: the `n8n` A record (`34.151.128.121`), the
Google **MX** records (email), the **NS** and **SOA** records.

> HTTPS: done. GitHub issued a Let's Encrypt certificate for the apex + `www`
> and **Enforce HTTPS** is on. If you ever re-point DNS, the cert reprovisions;
> if it stalls, remove and re-add the custom domain in Pages settings to force a
> re-check. Editing GoDaddy DNS triggers an SMS identity check each time.

---

## 9. Gotchas worth knowing

- **HTTPS has a provisioning window.** Right after a DNS change, GitHub needs a
  while to issue the cert; until then HTTPS errors and some visitors may briefly
  see a cached old page. This is normal and clears on its own.
- **Closed modals must stay `visibility:hidden`.** A descendant with
  `pointer-events:auto` (e.g. the demo slide) can otherwise capture clicks/focus
  through a "closed" full-viewport overlay — this caused dead buttons + an
  un-typeable email field. Fixed in the `.modal-overlay` CSS; keep it.
- **Motion respects `prefers-reduced-motion`** (hero canvas, drift reveal, demo).
- **JSON-LD FAQ schema must match the visible FAQ text** — update both together or
  Google flags the mismatch.
- The repo's old `Noahautob/Website-update` URL **301-redirects** to the
  `Automation-Builders` org. Use the org URL going forward.

---

## 10. Quick status

| Area | State |
|---|---|
| Site build / design / copy | ✅ done, live |
| GitHub Actions → Pages deploy | ✅ auto-deploys on push to main |
| Custom domain cutover (DNS) | ✅ done 2026-06-09 |
| HTTPS (cert + Enforce HTTPS) | ✅ done 2026-06-09 (Let's Encrypt, enforced) |
| Lead form → n8n (CORS + activate) | ⏳ engineer (see §5/§6) |
