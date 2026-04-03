# Executive Narrative: Analytics Team

**Student Name:** Boga Petruska\
**Date:** 2026-04-02\
**Case Context:** [x] Medium (MarketBridge)

---

## Context

MarketBridge processes 500,000 transactions per month across 15 metro areas and is approaching a profitability inflection point. The analytics team (me and three embedded analysts, with one Analytics Engineer hire in progress) is responsible for the metrics that inform every major decision: unit economics, market expansion go/no-go, and board reporting. Today, that responsibility is not being met. The board received conflicting transaction counts in the same meeting last quarter (487,000 from Finance, 523,000 from Product, a 7.4% gap), which stalled the Atlanta launch decision and weakened our fundraising narrative. The root cause is structural: there is no single source of truth. Three teams define the same metrics differently, dashboards are not trusted, and analysts spend roughly 80% of their time answering ad-hoc questions because stakeholders cannot self-serve. I joined four weeks ago as Head of Analytics after my predecessor left at eight months. The team is capable but skeptical of new leadership and operating without shared standards.

---

## What We Did

In the first 30 days, we focused on systemic fixes rather than quick wins. First, we established a monthly glossary governance process where Product, Finance, and Growth formally agree on metric definitions before they reach a dashboard or a board deck. The board number gap was a symptom; the root cause was that no such process existed. Second, we mapped all 14 stakeholders who depend on analytics and established a prioritized engagement cadence, replacing the previous model where stakeholders received analytics output only when they asked for it. We also drafted an AI usage policy to ensure we adopt AI coding assistants with a reviewed data processing agreement in place before anyone uses them with company data. Third, we completed a cost and capability audit of our data tooling and recommended converting the Mixpanel contract (our largest single tool cost at approximately $84,000 per year) to a month-to-month bridge at a reduced rate, tied to a deliverable-based sunset plan. This saves approximately $60,000 over the next 12 months while we build a trusted replacement on our existing warehouse.

---

## What We Learned

The metric definition problem is worse than it appeared from the outside. We initially assumed the board number gap was a data quality issue that could be fixed by cleaning a pipeline. In fact, it reflects a governance failure: Product, Finance, and Growth each independently defined "completed transaction" in ways that are internally consistent but mutually incompatible. No one was wrong; there was simply no process for agreeing. The fix is not primarily technical. We can build perfect data models, but until stakeholders agree on what each metric means, every dashboard will be challenged. The first glossary governance session confirmed this: it surfaced four additional metrics with conflicting definitions that had not yet reached the board but would have. Separately, we discovered that three pipeline breaks last quarter went undetected for days because Engineering made upstream schema changes without notifying us. Even with perfect definitions, our data will break silently without a formal change notification agreement.

---

## What's Next

Our top three priorities for the next quarter all connect to one goal: ensuring the board never sees conflicting numbers again.

First, hire an Analytics Engineer and complete the semantic layer for the top 15 board-facing metrics. One definition per metric, implemented once, with automated tests that catch discrepancies before they reach a dashboard. The role is already budgeted; we need a compensation adjustment to attract the right experience level (see What We Need). Without this hire, the analysts remain stuck spending 80% of their time on ad-hoc queries and the metric conflicts will recur.

Second, ship the first PM-facing dashboard built on trusted data, targeting five or more weekly active users within 90 days of the AE's start date. We are co-designing this with the product team rather than rushing it, because they have been burned by dashboards with numbers they could not reconcile. Shipping another one before definitions are agreed upon would deepen the credibility problem. Our North Star, self-serve adoption rate, is currently at zero, targeting 65-70% within 12 months.

Third, complete the data inventory and privacy audit required for the Q3 GDPR review and the Berlin and Amsterdam market launches. This is a hard deadline with regulatory consequences. Our partnership with Legal also surfaced EU requirements beyond GDPR (Digital Services Act transparency obligations, DAC7 provider income reporting) that we are designing for now to avoid expensive retrofitting later.

---

## What We Need

We need three things from leadership, each with a specific consequence if delayed.

The Analytics Engineer headcount is already approved and budgeted. We need approval this week on a $20-30,000 compensation increase above the budgeted level to attract candidates with production dbt experience, so we can begin sourcing before the Mixpanel renewal deadline forces a tooling decision without the AE in place. Without this, we either auto-renew Mixpanel at full cost ($84,000/year for a tool the team does not trust) or let it lapse and leave product managers with no analytics access for three to four months.

We need a written agreement with Engineering on schema change notifications: two sprints of advance notice before any change that affects our data pipelines. Last quarter, three pipeline breaks went undetected for days because no one told us the upstream schema had changed. Without this, we will continue discovering data quality problems from board members rather than from our monitoring.

We need Legal to prioritize the data processing agreement review for an AI coding assistant. The tool costs under $100/month for the full team and we estimate it will accelerate our infrastructure rebuild by 30-40%, particularly on repetitive work like data model documentation and test writing. The blocker is not cost, it is Legal's review of the vendor's data processing terms. Until that review is complete, we cannot authorize the tool for use with company data, and we want this resolved before the Q3 audit.

---

*AI assistance: I used Claude (Opus 4.6) as an iterative thinking partner to develop, pressure-test, and refine the ideas, structure, and language in this document. All analytical judgments, prioritization decisions, and strategic reasoning are my own.*
