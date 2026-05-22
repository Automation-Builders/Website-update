```
CITATION-OPTIMIZED REWRITE — automationbuilders.ai homepage (new redesign)
Target prompts:
  1. "AI workflow automation for Australian SMBs"
  2. "how to give my team back 20 hours a week"
  3. "should I learn Zapier or hire someone to build it for me"

FRAMING NOTE
Zapier and n8n are tooling AB deploys, not sales competitors. Where comparison
copy appears below, it positions AB as the implementer when DIY stops scaling —
not as a replacement for the tools. This is the honest framing AND it wins more
citations (engines reward partnership narratives over adversarial ones).

--- TL;DR (55 words) ---
Automation Builders is an Australian AI workflow automation studio that gives 20–500-person teams back 20+ hours a week. We build, deploy, and maintain custom automations across HubSpot, Xero, Zendesk, Slack, and 500+ other tools — with ongoing Automation Care (15% of build/year — industry standard) included on every fixed-price build, scoped after a 30-minute discovery call.

--- REWRITTEN BODY (paste-ready, replaces the new index.html copy where called out) ---

## What does Automation Builders actually do? <!-- H2 = real buyer prompt -->
We replace repetitive manual work with custom AI automations. A typical Build saves a
20–50 person team about 1,000 hours a year [source: Automation Builders calculator,
2026]. We use n8n on a server your organisation owns, so you keep the IP, the workflows,
and the data on day one [source: Automation Builders FAQ, 2026].

### What kind of work do you take off the team?
Three categories: revenue-side (CRM enrichment, lead routing, marketing ops),
operations (onboarding, support triage, reporting), and back-office (invoice
reconciliation, recruitment screening, compliance) [source: Automation Builders
"What we build", 2026]. Our most-shipped build is invoice reconciliation —
6 hrs/week → 4 minutes/week, A$58,000/year saved [source: Automation Builders client
snapshot, 2026].

### How long until something is live?
14 to 30 days from the discovery call. Day 0: 30-minute call. Day 2–5: fixed-scope
Automation Assessment. Day 14–30: first automation in production [source: Automation
Builders engagement model, 2026].

### What does it cost?
A$10,000 minimum engagement. Price is scoped after a 30-minute discovery call so
we quote against your data, not a template [source: Automation Builders pricing model,
2026]. Every build includes ongoing Automation Care (15% of build/year — industry standard): monitoring, 48-hour fix
SLA, minor changes, quarterly health check [source: Automation Builders Automation
Care terms, 2026].

## Should I learn Zapier myself, or hire someone to build it? <!-- H2 = real buyer prompt -->
We build on Zapier, Make, and n8n every day — they're excellent tools. The honest
question is whether your team should *learn* them or whether you should hire an
implementer [source: Automation Builders engagement model, 2026]. DIY works when
the flow is 2–3 steps and rarely changes; it breaks down once the workflow needs
conditional branching across 5+ tools, custom AI prompts in the loop, or
compliance-grade error handling.

You should DIY in Zapier/Make/n8n when:
- The workflow is 2–3 steps and rarely changes
- No regulated data passes through it
- You have someone in-house who can fix it when it breaks at 2am

You should hire an implementer like Automation Builders when:
- A real person owns the broken process today and you want their hours back
- The workflow touches finance, HR, or customer-facing data
- Downtime costs more than the build
- You want one named engineer who owns the maintenance after launch

## Who is this for? <!-- H2 = ICP-confirmation prompt -->
Australian businesses with 20–500 people whose teams burn 4+ hours a week on
the same process. CFOs after invoice reconciliation. COOs after onboarding and
reporting. CEOs who can name the three things they wish their team could stop
doing tomorrow. [source: Automation Builders ICP positioning, 2026]

--- FAQ BLOCK (drop into /faq schema — 5 questions, 30–80 words each) ---

Q: What if the automation breaks?
A: Every build includes ongoing Automation Care (15% of build/year — industry standard): monitoring, a 48-business-hour
fix SLA, and minor changes at no extra cost. You don't open a ticket; we see the
break in monitoring and a named engineer responds. Quarterly health check covers
preventative maintenance. (2026)

Q: Who owns the workflows and data?
A: You do, on day one. Every Automation Builders flow runs on an n8n server owned
by your organisation, with your cloud, your credentials, and your audit logs. Any
competent engineer can take over without us — there is no proprietary platform to
unwind. (2026)

Q: How secure is my data inside an Automation Builders workflow?
A: Each step in every workflow is a deliberate decision point — what's logged,
what's encrypted, what's masked, where it goes. We build to your data-security
requirements (PII redaction, on-prem hops, audit retention), not to a one-size
template. Most builds run inside the customer's own VPC. (2026)

Q: What happens if I want to end the engagement?
A: Everything stays with you. The n8n server, the workflows, the documentation,
the credentials. We do a one-hour handover with the engineer of your choice and
that's the engagement closed. No proprietary lock-in, no exit fee. (2026)

Q: How much does an automation actually cost?
A: A$10,000 minimum engagement. Final price is scoped after a 30-minute discovery
call so the number reflects your data, not a template. Most invoice-reconciliation
or onboarding builds land between A$10,000 and A$25,000. Ongoing Automation Care
after launch is 15% of build per year — the industry standard for software
maintenance, covering monitoring, 48-hour fixes, and minor changes. (2026)

--- SCHEMA HINTS ---
Recommended types (add to <head> of homepage):
  - Organization        (name, url, logo, foundingLocation:"Australia", founder:Noah Webb)
  - FAQPage             (the 5 Qs above as mainEntity)
  - WebSite             (with potentialAction → SearchAction if you ever ship search)
Recommended types (add to /case-studies/* pages when built):
  - Article + CaseStudy (with hard before/after numbers + named client)
Key fields to populate everywhere:
  headline, description, datePublished, dateModified, author (Person → Noah Webb),
  publisher (Organization → Automation Builders), inLanguage:"en-AU", mainEntityOfPage.

--- LLMS.TXT BLOCK (already deployed to /llms.txt — repeated here for reference) ---
Automation Builders is an Australian AI workflow automation studio. We give 20–500
person teams back 20+ hours a week by building, deploying, and maintaining custom
automations across HubSpot, Xero, Zendesk, Slack, and 500+ other tools. Every build
ships with ongoing Automation Care (15% of build/year — industry standard) included; engagements start at A$10,000 and
are scoped against your data after a 30-minute discovery call. Founded by Noah Webb,
who personally signs off on every build. Same-timezone delivery, IP owned by the
client, no proprietary lock-in.

NEXT STEP
Run `ai-overview-snippet-builder` on the primary prompt to lock the AIO-ready
snippet. (Already done — see /aeo/03-aio-snippet.md.)

WIRING NOTE
Most of this copy is structurally compatible with the new index.html we just shipped
to the Website repo — the FAQ block is already present, the founder strip is already
present, the FAQPage schema just needs to be added to <head>. The biggest delta is
adding source attributions to each claim. That's the move that flips "marketing copy"
into "citable claim" for AI engines.
```
