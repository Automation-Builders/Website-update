# Automation Builders — Website Handoff

Everything an engineer needs to run, edit, deploy, and finish this site.
Last updated: 2026-06-03.

---

## 1. What this is

The marketing site for Automation Builders (automationbuilders.ai). It is a
**single static `index.html`** — vanilla HTML, CSS, and JS in one file. No build
step, no framework, no bundler. The only runtime dependency is Lenis (smooth
scroll), loaded from a CDN `<script>` tag.

- **Repo:** https://github.com/Automation-Builders/Website-update (branch `main`)
- **Host:** Vercel — project `automation-builders`
- **Live (current):** https://automation-builders.vercel.app
- **Custom domain:** `automationbuilders.ai` still points at the OLD site (Figma
  Sites). Not cut over yet — see §8.

### Repo layout
```
index.html                     ← the entire site (HTML + CSS + JS)
vercel.json                    ← proxies /api/lead → the n8n webhook
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

---

## 2. Run it locally

No install needed. From the repo root:

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Edit `index.html`, refresh. That's the whole loop.

> Note: `/api/lead` only works in production (Vercel proxies it). Locally the
> lead POST just fails gracefully and the UI shows the honest fallback.

---

## 3. Editable config (top of the `<script>` block in `index.html`)

| Constant | What it does |
|---|---|
| `CALENDLY_URL` | Booking link. Currently `calendly.com/noah-automationbuilders/30min`. |
| `LEAD_WEBHOOK` | `'/api/lead'` — **leave as-is.** It's same-origin and Vercel proxies it to n8n (see §5). To change the destination, edit `vercel.json`, NOT this line. |
| `DEMO_VIDEO` | Set `.embedUrl` (Loom/Vimeo) or `.fileUrl` (mp4) to replace the animated demo with a real video. Both empty = animated demo (default). |
| `SCARCITY` | The "We onboard 2 clients/month, June is full…" line above the final CTA. Edit monthly. |
| `COUNTER_START_AUD` / `COUNTER_TICK_MS` | Hero live counter start value and tick speed. |

---

## 4. Deploy

**Currently manual** (auto-deploy not yet wired — see below):

```bash
vercel --prod          # from the repo root, deploys to production
```

The Vercel project is already linked locally (`.vercel/` is gitignored). The CLI
user must have access to the `automation-builders` project.

### Wire up auto-deploy (recommended — one-time, dashboard only)
The repo was transferred to the **Automation-Builders** GitHub org, which is why
earlier CLI attempts failed. To finish:

1. Vercel → **automation-builders** project → **Settings → Git → Connect Git Repository**
2. Choose GitHub → **grant the Vercel GitHub App access to the `Automation-Builders` org**
   (an org owner may need to approve)
3. Select **`Automation-Builders/Website-update`**, set **Production Branch = `main`**

After that, every push to `main` auto-deploys; no more manual `vercel --prod`.

---

## 5. Lead capture — how it works

Two CTAs send leads: **"Email me this report"** and **"Book a call"**.

```
Browser  ──POST /api/lead──►  Vercel (vercel.json rewrite)  ──►  n8n webhook
```

- The site POSTs JSON to the **same-origin** path `/api/lead`.
- `vercel.json` rewrites that server-side to
  `https://n8n.automationbuilders.ai/webhook/5e644b5e-d54e-4a7e-83ea-ea1666b199f6`.
- Because it's same-origin from the browser's view, **there is no CORS** to configure.
- `postLead()` returns true only on a real 2xx, so the success toast is honest.
- Booking always proceeds to the Calendly iframe regardless of the webhook.

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
   Its webhook path matches the URL in `vercel.json`, so no URL change is needed.
2. Add credentials to the nodes marked `REPLACE_ME`:
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
3. **Activate** the workflow (toggle, top-right). Production URLs only run when active.
4. **Test:** on the live site, submit "Email me this report" → confirm an entry in
   n8n **Executions**, the email in the prospect's inbox, and the Slack ping.

The report email's HTML and the Slack text are built in the **"Build report"** Code
node — edit copy there.

---

## 7. Decisions already locked (don't re-open)

- **Calendly** = `noah-automationbuilders`.
- **Lead backend** = n8n via the Vercel proxy.
- **Testimonials** parked until there are 3 real ones; trust currently carried by the
  founder cards + principles row + an *illustrative* (clearly labelled) case study.
- **Demo** = the animated HTML player; a real Loom can drop in via `DEMO_VIDEO`.
- **Voice/copy:** no em dashes anywhere in visible copy (use commas/colons). Founder
  bios are author-written — don't rewrite them.

---

## 8. Domain cutover (do when ready — NOT yet)

`automationbuilders.ai` currently serves the old Figma Sites build.
To move it to this site:

1. Vercel → project → **Settings → Domains → Add** `automationbuilders.ai` (+ `www`).
2. Vercel shows the DNS records to set.
3. Update DNS at the registrar / Cloudflare, removing the Figma Sites records.
4. Nothing in the code changes — `/api/lead` is relative, so the proxy follows the domain.

---

## 9. Gotchas worth knowing

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
| Lead proxy (site → Vercel → n8n) | ✅ wired + confirmed routing |
| n8n workflow credentials + activate | ⏳ engineer (see §6) |
| Vercel auto-deploy | ⏳ engineer (see §4) |
| Custom domain cutover | ⏸ when ready (see §8) |
