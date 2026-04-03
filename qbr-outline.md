# QBR Outline

**Student Name:** Boga Petruska\
**Date:** 2026-04-02\
**Case Context:** Medium (Series B) -- MarketBridge

---

## Executive Summary

**Status:** At Risk

**Headline:** Analytics has no single source of truth. Board-facing metrics conflict across tools by up to 7.4%, which last week prevented the board from determining whether unit economics are improving, stalling the Atlanta launch go/no-go and weakening our fundraising narrative.

**Top Risk:** Without a single source of truth, the board will see conflicting numbers again next quarter. That blocks capital allocation decisions (Atlanta launch, EU expansion), undermines the fundraising narrative, and erodes confidence in Finance, Product, and Analytics simultaneously. Every quarter we delay the fix, the credibility gap widens.

**Top Ask:** The two hires are already budgeted. I need sign-off on a $20-30K comp increase for the AE role to attract candidates with production dbt experience, and I need it this week so we can post and start sourcing before the Mixpanel renewal deadline forces a decision without the AE in place.

---

## Key Metrics and Progress

*Metrics are ordered as a causal chain: the problem, the fix, the outcome, the constraints.*

| Metric | Target | Actual | Trend | Commentary |
|---|---|---|---|---|
| Board metric conflicts (the problem) | Zero conflicts | 3 last quarter | Flat | Root causes identified: conflicting definitions across teams (governance) and silent pipeline failures including timezone mismatches and identity resolution errors (technical). Fixing both: glossary governance launched, AE hire will address pipeline reliability. |
| Glossary coverage (the fix) | Top 5 board-facing by Q2; all 15 by Q3 | ~15% (2 of ~15 defined) | Up | First two definitions approved in inaugural governance session. Current pace (~2/month) driven by cross-functional sign-off time, not analyst capacity. AE accelerates the implementation side. Q2 target achievable if we prioritize the 5 board-facing metrics first (on track) and extend to remaining 10 operational metrics through Q3. |
| Self-serve adoption (the outcome) | 65-70% by month 12 | ~0% | N/A (new metric) | Metric will not move until first dashboard ships (~90 days post-AE start). Glossary governance is underway and PMs are involved in co-designing the dashboard, which builds the trust foundation self-serve depends on. |
| Data stack cost (constraint) | $25K/month (no increase without CTO offset) | $25K/month | Flat | Mixpanel bridge decision (see Asks) reduces this by ~28% once sunset is complete. |
| Ad-hoc response time (guardrail) | < 2 business days | ~2-5 days | Flat | Must not worsen during infrastructure buildout. Analysts are at capacity. |
| Pipeline reliability (guardrail) | Zero undetected P0 breaks | 3 last quarter | Unmeasured (no monitoring exists) | AE will implement alerting as part of 90-day outcomes. Engineering SLA on schema changes requested (see Asks). |

---

## Wins and Impact

1. **Identified and decomposed the board number gap**
   - What we did: Traced the 487K vs. 523K transaction count discrepancy to three root causes: ~20K cancellations/refunds counted differently, ~9K timezone mismatch between systems, ~7K identity resolution double-counting.
   - Business impact: The board can now be given a corrected, reconciled number with an explanation. More importantly, we know the structural fix required (unified definitions, not just better queries).
   - Stakeholders affected: CFO (Christine), CTO (Raj), Board/Investors.

2. **Established glossary governance process**
   - What we did: Created a monthly cross-functional meeting where Product, Finance, and Growth formally agree on metric definitions before they reach dashboards or board decks.
   - Business impact: First session approved definitions for 2 board metrics and surfaced 4 additional metrics with conflicting definitions that had not yet reached the board. This is the structural fix for the metric chaos, not a one-time cleanup.
   - Stakeholders affected: VP Product (Diane), CFO (Christine), Head of Growth (Marco).

3. **Recommended Mixpanel contract restructuring**
   - What we did: Completed a cost and capability audit. Recommended converting from a full annual renewal (~$84K/year) to a month-to-month bridge at a reduced rate, tied to a deliverable-based sunset plan.
   - Business impact: Saves approximately $60K over 12 months. Demonstrates cost discipline: no tool renewal without a sunset plan for the replacement. Bridge rate is contingent on AE hire (see Asks).
   - Stakeholders affected: CTO (Raj), VP Product (Diane, whose PMs use Mixpanel daily).

---

## Risks and Blockers

| # | Risk / Blocker | Status | Impact if Unresolved | Mitigation Plan | Owner |
|---|---|---|---|---|---|
| 1 | AE hire delayed beyond 6 weeks | Active | Mixpanel renewal defaults to full annual cost ($84K). dbt rebuild delayed by months. Board metric conflicts persist into next quarter. | Comp increase approval this week to begin sourcing. Parallel: Head of Analytics + Senior Analyst begin dbt audit to reduce AE ramp time. | Head of Analytics |
| 2 | Engineering schema changes breaking pipelines without notification | Active | Undetected data quality issues surface in board decks or PM dashboards, repeating the credibility crisis. 3 incidents last quarter. | Requesting a written SLA: 2-sprint advance notice on schema changes. Adding to bi-weekly Engineering sync agenda. | Head of Analytics + Engineering |
| 3 | Q3 GDPR audit readiness | Active | Regulatory finding if PII flow inventory is incomplete. Could delay Berlin/Amsterdam launches. | Data inventory underway as part of AE 90-day outcomes. Partnership with Legal surfaced additional EU requirements (DSA, DAC7) being designed for now. | Head of Analytics + Legal (Anya) |

