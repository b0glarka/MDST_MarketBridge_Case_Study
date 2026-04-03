# 12-Month Analytics Roadmap with RICE Prioritization

| Field | Your Entry |
|---|---|
| **Student Name** | Boga Petruska |
| **Date** | 2026-03-16 |
| **Case Context** | Medium (Series B) -- MarketBridge |

---

## North Star Metric

**What is your North Star metric?**

| Element | Your Answer |
|---------|-------------|
| **Metric name** | Self-serve adoption rate |
| **Current baseline** | ~0%. PMs do not trust existing dashboards (Mixpanel numbers conflict with SQL). All recurring data requests go through analyst ad-hoc tickets. |
| **Target (end of 12 months)** | 65-70% of recurring data requests served via self-serve dashboards without analyst involvement. |
| **Why this metric?** | Two-sided multiplier for path to profitability. Side 1: PMs make faster product decisions (feature velocity, conversion improvements) when they can access trusted data without waiting days for an analyst. Side 2: Analysts shift from ticket-taking (~80% reactive today) to strategic work (churn modeling, attribution, supply-side analysis) that directly informs revenue and cost decisions. Diane (VP Product, strongest executive sponsor) is personally invested in this outcome because her PMs spend more time debating numbers than acting on them. |
| **How is it measured?** | Categorized intake system: tag each incoming data request as "self-serveable" (answer exists in a dashboard) or "novel" (requires analyst work). Self-serve adoption rate = 1 - (self-serveable requests reaching analysts / total self-serveable requests). Measured weekly via request intake log. Requires implementing a lightweight tagging process in Slack or Jira as a precondition. |

**Note on metric lifecycle:** This is a transformation metric, not an evergreen one. Once self-serve adoption stabilizes above 65-70% and infrastructure is mature, the North Star should graduate to a business-outcome metric such as retention lift in data-informed cohorts vs. control cohorts. Self-serve adoption is the leading indicator (are people using the data?). Retention lift is the lagging indicator (did the data change outcomes?). We steer by the leading indicator now because the bottleneck is real and immediate. As we approach the target, we will propose the next North Star in a future roadmap cycle.

---

## Guardrail Metrics

_Guardrails are metrics that are currently at an acceptable baseline and could degrade if we chase self-serve adoption too aggressively. These are "must not get worse" constraints, not things we are building from scratch._

| # | Guardrail Metric | Current Baseline | Threshold (Must Not Fall Below) | Why It Matters |
|---|-----------------|-----------------|-------------------------------|----------------|
| 1 | Ad-hoc response time | Slow but functional (~2-5 business days for standard requests) | Must not exceed current average during transition to self-serve | As we redirect analyst time toward infrastructure and dashboard building, stakeholders who haven't been migrated to self-serve yet could get worse service. The interim period is dangerous: if Marco can't get a number he needs because all analysts are building dashboards, we've traded one problem for another. |
| 2 | Data stack cost | $25K/month (all tooling: Segment, Mixpanel, Fivetran, BigQuery, etc.) | Must not increase without CTO-approved justification tied to a specific cost offset | Raj's top concern is cost rationalization (costs doubled YoY). Building self-serve dashboards could push costs up: new BI tool licensing, increased BigQuery compute from more dashboard queries, potentially maintaining Mixpanel during a transition period. Self-serve must be cost-neutral or cost-reducing, not additive. |
| 3 | Analyst retention | 3 analysts, all currently employed (morale declining, senior analyst hinting at leaving) | Zero attrition during the 12-month transformation period | Losing even one analyst drops the team from 3 to 2 (33% capacity loss) during the most demanding period. The senior analyst holds irreplaceable Salesforce knowledge. If the push to self-serve feels like "your job is being automated away" rather than "we're freeing you for better work," they leave. |

---

## RICE Scoring Table

**Scoring context:** Reach is based on the 14 stakeholders in the stakeholder map. For compliance initiatives, Reach reflects company-wide risk exposure (~150 employees) if the initiative fails. Impact is scored against the North Star (self-serve adoption rate) as primary, with annotations where the initiative serves a different purpose (compliance, stakeholder relationship, strategic positioning).

