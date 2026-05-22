# 30-Second Demo Script — Invoice Automation
For Noah to record on Loom / OBS / QuickTime when ready. Built to match the animated demo currently in `#demoModal` so the visual story stays consistent.

**Total runtime:** 30 seconds
**Voiceover wordcount target:** ~65 words (≈2.1 words/sec — calm, declarative pace)
**Tone:** Confident, plain-spoken Australian. No hype. No "imagine if…". Show, don't sell.
**Setup before recording:** screen at 1920×1080, Slack + Xero + n8n open in tabs, a dummy invoice PDF in your inbox ready to send.

---

## Shot list + voiceover

### 00:00 – 00:03 — The problem
**On screen:** Hard cut from black to a Xero "Bills to pay" view with ~14 unprocessed invoices listed. Hold for 2 seconds. Subtle red counter overlay top-right: `06:00:00` ticking up.
**VO:**
> *"Tuesday morning. Fourteen invoices. Six hours, gone."*

### 00:03 – 00:09 — Step 1: Inbox
**On screen:** Cut to n8n editor canvas, zoomed so all four nodes are visible. The Gmail-trigger node pulses green as a new email lands. Brief inset of the Gmail inbox with the PDF email arriving.
**VO:**
> *"An invoice arrives. n8n grabs the PDF inside sixty seconds."*

### 00:09 – 00:15 — Step 2: AI extract
**On screen:** Click into the AI Extract node. Right panel shows the JSON output filling in real time: `supplier_name`, `total_aud`, `gl_code`, `due_date`, `confidence: 0.96`. No need to read every field — let the viewer see structured data appearing.
**VO:**
> *"Claude reads it. Pulls supplier, amount, GL code, due date — and scores its own confidence."*

### 00:15 – 00:21 — Step 3: Xero
**On screen:** Cut to Xero "Bills to pay" — a new DRAFT bill appears at the top. Highlight the "Draft" status badge for a beat.
**VO:**
> *"A draft bill posts in Xero. Always draft — a human still approves."*

### 00:21 – 00:27 — Step 4: Slack
**On screen:** Cut to Slack #finance channel. A message appears: "📥 Acme Co. — A$1,247 — [Review in Xero →]". Cursor hovers the link.
**VO:**
> *"Slack pings finance with a one-click approve. No tab-hunting."*

### 00:27 – 00:30 — The payoff
**On screen:** Overlay text on a darkened screen: **"6 hrs → 4 mins. Every week."** Logo + "Built by Automation Builders" lower-right. Hold for 3 seconds.
**VO:**
> *"Six hours back, every week. Built by Automation Builders."*

---

## Safety callouts before you publish

- **Don't claim "100% automated"** in the voiceover — the flow still has a human approval step. Saying "supervised automation" or "human-in-the-loop" is accurate and avoids regulatory exposure (especially for AU accounting workflows).
- **Don't show a real client's invoice or supplier names** — use a dummy PDF you generate. "Acme Co." is a safe placeholder. Avoid implying a customer relationship you don't have.
- **Don't quote A$58K as a specific past client outcome** in the voiceover — the website uses it as an illustrative calculator number. The 30-second script intentionally leaves the dollar figure out so visitors are nudged to the calculator for their own number.
- **Don't show real credentials** in the n8n editor — the workflow JSON in this folder has `REPLACE_ME` placeholders. Make sure your screen-record doesn't reveal API keys, OAuth tokens, or webhook URLs.
- **Captions / accessibility** — burn captions into the video. More than half of B2B video is watched on mute.

---

## Recording checklist

- [ ] Loom Pro account so the video lives on a stable URL (free Loom URLs expire / get rate-limited)
- [ ] 1920×1080, 30fps minimum
- [ ] System audio off, only mic audio (no Slack notifications during recording)
- [ ] Dummy invoice PDF + dummy supplier name ready before you hit record
- [ ] Rehearse the voiceover twice — at 30s the cuts are unforgiving, every beat needs to land
- [ ] Trim to exactly 28–32 seconds in post (don't pad)
- [ ] Burn-in captions (Loom does this automatically, or use Descript)

## When the video is ready

Open `/Users/noahwebb/Projects/Website/index.html` and find the `DEMO_VIDEO` constant near the top of the `<script>` block. Set ONE of:

```js
const DEMO_VIDEO = {
  embedUrl: 'https://www.loom.com/embed/YOUR_LOOM_ID',
  fileUrl:  '',
  poster:   ''
};
```

That single edit replaces the animated demo with the real video. Nothing else to change.

## Reference assets in this folder

- `n8n-workflow-invoice-automation.json` — importable to your n8n. Build it once, demo it forever. Replace the `REPLACE_ME` credential IDs with your real Gmail/Xero/Slack accounts before running.