---

## Roadmap Update

### Now (This Quarter)

| Initiative | Status | Notes |
|---|---|---|
| Hire Analytics Engineer | In progress | JD, rubric, work sample, interview loop complete. Blocked on comp increase approval. |
| Mixpanel tooling decision | In progress | Decision memo complete. Recommending month-to-month bridge. Awaiting CTO approval. |
| Single source of truth (dbt + glossary) | Early stage | Glossary governance launched. dbt rebuild awaits AE hire. |
| Audit-ready (PII + Segment + GDPR) | In progress | Data inventory underway. Legal partnership active. |
| Zero undetected P0 failures | Not started | Depends on AE hire + Engineering SLA. |
| First PM dashboard (self-serve) | Not started | Depends on dbt models. Targeting 90 days post-AE start. Co-designing with PMs. |

### Next (Next Quarter)

| Initiative | Dependency | Notes |
|---|---|---|
| EU data residency (Berlin/Amsterdam launch) | Engineering infrastructure + Legal guidance | Architecture decisions being made now to avoid retrofitting. |
| Launch-ready dashboards (market analytics) | dbt models + PM dashboard pattern established | Atlanta first, then Berlin/Amsterdam. |
| Supply-side visibility (Salesforce rebuild) | AE in seat + Senior Analyst knowledge transfer | Eliminates single-person dependency on Salesforce joins. |

### Later (6+ Months)

| Initiative | Why Later | Notes |
|---|---|---|
| A/B experimentation platform | Requires trusted data foundation first | Revisit once self-serve adoption reaches 30%+. |
| Channel ROI clarity (attribution) | Needs clean data + experiment capability | Marco's priority, sequenced after infrastructure. |
| Financial-product data bridge (NetSuite) | Requires Christine's engagement + dedicated capacity | Important for unit economics but not urgent this quarter. |

**Changes from Original Roadmap:** None. Priorities remain as planned. The main risk is timeline compression if the AE hire is delayed.

---

## Asks and Decisions Needed

| # | Ask / Decision | Context | Urgency | Recommended Action |
|---|---|---|---|---|
| 1 | Approve $20-30K comp increase for AE role | Role is budgeted. Increase needed to attract candidates with production dbt experience. Without it, we source from a weaker pool and the dbt rebuild takes longer. | High (this week) | Approve increase. Post role immediately. |
| 2 | Written SLA with Engineering on schema change notifications | 3 pipeline breaks went undetected last quarter. We need 2-sprint advance notice before upstream changes. | High (this month) | CTO directs Engineering to formalize notification process. Add to bi-weekly sync. |
| 3 | Legal prioritizes DPA review for AI coding assistant | Tool costs under $100/month for the team. Accelerates dbt rebuild by 30-40%. Blocker is Legal's review of vendor terms, not cost. | Medium (before Q3 audit) | Anya schedules review within 2 weeks. |

---

## Anticipated Pushback

**The hardest question:** "You're asking for a comp increase to hire one person, and your entire plan depends on them. What happens if the hire doesn't work out, or takes 3 months instead of 6 weeks?"

**My answer:** The plan is sequenced to manage this risk, not eliminate it. If the hire takes longer than expected, we extend the Mixpanel bridge (the sunset trigger is tied to a deliverable, not a date, so we do not lose PM access). In parallel, the Senior Analyst and I begin the dbt audit ourselves, so the AE ramps faster once in seat. If the hire does not work out within the 90-day evaluation period, the loss is the comp delta ($20-30K), not the full investment, and we re-source immediately. The alternative to this plan is not "save the $20-30K." The alternative is that analysts continue spending 80% of their time on ad-hoc queries, the board sees conflicting numbers again next quarter, and we auto-renew Mixpanel at $84K/year for a tool nobody trusts. The comp increase is the cheapest lever we have for the highest-impact problem we face.

---

## Appendix: Supporting Data

- **Board number gap decomposition:** 487K (NetSuite/Finance) vs. 523K (Mixpanel/Product). Gap of ~36K transactions (7.4%) decomposed as: ~20K cancellations/refunds (definitional), ~9K timezone mismatch (technical), ~7K identity resolution double-counting (technical).
- **Mixpanel cost analysis:** Current annual cost ~$84K ($7K/month, 28% of data stack budget). Recommended bridge: $4-5K/month for 3-4 months ($15-21K total). Net first-year savings after bridge: ~$60K.
- **AE comp justification:** Budgeted role at mid-level comp. Market rate for candidates with production dbt + BigQuery experience requires 60th-75th percentile targeting, which is $20-30K above the budgeted level. Incremental cost is the delta, not the full salary.
- **Glossary governance tracker:** 2 of ~15 board-facing metrics defined and approved. 4 additional conflicts identified. Current pace: ~2 definitions per month. Accelerates to ~4-5/month with AE support.
- **Pipeline incident log:** 3 undetected breaks in Q4, all caused by upstream schema changes without notification. Average detection time: 3-5 days (discovered by stakeholders, not monitoring).

---

*AI assistance: I used Claude (Opus 4.6) as an iterative thinking partner to develop, pressure-test, and refine the ideas, structure, and language in this document. All analytical judgments, prioritization decisions, and strategic reasoning are my own.*
