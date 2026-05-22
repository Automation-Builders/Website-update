# AEO edits — v2.1 (2026-05-19)

- Added full structured data (JSON-LD @graph) in `<head>`: `Organization`, `Person` (founder), `WebSite`, `FAQPage`. FAQPage answers match visible FAQ copy (Google flags mismatch). Single biggest AEO lift in the file — schema is the cheapest move to make engines confident about citing you.
- Added Open Graph + Twitter Card meta tags + canonical URL + `en_AU` locale.
- Tightened meta description with n8n + integrations keywords.
- Reframed trust block: removed the 3 client-logo placeholders, removed the placeholder testimonial blockquote, moved the founder strip up, added a 3-card "principles" row (Australian / your-IP / 12mo Care) as the trust signal until real testimonials land in Q3 2026.
- Reframed the mini case study from "Mini case study" to "Typical invoice reconciliation build (illustrative)" with the calculator math shown — citable, honest, no implied past client.
- Added anchor IDs to each FAQ `<details>` (`#faq-breakage`, `#faq-ip`, `#faq-data-security`, `#faq-exit`, `#faq-cost`) so engines can deep-link.
- Updated FAQ answer for "How much will it cost?" to include "A$10,000 minimum, 12 months Automation Care included" — the citable specifics engines lift.
- Deployable `/llms.txt` written to the Website repo root (separate from the AEO reports).

# Redesign changes — v2

- New Tesla-style hero: single H1 "Stop doing it by hand.", subhead with 20+ hrs/week claim, two CTAs (primary "See your savings" → calculator, secondary "Watch 60-sec demo"), live A$ counter (+A$1 every 8s, starts A$100k — editable via `COUNTER_START_AUD`).
- Calculator moved directly under hero. Per-row fields: process name, people involved, hours/week per person, avg hourly rate, owner (name + role). `% automatable` moved to global assumptions. Investment box removed (no more pricing in the result panel). Result headline: "A$X unlocked over 3 years" + FTE in muted text.
- Booking modal collapsed to name + email + urgency only. Calendly iframe embeds in-modal after submit (no redirect). Users who haven't touched the calculator first see a prompt nudging them through it before booking.
- Added "Email me this report" soft-conversion path. Captures name + email + full calculator state to `/api/lead` (POST) and console.logs (placeholder — wire up the endpoint).
- Six agent-type cards → three categories (Revenue / Operations / Back-office). Each has a "See in calculator →" button that pre-fills sample processes and scrolls to the calculator.
- Pricing tiers section removed entirely. Blueprint folded into the "What happens after you book" Day 2–5 step (Automation Assessment, fixed scope, fixed price).
- Added trust block: 3 client logo placeholders, testimonial placeholder, mini case study card (invoice reconciliation example — replaceable), founder strip.
- Added "What happens after you book" 3-step strip (Day 0 / Day 2–5 / Day 14–30).
- Added 5-question FAQ using `<details>` accordions: breakage, IP, data, exit, cost.
- Added editable scarcity line above final CTA — month + status configurable via the `SCARCITY` constant at the top of the `<script>` block.
- Whitespace ~2× larger across all sections. Inter loaded at weights 400 + 600 only (no 700s). Buttons standardised at 56px min-height. Sticky nav with primary CTA always visible top-right. Gradient text used in one place only (hero counter amount).
- Original `index.html` preserved at `index-v1-backup.html`.

## Placeholders that need real content
- `square_logo.png` is fine; **`founder.jpg`** referenced in the founder strip needs to be added (currently a dashed-border placeholder).
- **3× client logos** in the trust block — currently grey rectangles labelled "Client logo — replace".
- **Testimonial quote** — currently bracketed placeholder; pull from Gong or email and replace.
- **Mini case study** — invoice reconciliation numbers are illustrative; swap in a real before/after if you have one.
- **60-second demo video** — `#demoModal` has a placeholder; drop in the embed or `<video>` tag when ready.
- **`/api/lead` webhook** — both booking and email-report flows POST here. Wire up an endpoint (or replace with Slack webhook, n8n, Resend, etc.). Until then the data still appears in `console.log` for testing.
- **`SCARCITY` constant** in `<script>` — update monthly (e.g. `currentMonth: 'June', currentStatus: 'is full.'`).
