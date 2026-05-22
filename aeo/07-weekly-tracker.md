```
WEEKLY AEO TRACKER — automationbuilders.ai
Week of 2026-05-19 | Powered by the Psyke AEO Skill Pack
Week 1 baseline — no prior data, so no deltas yet. Re-run next Monday for week 2.

SCOREBOARD
- ChatGPT      7/100      —  (baseline)
- Claude       7/100      —  (baseline)
- Perplexity   3/100      —  (baseline)
- Google AIO   3/100      —  (baseline)
- WEIGHTED     5/100      —  (baseline)

SHARE OF VOICE (you / comp1 / comp2 / comp3)
automationbuilders.ai: 5%  |  zapier.com: 72%  |  n8n.io: 28%  |  mantelgroup.com.au: 13%

WHAT MOVED (this week)
~ Week 1 baseline established. Nothing to diff against yet.
~ Major structural gap identified: no /llms.txt, no JSON-LD schema, no comparison
  pages, no case studies. The site is invisible to engines by design — every gap
  is a fixable one.
~ The new redesign sitting in the Website repo addresses 4 of the 5 highest-lift
  fixes the moment it ships (FAQ block, founder strip, clean H1/H2 hierarchy,
  trust block placeholder). Deploying it is itself the single biggest move.

THIS WEEK'S 3 PLAYS

1. SHIP /llms.txt + ADD ORGANIZATION + FAQPAGE SCHEMA
   Target: every engine, especially Google AIO.
   Deliverable: /llms.txt is already drafted at /Users/noahwebb/Projects/Website/llms.txt
   — deploy it to the live site root. Add the FAQPage and Organization schema
   blocks from /aeo/05-citation-rewrite.md to the new index.html <head>.
   Owner: Noah   |   Due: Wed 2026-05-21
   Expected lift by next Monday: +5 pts AIO, +3 pts Claude.

2. PUBLISH /guides/should-i-learn-zapier-or-hire-help
   Target prompt: "should I learn Zapier or hire someone to build it for me"
   Deliverable: the honest-tradeoffs guide outlined in /aeo/05-citation-rewrite.md
   (DIY-when / hire-help-when table + FAQPage schema). AB framed as Zapier's
   implementer, not its replacement — the engines reward partnership framing.
   Owner: Noah   |   Due: Fri 2026-05-23
   Expected lift by next Monday: +0 (citation re-index takes 2–4 weeks).
   Expected lift in 4 weeks: +8 pts ChatGPT, +4 pts AIO.

3. CASE STUDIES — DEFERRED TO Q3 2026
   AB has two builds in delivery; testimonials and named case studies land after
   launch. Until then, the trust block uses an honest "Typical build
   (illustrative)" card with calculator math shown — citable without claiming a
   specific past client. Diary this: as soon as the first client signs off on a
   public reference, add a CaseStudy schema block and a quote with their name +
   title + company. Expected lift when added: +6 pts across all engines on
   validation intent.

LAGGING INDICATOR TO WATCH
Citation-to-traffic ratio. Right now the site has near-zero citations AND near-zero
AI-referral traffic, so this metric is undefined. The first signal of progress is
NOT a citation — it's a single Perplexity or ChatGPT referral in Google Analytics 4
(filter on referrer contains "perplexity.ai" or "chatgpt.com"). Track this weekly.

ONE-LINE SUMMARY (Slack-pasteable)
AEO week 1 baseline: 5/100 weighted, dominated by Zapier (72%). 3 plays this week:
ship /llms.txt + schema, publish /vs/zapier, replace trust-block placeholders with
real case studies. Re-run next Monday to see deltas.

NEXT STEP
Set up `loop` to run this every Monday automatically:
  /loop 7d /weekly-aeo-tracker automationbuilders.ai vs zapier.com n8n.io mantelgroup.com.au
```
