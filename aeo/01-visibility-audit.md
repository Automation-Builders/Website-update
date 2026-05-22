```
AEO VISIBILITY REPORT — automationbuilders.ai
Generated: 2026-05-19 | by the Psyke AEO Skill Pack (run manually by Claude)

INPUTS
- Domain: automationbuilders.ai
- Category: AI-enabled workflow automation studio (boutique agency)
- ICP: CEOs of Australian 20–500-person businesses with manual, repetitive operations
- Citation-share competitors (NOT sales competitors — see framing note below):
    1. zapier.com         — DIY tool buyers consider before hiring help
    2. mantelgroup.com.au — closest AU consulting competitor (AI/data arm: Eliiza)
    3. n8n.io             — open-source platform AB themselves deploy on

FRAMING NOTE (read this first)
Zapier and n8n are NOT sales competitors of Automation Builders — AB deploys on
both as part of every Build. They appear in this audit because they win the
*citation* share-of-voice on the prompts AB's buyers run ("how do I automate
X", "should I learn Zapier or hire help"). The AEO play is not to beat them
head-on; it's to be the answer the engines surface when the buyer concludes
"I shouldn't learn this myself." Every page suggestion in the reports below
should be read with that framing — AB wins by being recommended as the
implementer, not the replacement.

METHOD NOTE
Predictive scoring based on (a) the live site at automationbuilders.ai as of today,
(b) what's in Claude's training data through Jan 2026, and (c) each engine's documented
retrieval bias. This is a model-based estimate, not a real-time crawl of each answer
engine. To validate, run the 30 prompts manually against each engine and mark hits.

CITATION SCORE
- ChatGPT:        7/100
- Claude:         7/100
- Perplexity:     3/100
- Google AIO:     3/100
- WEIGHTED AVG:   5/100

The live site has near-zero presence. Tiny domain authority, no schema, no llms.txt,
no third-party citations, no comparison content, no case studies. Engines have
nothing to retrieve.

CITED ON (top 10 prompts where the brand IS likely cited — generous read)
1. "automationbuilders.ai pricing"                       — ChatGPT / Claude (brand-exact lookup → returns domain)
2. "is Automation Builders legit"                         — ChatGPT / Claude
3. "Automation Builders Calendly book"                    — Perplexity (URL match)
4. "support@automationbuilders.ai"                        — Claude (footer scrape)
5. "does Automation Builders work with Xero"              — ChatGPT (inferred from 500+ integrations claim)
6. None of the 24 generic prompts → competitor cited every time
7–10. (no further citations expected)

MISSING ON (top 10 high-intent prompts where a competitor appears, you don't)
1. "best AI automation agency for Australian SMBs"        — Mantel Group / large AU consultancies cited
2. "n8n vs Zapier for business automation"                — n8n.io / Zapier own this entirely
3. "how to automate invoice reconciliation for SMB"       — Zapier guides dominate
4. "should I hire an automation agency or use Zapier"     — Zapier comparison content owns this
5. "how to integrate HubSpot Xero Gmail Slack"            — Zapier integration pages cited
6. "top workflow automation companies in Australia 2026"  — Mantel Group / Datacom / Accenture cited
7. "how to automate ticket triage in Zendesk"             — Zapier + Zendesk docs cited
8. "AI automation for recruitment screening"              — Zapier + niche RPO platforms cited
9. "boutique AI automation agency Australia"              — small AU agencies with comparison pages cited
10. "how to give my team back 20 hours a week"            — productivity blogs / Zapier cited

TOP 3 FIXES (ranked by lift)

1. PUBLISH /llms.txt + ADD JSON-LD SCHEMA TO HOMEPAGE
   Expected lift: +12 pts on Google AIO, +8 pts on Claude, +4 pts on Perplexity.
   Why: AIO heavily weights Schema.org + canonical signals. Claude's bias toward
   documentation-shaped sources rewards a clear llms.txt. Cheapest win in the stack
   — content already exists in the new redesign; just needs to be indexed for engines.
   How: run the `llms-txt-generator` output already in /aeo/04-llms.txt.

2. SHIP THREE "HIRE VS DIY" GUIDES (NOT vs-pages against partners)
   Expected lift: +18 pts on ChatGPT, +10 pts on Perplexity over 60 days.
   Pages to ship:
   - /guides/should-i-learn-zapier-or-hire-help
   - /guides/n8n-yourself-vs-hire-an-n8n-consultancy
   - /guides/automate-in-house-vs-hire-agency
   Each page positions AB as the answer when "do it yourself" stops scaling — not
   as a competitor to Zapier or n8n (we deploy on both). This captures the same
   high-intent comparison prompts as /vs pages would, without the bad-faith
   framing of selling against the tooling we use. Comparison intent is the
   highest-converting AEO category and currently 0% owned.

3. PUBLISH 5 PROBLEM-LED CASE STUDIES WITH HARD NUMBERS + SCHEMA — POST-LAUNCH
   Expected lift: +9 pts across all engines over 90 days.
   The current site has zero social proof. Engines won't cite a brand they can't
   verify. Each case study = a `CaseStudy`/`Article` schema block + a hard number
   ("6 hrs → 4 min, A$58K/yr saved") + a named client. AB has two builds in
   delivery; testimonials and named case studies land in Q3 2026 after launch.
   Until then, the new redesign uses an honest "Typical build (illustrative)"
   card with the calculator math shown — which is still citable (the math is
   sourced and dated) without claiming a specific past client.

NEXT STEP
Run `prompt-gap-finder` on this domain to expand the missing-prompt list to 50.
(Already done — see /aeo/02-prompt-gaps.md.)
```