| # | Initiative | Reach (/qtr) | Impact | Confidence | Effort (PM) | RICE Score | Horizon |
|---|-----------|-------|--------|------------|--------|------------|---------|
| 4 | Audit-ready: complete PII flow inventory, Segment event audit, and GDPR prep delivered to Legal before Q3 | 150 (company-wide) | 2 | 80% | 2.5 | **96** | Now |
| 2 | Tooling decision: cost-justified Mixpanel recommendation to CTO with migration plan if applicable | 12 | 2 | 80% | 0.5 | **38.4** | Now |
| 7 | EU launch unblocked: data architecture supports EU-only storage/processing for Berlin and Amsterdam | 150 (company-wide) | 2 | 50% | 4 | **37.5** | Next |
| 6 | Hire Analytics Engineer: source, interview, and onboard at competitive comp. Budget note: the cost is not the full $130-160K salary (2 hires are already budgeted). The incremental ask is a $20-30K compensation delta above the originally budgeted level to attract mid-to-senior candidates with production dbt experience. This delta is recoverable: the AE directly enables $30-50K/yr in tooling savings (Segment volume reduction, potential Mixpanel sunset, BigQuery optimization). Net cost-neutral or cost-positive within 12 months. | 15 | 3 | 90% | 2 | **20.25** | Now |
| 3 | Zero undetected P0 failures: tiered alerting catches critical pipeline breakages within 4 hours | 15 | 1 | 100% | 1 | **15** | Now |
| 1 | Single source of truth: top 15 business metrics have one agreed definition, implemented as tested dbt models with schema YAML as living glossary. Governance: definitions proposed by analytics, reviewed in the monthly cross-functional metrics review (see charter cadences), and require sign-off from the relevant domain owner before implementation in dbt. | 15 | 3 | 80% | 3 | **12** | Now |
| 5 | First self-serve win: one PM dashboard in production on dbt models, 5+ PMs using weekly, 50% reduction in related ad-hoc requests. PM enablement (training, documentation, office hours) as sub-task. | 8 | 2 | 80% | 1.5 | **8.5** | Now |
| 8 | Launch-ready dashboards: baseline metrics and supply-demand tracking live for each new market before go-live (Atlanta Q2, Berlin/Amsterdam Q3-Q4) | 6 | 1 | 80% | 1.5 | **3.2** | Next |
| 9 | Supply-side visibility: provider health metrics available in BigQuery without single-person Salesforce dependency | 6 | 2 | 80% | 3 | **3.2** | Next |
| 13 | Analyst standardization: formalize documentation practices from Now initiatives into shared coding standards, peer review process, onboarding guide, and cross-training sessions | 4 | 1 | 80% | 1.5 | **2.1** | Later |
| 12 | Rigorous experiments: PMs can run properly controlled A/B tests without analyst involvement | 8 | 2 | 50% | 4 | **2.0** | Later |
| 10 | Channel ROI clarity: multi-touch attribution model replacing last-touch UTM, CAC/LTV by channel available to Growth | 4 | 2 | 50% | 3 | **1.3** | Later |
| 11 | Financial-product bridge: unit economics at market level by combining BigQuery product data with NetSuite financial data | 3 | 1 | 80% | 2 | **1.2** | Later |
| 14 | Regulatory and ESG readiness: ensure dbt models and pipeline designs can support DSA audit queries, DAC7 tax reporting, and algorithmic fairness analysis for EU markets. Not active development, but architectural awareness: design decisions made in Now and Next should not foreclose these capabilities. EU expansion is the forcing function. | 6 (Growth + Legal + EU launch teams) | 0.5 | 50% | 1 | **1.5** | Later |

**Where RICE and horizon placement diverge:**

- **Initiative #1 (dbt + glossary) scores 12 but is placed in Now.** RICE undervalues this because Reach is "only" 15 internal stakeholders and Effort is high (3 PM). But this is the foundational initiative. Initiatives #3 (monitoring), #5 (PM dashboard), and eventually #8, #9, #12 all depend on the dbt layer being trustworthy. Without #1, we are building dashboards on untrusted data. The dependency chain, not the RICE score, justifies the Now placement.

- **Initiative #7 (EU data residency) scores 37.5 but is placed in Next, not Now.** Despite a high score driven by company-wide risk, this initiative has a 50% Confidence because it depends entirely on Engineering delivering infrastructure changes. The analytics team cannot build this alone. Next is the right horizon because Berlin/Amsterdam launches are Q3-Q4 and the engineering dependency is the long pole. Starting discovery and requirements now, but committing to delivery next quarter.

- **Initiative #8 (market launch dashboards) scores 3.2 but Atlanta needs it in Q2.** The Atlanta launch is calendar-driven and falls at the boundary of Now/Next. Practically, Atlanta dashboards are a small sub-task (S-sized, ~2 weeks) that can be built once the first dbt models from initiative #1 are in place. Berlin/Amsterdam dashboards follow later when EU data residency (#7) is resolved.

---

## Roadmap Visualization

