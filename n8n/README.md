# Website lead-capture automation (n8n)

The site sends every lead to `/api/lead`, which `vercel.json` proxies to your n8n
webhook: `https://n8n.automationbuilders.ai/webhook/5e644b5e-d54e-4a7e-83ea-ea1666b199f6`

`lead-capture-workflow.json` in this folder is an importable starter. Import it,
swap the credential placeholders, activate it. Or build it by hand with the steps below.

## What the site POSTs

```json
{
  "kind": "email-report",          // or "booking"
  "ts": "2026-06-02T05:00:00.000Z",
  "name": "Sarah Chen",
  "email": "sarah@acme.com.au",
  "urgency": "ASAP",               // booking only
  "calculator": {
    "tasks": [{ "name": "Invoice reconciliation", "owner": "", "people": 2, "hrs": 6, "rate": 55 }],
    "assumptions": { "weeksPerYear": 48, "oncostMultiplier": 1.3, "annualGrowthPct": 10, "automatablePct": 80 },
    "results": {
      "threeYearValue": "A$123,456", "fteLine": "Equivalent to 1.2 FTE back to your team.",
      "hoursPerYear": "1,234", "costPerYear": "A$41,184", "fiveYearCost": "A$205,000", "processCount": "1"
    }
  }
}
```

In n8n these fields live under `{{ $json.body.* }}` — e.g. `{{ $json.body.email }}`,
`{{ $json.body.calculator.results.threeYearValue }}`.

## Build it by hand (5 nodes)

1. **Webhook** (you already made this). Method `POST`, the path above.
   - Set **Respond** = *Immediately* (response code 200). This makes the site show
     "Report on its way ✓" the instant n8n receives it; the email send runs after.
   - Activate the workflow (toggle, top-right) so the **Production** URL is live.

2. **Switch** on `{{ $json.body.kind }}` → two outputs: `email-report` and `booking`.

3. **Code** node (email-report branch) — builds the report HTML + a Slack summary
   from the calculator data. Copy the `jsCode` from `lead-capture-workflow.json`.

4. **Gmail** (or **Microsoft Outlook**) node — send to `{{ $json.to }}`, from
   `support@automationbuilders.ai`, subject `{{ $json.subject }}`, HTML body `{{ $json.html }}`.

5. **Slack** node(s) — post `{{ $json.slackText }}` to `#leads` for reports, and a
   booking alert on the booking branch.

## Test it

- Activate the workflow.
- On the live site → "Email me this report" → submit. You should see the execution
  in n8n's **Executions** list, an email in the prospect's inbox, and a Slack ping.
- If the email doesn't arrive: check the Gmail/Outlook credential and that the
  workflow is **Active** (production URL only runs when active).

## Notes

- CORS is handled by the Vercel proxy — n8n doesn't need any CORS config.
- To change the destination later, edit `vercel.json` (not the site JS).
- Booking still goes through Calendly regardless; this flow just captures the prep data.
