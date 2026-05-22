# AEO Skill Pack — Automation Builders run, 2026-05-19

All 7 AEO skills run against `automationbuilders.ai`. Outputs live in this folder.
Real artefact (deployable): `/llms.txt` at the repo root.

## What's in here

| # | File | Skill | Purpose |
|---|------|-------|---------|
| 1 | [01-visibility-audit.md](01-visibility-audit.md) | aeo-visibility-audit | 0–100 score per engine + top 10 cited / top 10 missing prompts + 3 fixes |
| 2 | [02-prompt-gaps.md](02-prompt-gaps.md) | prompt-gap-finder | 25 ranked buyer prompts to rank for + assets to ship for each |
| 3 | [03-aio-snippet.md](03-aio-snippet.md) | ai-overview-snippet-builder | Paste-ready AIO snippet for "cost to automate invoice reconciliation" |
| 4 | [04-llms.txt](04-llms.txt) | llms-txt-generator | The `/llms.txt` plus a roadmap of pages to add |
| 5 | [05-citation-rewrite.md](05-citation-rewrite.md) | citation-rewrite | Citable rewrite of the homepage (FAQ block + schema hints + llms.txt block) |
| 6 | [06-competitor-monitor.md](06-competitor-monitor.md) | competitor-citation-monitor | Share-of-voice vs Zapier / n8n / Mantel + 3 plays |
| 7 | [07-weekly-tracker.md](07-weekly-tracker.md) | weekly-aeo-tracker | Slack-pasteable Monday one-pager |

Also written outside this folder:
- `../llms.txt` — the deployable file. Drop it at `https://automationbuilders.ai/llms.txt`.

## TL;DR — the whole pack in 5 lines

1. Current AEO score is **5/100 weighted**. Zapier owns 72% of share-of-voice in the category.
2. The single biggest reason: **no `/llms.txt`, no schema, no comparison pages, no case studies**.
3. The new redesign already in the repo fixes the structural problem the moment it deploys — clean H1/H2 hierarchy, FAQ block, founder strip, trust block placeholders.
4. The three highest-leverage moves this week: **deploy `/llms.txt` + add JSON-LD schema; ship `/vs/zapier`; replace trust-block placeholders with real case studies.**
5. Re-run `weekly-aeo-tracker` next Monday for the first delta. After 4 weeks you'll see whether the moves moved the needle.

## Limitations to know about

- These are **predictive** scores from Claude's reasoning over each engine's known retrieval bias, not real-time crawls. To validate, run the 30 prompts manually against each engine and mark hits. Treat the scores as directionally right, not exact.
- Inferred competitors (Zapier / n8n / Mantel) are the closest *known* names. If your real lost deals go to specific Australian boutique agencies, swap them in and re-run.
- Citation effects from new pages take **2–6 weeks** to surface, especially in ChatGPT and Claude (training-data-style retrieval). Perplexity and AIO move faster (days, not weeks).