### Now (This Quarter - Committed)
_Actively staffed. Accountable for delivery. Team capacity: Head of Analytics + 3 embedded analysts + AE (joining month 2-3)._

| Initiative | Size (S/M/L/XL) | Key Dependency | Expected Outcome |
|-----------|-----------------|----------------|-----------------|
| #6 Hire Analytics Engineer | L | HR process, competitive comp approval from CTO | AE onboarded and productive by end of quarter. Every other Now initiative accelerates once AE arrives. |
| #1 Single source of truth (dbt + glossary) | XL | Cross-functional sign-off on metric definitions (Head of Analytics drives this); AE to implement models | Top 15 board-facing and operational metrics have one agreed definition implemented as tested dbt models. Metric debates replaced by glossary lookups. |
| #2 Tooling decision (Mixpanel) | S | AE technical audit (due by day 30); CTO budget approval | Decision made and communicated. If migrating, transition plan scoped with timeline. If renewing, negotiated at reduced rate with sunset conditions. |
| #4 Audit-ready (PII + Segment + GDPR) | L | Legal (Anya) co-ownership; Segment event inventory overlaps with dbt source audit | Complete PII flow inventory, consent record remediation plan, and Segment event audit delivered to Legal. Q3 audit preparation on track. |
| #3 Zero undetected P0 failures | M | AE (primary builder); Engineering cooperation for Fivetran alerting | Automated alerts for all P0 pipelines (Stripe, transactions, user identity). P1 alerting in place. Breakages caught within 4 hours, not days. |
| #5 First self-serve win (PM dashboard) | M | dbt models from #1 for underlying data; Diane driving PM adoption | One high-demand dashboard live on trusted dbt models. 5+ of 8 PMs using it weekly. 50% reduction in ad-hoc requests for covered metrics. PM enablement (documentation, walkthrough) delivered. |

### Next (Next Quarter - Planned)
_Scoped and ready to start. Move into Now when current quarter completes or dependencies resolve._

| Initiative | Size (S/M/L/XL) | Key Dependency | Expected Outcome |
|-----------|-----------------|----------------|-----------------|
| #7 EU launch unblocked (data residency) | XL | Engineering infrastructure for EU-only storage/processing; Legal guidance on residency requirements | Data architecture supports EU-only data flows for Berlin and Amsterdam. Analytics pipelines can operate on EU-resident data without touching US infrastructure. |
| #8 Launch-ready dashboards (market analytics) | M | dbt models from #1; market launch timelines from Marco; EU data residency (#7) for Berlin/Amsterdam | Baseline metrics and supply-demand tracking live for each new market before go-live. Atlanta first (may start late in Now quarter), then Berlin/Amsterdam. |
| #9 Supply-side visibility (Salesforce rebuild) | L | Senior analyst knowledge transfer (started in Now via #4 Segment audit documentation); Sales Ops cooperation on Salesforce schema | Provider health metrics (response rates, earnings, lead pipeline, supply-demand balance by metro/category) available in BigQuery via documented, maintainable dbt models. Single-person Salesforce dependency eliminated. |

### Later (6-12 Months - Exploratory)
_Directional. Details intentionally vague. Represent where the team is heading once Now and Next are delivered._

| Initiative | Size (S/M/L/XL) | Key Dependency | Expected Outcome |
|-----------|-----------------|----------------|-----------------|
| #10 Channel ROI clarity (attribution model) | L | Reliable event tracking (from #4 Segment cleanup); dbt models for user journeys (#1); Marco's patience | Multi-touch attribution model replacing last-touch UTM. CAC/LTV by channel available to Growth. Marco can make evidence-based acquisition spend decisions. |
| #12 Rigorous experiments (A/B platform) | XL | Stable dbt layer (#1); clean Segment events (#4); PM self-serve maturity (#5); statistical design expertise (hire #2 or existing analyst upskilling) | PMs can design and run properly controlled A/B tests with statistical rigor. Diane's second major ask, delivered after her first ask (self-serve) is stable. |
| #11 Financial-product bridge (NetSuite) | M | dbt layer (#1); CFO engagement (currently Keep Satisfied, may need to escalate); NetSuite data access | Unit economics at market level by combining BigQuery product data with NetSuite financial data. Christine's team stops maintaining parallel Excel models. |
| #13 Analyst standardization + cross-training | M | Documentation accumulated during Now initiatives; team trust established; AE as co-driver of standards | Shared coding standards, peer review process, onboarding guide for future hires, cross-training sessions. The documentation created as a byproduct of Now work gets formalized into institutional practices. |
| #14 Regulatory and ESG readiness | S | EU data residency (#7) in place; Legal (Anya) guidance on DSA/DAC7 requirements | dbt models and pipelines verified to support DSA audit queries, DAC7 tax reporting for EU providers, and algorithmic fairness analysis. Not a build, but a design audit: confirm that Now/Next architecture decisions did not foreclose these capabilities. EU expansion is the forcing function. |

