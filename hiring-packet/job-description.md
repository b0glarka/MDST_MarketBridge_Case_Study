# Job Description

**Student Name:** Boga Petruska\
**Date:** 2026-03-16\
**Case Context:** Medium (Series B) -- MarketBridge\
**Role Title:** Analytics Engineer\
**Level:** Mid

---

## Role Summary

> MarketBridge is hiring an Analytics Engineer to turn a partially built data foundation into the trusted infrastructure that powers every metric, dashboard, and experiment at the company. You will complete and extend our dbt project, reconcile conflicting metric definitions across Product, Growth, and Finance, and build the modeling layer that lets a team of three analysts stop firefighting and start doing high-impact work. This is a high-ownership role where your models become the single source of truth for a company processing 500,000 transactions per month across 15 metro areas.

---

## 90-Day Outcomes

1. **Trusted dbt semantic layer for top 10-15 business metrics.** The most contested metrics (active user, completed transaction, CAC, LTV, churn) have cross-functionally agreed definitions implemented as documented, tested dbt models with schema YAML. These models serve as the company's living business glossary. You will partner with the Head of Analytics to drive definition sign-off; your job is to translate agreed definitions into model logic and push back when definitions are ambiguous or contradictory.

2. **Documented inventory of all data sources, event tracking, and critical pipeline logic.** Complete audit of all 340 Segment events (identifying redundant, broken, and missing tracking), all Fivetran connectors, and all critical data pipeline knowledge, including the Salesforce-to-BigQuery joins that currently depend on a single analyst. Deliverable: a written inventory that eliminates single-person knowledge dependencies on any critical data flow. This inventory also serves as the starting point for the PII flow map required for the Q3 GDPR audit.

3. **One PM-facing dashboard in production, built on dbt models, with measurable adoption.** Identify the highest-demand PM dashboard (likely weekly product KPIs or funnel conversion), rebuild it on the new dbt models so the numbers are definitionally correct and match across tools, and ship it. Success metric: 5+ of 8 PMs using the dashboard at least once per week by day 90, with a 50%+ reduction in ad-hoc analyst requests for the metrics that dashboard covers.

4. **Technical capabilities audit of Mixpanel vs. warehouse-native alternatives.** Deliver a structured comparison documenting what Mixpanel currently does for the product team, which capabilities can be replicated via BigQuery + dbt + a BI tool, what would be lost in a migration, and estimated cost impact. This audit informs the Head of Analytics' renewal recommendation to the CTO. Due by day 30 (before the 6-week renewal deadline).

5. **Pipeline monitoring and alerting operational, tiered by business criticality.** Not all pipelines are equally important. By day 90, monitoring and alerting should be in place with response targets matched to impact:

   | Tier | Pipelines | Why Critical | Detection Target | Examples |
   |---|---|---|---|---|
   | **P0: Board/revenue** | Fivetran connectors feeding transaction, payment, and user tables in BigQuery; dbt models behind board-facing metrics | A breakage here means board numbers are wrong or revenue reporting is stale. Christine and Raj see these. | 100% caught within 4 hours (business hours) | Stripe-to-BigQuery sync, `fct_transactions`, `fct_bookings`, core user identity models |
   | **P1: PM-facing / operational** | dbt models powering the PM dashboard (outcome #3); Segment event flow for product analytics; supply-demand metrics | A breakage here means PMs lose trust in the dashboard you just shipped, undoing outcome #3. | 95% caught within 6 hours | Weekly KPI dashboard models, funnel conversion models, Segment-to-BigQuery event flow |
   | **P2: Internal / analytical** | Salesforce-to-BigQuery sync; marketing attribution tables; operational reporting models | A breakage here slows analyst work but doesn't immediately surface to executives. | Caught within 24 hours (next business day) | Salesforce connector, Growth/Marketing models, Ops reporting tables |
   | **P3: Low-frequency / archival** | Historical backfills, one-off analysis tables, deprecated Segment events not yet cleaned up | Breakage has minimal immediate impact. | Weekly audit check | Legacy tables, staging models not yet in production use |

   Deliverables: automated alerts (Slack channel + email) for P0 and P1 pipelines; daily digest for P2; weekly audit for P3. Defined escalation path: AE is first responder for P0/P1 during business hours, with a documented runbook so an analyst can triage if the AE is unavailable.

---

## Key Responsibilities

- Own and extend the dbt project: build, test, document, and maintain transformation models that serve as the company's authoritative metric definitions
- Partner with analysts, PMs, and business stakeholders to translate business glossary definitions into model logic, ensuring every metric has one number and one definition
- Monitor and maintain data pipeline reliability across Fivetran, Segment, and BigQuery, including incident response and root cause analysis
- Audit and improve Segment event tracking: clean up redundant/broken events, establish a tracking plan for new instrumentation, and document the current state
- Build and maintain dashboards that serve self-serve analytics for product managers, reducing the analyst team's ad-hoc request burden
- Collaborate with Legal/Privacy on data flow documentation, PII inventory, and EU data residency requirements as they affect the transformation layer
- Document all models, pipeline logic, and data quirks so that no critical knowledge lives in one person's head

---

## Required Qualifications

- 3+ years of professional experience in analytics engineering, data engineering, or a technical analyst role where you owned the transformation layer *(tied to: all 90-day outcomes require someone who has done this before, not someone learning on the job)*
- Production dbt experience: you have built, tested, and maintained dbt projects with at least 30+ models in a team environment *(tied to: outcome #1, completing and extending the existing dbt project)*
- Strong SQL (complex joins, window functions, CTEs, performance optimization) and comfort working directly in a cloud warehouse (BigQuery preferred, Snowflake or Redshift acceptable) *(tied to: outcomes #1-4)*
- Experience reconciling conflicting data sources or metric definitions across teams. You have been in the room where Product says one number and Finance says another, and you know how to diagnose why and fix it in the model layer *(tied to: outcome #1, business glossary implementation)*
- Ability to read a business glossary entry and translate it into correct model logic, and to push back when a definition is ambiguous or contradictory *(tied to: outcome #1)*
- Comfort working with messy, partially built infrastructure. You have inherited someone else's unfinished project and made it work. *(tied to: the entire MarketBridge data environment)*

---

## Preferred Qualifications

- Experience with Segment (or similar CDP) event tracking audits and cleanup
- Familiarity with Fivetran or similar managed ELT connectors
- Exposure to marketplace or two-sided platform business models (understanding of supply-demand dynamics, unit economics, provider vs. consumer metrics)
- Experience with data pipeline monitoring and alerting tools (Monte Carlo, Elementary, Great Expectations, or custom dbt-based monitoring)
- Familiarity with GDPR, data residency requirements, or privacy-by-design principles in a data engineering context

---

## What We Offer

- Competitive salary benchmarked to 60th-75th percentile for analytics engineering roles in the company's market, with equity participation (Series B stage, meaningful upside)
- Direct impact on a company processing 500K transactions/month across 15 metro areas, with 3 new market launches this year
- A Head of Analytics (your manager) who is invested in building a proper data function, not just adding headcount. You will have a voice in tooling, architecture, and process decisions.
- Professional development budget for conferences, certifications (dbt Analytics Engineering Certification, GCP Professional Data Engineer), and training
- Hybrid work arrangement with async-first communication norms

---

## About the Team

> You will join a four-person analytics team: a Head of Analytics (your manager, recently hired) and three embedded analysts supporting Product, Growth, and Operations respectively. The team is in transition. The previous Head of Analytics left after eight months, and the analysts have been operating independently without shared standards, peer review, or centralized infrastructure. Morale is recovering but skepticism about new initiatives is real. You will be the first dedicated analytics engineering hire, which means you are not competing with existing workflows: you are building the foundation that makes everyone else's work more reliable. The culture values shipping over perfection, honest communication over politics, and documentation over tribal knowledge. We would rather have a tested, documented model in production this week than a perfect architecture diagram next quarter.

---

## Evaluation Criteria

Use these dimensions to self-assess your job description. For official grading criteria, see `assessment/grading-rubrics.md` (Hiring Packet component, 20%).

| Criterion | What We Are Looking For |
|:---|:---|
| **Outcome Orientation** | Are the 90-day outcomes specific, measurable, and realistic? Do they drive the rest of the document? |
| **Honest Scoping** | Are "required" qualifications truly required? Is the level appropriate for the outcomes described? |
| **Case Context Fit** | Does the JD reflect the specific constraints and opportunities of your chosen company context? |
| **Candidate Appeal** | Would a strong candidate reading this JD understand the role and be excited to apply? |
| **Completeness** | Are all sections filled in with thoughtful, specific content (not generic boilerplate)? |

---

*AI assistance: I used Claude (Opus 4.6) as an iterative thinking partner to develop, pressure-test, and refine the ideas, structure, and language in this document. All analytical judgments, prioritization decisions, and strategic reasoning are my own.*