---

## Dependencies and Sequencing

### Key Dependencies

| Initiative | Depends On | Type | Risk if Delayed |
|-----------|-----------|------|----------------|
| #1 Single source of truth (dbt) | #6 AE hire (AE is primary builder); cross-functional metric definition sign-off (Head of Analytics drives) | People + Stakeholder | If AE hire takes 3+ months, dbt work is limited to what Head of Analytics can do alone while managing everything else. If stakeholders can't agree on definitions, models get built on assumptions that get challenged later. |
| #5 First self-serve win (dashboard) | #1 dbt models (dashboard must be built on trusted data); Diane driving PM adoption | Technical + Stakeholder | If dbt models are delayed, dashboard is either delayed or built on untrusted data (which defeats the purpose). If Diane doesn't push PM adoption, dashboard gets built and ignored. |
| #7 EU data residency | Engineering infrastructure delivery; Legal (Anya) requirements clarity | Technical + Stakeholder | If Engineering is slow, Berlin/Amsterdam launches are delayed. This is outside analytics team control. Early discovery reduces surprise, but the dependency is real. |
| #4 Audit-ready (GDPR) | Legal (Anya) co-ownership; Segment event inventory (analytics team) | Data + Stakeholder | If PII inventory is incomplete by Q3, GDPR audit is at risk. This has regulatory consequences beyond the analytics team. Starting early is the primary mitigation. |
| #9 Supply-side visibility | Senior analyst cooperation on Salesforce knowledge transfer; Sales Ops schema stability | People + Data | If senior analyst leaves before knowledge is documented, supply-side data capability is lost. This is the highest single-person-dependency risk on the roadmap. |
| #2 Tooling decision (Mixpanel) | #6 AE hire (AE delivers technical audit); 6-week renewal deadline | People + Technical | If AE hasn't started by week 4, Head of Analytics must do the Mixpanel audit personally, compressing other work. If decision is deferred, Mixpanel auto-renews at current (potentially inflated) rate. |

### Sequencing Notes

**Critical path:** #6 (Hire AE) --> #1 (dbt + glossary) --> #5 (PM dashboard) --> self-serve adoption measurable

This is the backbone of the roadmap. Everything else either feeds into this path or runs in parallel.

**Parallel tracks during Now quarter:**

- **Track A (AE-led, starts month 2-3):** #1 dbt project, #2 Mixpanel audit, #3 pipeline monitoring. These are the AE's primary workstreams once onboarded.
- **Track B (Head of Analytics-led, starts month 1):** #6 hiring process, cross-functional definition sign-off meetings for #1, stakeholder management, #5 dashboard scoping (identifying which dashboard to build first based on PM input).
- **Track C (Analyst team + Legal, starts month 1):** #4 PII inventory and Segment event audit. Analysts document what they know about current data flows. Anya provides the compliance requirements checklist. This work starts immediately and doesn't depend on the AE.

**The first 6 weeks are the constraint.** The Mixpanel deadline (6 weeks) and the AE hiring timeline (8-12 weeks) overlap poorly. If the AE hasn't started by week 4, the Head of Analytics must do the Mixpanel technical audit personally. Plan for this contingency by starting Mixpanel discovery in week 1 (interview the PMs who use it, pull usage data, get pricing details from the vendor) so the formal audit is faster regardless of who does it.

**Infrastructure capacity and Charter Principle #2:** The charter sets a 30% floor for infrastructure and debt reduction work. During the Now quarter, infrastructure work exceeds this significantly (approximately 60-70% of capacity) by design, as the team is rebuilding the data foundation. As the team transitions to Next and Later initiatives, the 30% floor ensures infrastructure maintenance (pipeline monitoring, dbt model upkeep, Segment hygiene) doesn't get squeezed out by stakeholder-facing work. This is the mechanism that prevents the next Head of Analytics from inheriting the same abandoned infrastructure problem.

**Transition from Now to Next:** Initiatives #7, #8, #9 become active when:
- The AE is onboarded and productive (freeing Head of Analytics capacity)
- The dbt layer has enough models in production to support market-specific dashboards (#8)
- Engineering has begun EU infrastructure work (#7)
- Senior analyst Salesforce knowledge is documented (#9 precondition met via #4)

---

## Risk Register

| # | Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|---|
| 1 | AE hire takes longer than 6 weeks | Medium | High | Head of Analytics + Senior Analyst begin dbt audit in parallel. Mixpanel bridge extends (tied to deliverable, not date). Glossary governance continues with current team. | Head of Analytics |
| 2 | Stakeholders cannot agree on metric definitions | Medium | High | Monthly glossary governance meeting with escalation to CTO if consensus not reached. Start with the 5 board-facing metrics, not all 15 at once. | Head of Analytics |
| 3 | Engineering schema changes break pipelines without notification | High | Medium | Requesting written SLA: 2-sprint advance notice. Configuring existing Fivetran alerts + dbt tests as part of AE 90-day outcomes. | Head of Analytics + Engineering |
| 4 | Q3 GDPR audit finds gaps in PII inventory | Medium | High | Data inventory started in month 1 (not waiting for AE). Legal partnership active. DSA and DAC7 requirements surfaced proactively. | Head of Analytics + Legal (Anya) |
| 5 | Senior analyst leaves before Salesforce knowledge is documented | Low | High | Knowledge transfer structured into AE onboarding. Documentation of Salesforce joins is part of initiative #4 (audit-ready). Analyst retention is a guardrail metric. | Head of Analytics |
| 6 | Mixpanel bridge costs accumulate if AE delivery slips | Low | Medium | Bridge is at a reduced rate (~$4-5K/month vs. $7K). Sunset trigger is deliverable-based (5+ PM weekly users on replacement dashboard). Even extended bridge is cheaper than full renewal. | Head of Analytics |

---

## Metrics Tree

_The core argument: self-serve adoption is a two-sided multiplier that connects directly to the board's profitability mandate._

```
Business Outcome:     Path to Profitability (board mandate)
                                    |
                             Unit Economics
                       /                       \
               Revenue Growth             Cost Efficiency
                     |                          |
               Faster PM                  Analyst capacity
               decisions                  shifts to high-
               (self-serve)               impact work
                     |                          |
               Feature velocity,          Churn models,
               conversion                 attribution,
               improvements               supply-side analysis
                       \                      /
                         \                  /
                           NORTH STAR:
                           Self-serve adoption rate
                           (0% --> 65-70%)
```

**Input metrics (levers we pull to move the North Star):**
- Trusted dbt models in production (count)
- Glossary coverage (% of recurring questions with a defined metric behind them)
- Dashboard adoption (weekly active PM users)

**Guardrails (must not degrade while pursuing North Star):**
- G1: Ad-hoc response time (no worse than current ~2-5 days)
- G2: Data stack cost (no increase without CTO-approved offset)
- G3: Analyst retention (zero attrition during transformation)

---

## Evaluation Criteria

This artifact will be assessed as part of the Roadmap + Exec Narrative portfolio component (20% of course grade). For the Day 1 Checkpoint (10%, pass/fail), only completeness is assessed — all sections must have content.

**For the final portfolio submission, this roadmap will be evaluated on:**

| Criterion | Excellent | Good | Needs Work |
|-----------|-----------|------|------------|
| **North Star & Guardrails** | Clear metric with baseline and target; guardrails protect against obvious over-optimization risks | Metric identified but baseline or target is vague; guardrails present but not well-justified | Missing baseline/target; guardrails absent or unrelated to North Star |
| **RICE Scoring** | 8+ initiatives scored with plausible estimates; scoring drives meaningful prioritization discussion | 8 initiatives scored but estimates feel arbitrary; limited connection between scores and placement | Fewer than 8 initiatives or RICE applied mechanically without judgment |
| **Now/Next/Later Placement** | Placement is defensible; deviations from RICE ranking are explained; realistic given team size | Placement follows RICE scores but lacks nuance about dependencies or team capacity | Placement feels random or disconnected from scores |
| **Dependencies** | Critical path is clear; external dependencies identified; realistic about what blocks what | Some dependencies noted but not systematically mapped | Dependencies not addressed |
| **Business Alignment** | Every initiative connects clearly to business outcomes; a VP could read this and understand why | Most initiatives have business rationale; some feel like internal projects | Roadmap reads like a technical task list, not a business strategy |

---

*Day 1 draft. To be refined for final portfolio submission by March 30. See `assessment/grading-rubrics.md` for evaluation criteria.*

*AI assistance: I used Claude (Opus 4.6) as an iterative thinking partner to develop, pressure-test, and refine the ideas, structure, and language in this document. All analytical judgments, prioritization decisions, and strategic reasoning are my own.*
