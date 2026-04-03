# Manager Operating System: MarketBridge Analytics Team

**Student Name:** Boga Petruska\
**Date:** 2026-04-02\
**Case Context:** Medium (Series B) -- MarketBridge\
**Role:** Head of Analytics (newly hired)\
**Team:** 3 embedded analysts + 1 Analytics Engineer (hiring in progress)\
**Budget:** $25K/month tooling (Segment, Mixpanel, Fivetran, BigQuery)

---

## 1. Team Overview

The Analytics team exists to turn fragmented data into a single source of truth that drives marketplace growth and profitability decisions. The team has been operating without leadership for months. The previous Head of Analytics left after eight months. Three embedded analysts work independently without shared standards. The board recently received conflicting transaction counts (487K vs. 523K, a 7.4% gap). Trust in the data function is at its lowest point.

| In Scope | Out of Scope |
|---|---|
| Unified metric definitions, business glossary, semantic layer (dbt + BigQuery) | Production ML model deployment (Engineering) |
| Product analytics, experimentation, retention reporting | Backend database administration (Engineering) |
| Executive reporting, KPI dashboards, board-facing metrics | Salesforce/CRM administration (Sales Ops) |
| Data tooling decisions within $25K/month budget | NetSuite and financial ledger management (Finance) |
| GDPR compliance for analytics workflows (with Legal) | Ad-hoc requests from teams outside the intake process |

**Operating principles:** (1) One number, one definition. (2) Infrastructure is product work: protect 30% capacity for infrastructure/debt. (3) Privacy by design, not by review. (4) Say no with alternatives. (5) Show the work: if it is not in the repo, it does not exist.

**Scaling note:** This OS is designed for a 4-person team. As the team grows to 6-8, the main structural change is splitting into infrastructure and analytics pods with a tech lead for day-to-day Type 2 decisions. Core invariants (one number/one definition, decision hygiene, stakeholder tiering, weekly 1:1 with Raj) do not change.

**North Star and guardrails:**

| Element | Metric | Baseline | Target |
|---|---|---|---|
| North Star | Self-serve adoption rate (% of recurring questions answered without analyst involvement) | ~0% | 65-70% by month 12 |
| Guardrail 1 | Ad-hoc response time | ~2-5 days | Must not exceed baseline during transition |
| Guardrail 2 | Data stack cost | $25K/month | No increase without CTO-approved offset |
| Guardrail 3 | Analyst retention | 3 analysts | Zero attrition during 12-month transformation |
| Input metric | Trusted dbt models in production | 0 | Growing quarterly |
| Input metric | Glossary coverage (% of recurring questions with defined metric) | ~0% | 100% of board metrics by Q2 |
| Input metric | Dashboard adoption (weekly active PM users) | 0 | 5+ by AE day 90 |

---

## 2. Cadence Calendar

| Meeting | With | Freq. | Dur. |
|---|---|---|---|
| 1:1 (structured: on track / at risk / what I need) | CTO (Raj) | Weekly | 30 min |
| 1:1s: coaching, SBI feedback, career. Their agenda first. | Each analyst (x3) | Weekly | 30 min ea. |
| 1:1: dbt progress, pipeline issues, priorities | Analytics Engineer | Weekly | 30 min |
| Team sync: wins, blockers, announcements. Hard stop. | Full team | Weekly | 30 min |
| Analytics sync: dashboards, experiments, PM needs | VP Product (Diane) | Weekly | 30 min |
| Privacy sync: GDPR, data residency, PII inventory | Legal (Anya) | Weekly* | 30 min |
| Data review: launch metrics, attribution | Growth (Marco) | Bi-weekly** | 30 min |
| Infra sync: pipeline reliability, schema changes | Engineering | Bi-weekly | 30 min |
| Data quality: Salesforce-BigQuery, supply-side | Sales Ops | Bi-weekly | 30 min |
| Financial-product: unit economics, glossary | CFO (Christine) | Monthly | 45 min |
| Glossary governance: propose/approve/reject definitions | PMs (invited) | Monthly | 45 min |
| Retrospective: blameless, vote on top items | Full team | Monthly | 45 min |
| Roadmap planning: RICE re-scoring, OKR alignment | Full team | Quarterly | Half day |
| Performance calibration: SBI evidence, norm by level | CTO (Raj) | Quarterly | 60 min |
| QBR prep: lock board numbers, exec narrative | CTO, CFO | Quarterly | 60 min |

*Drops to bi-weekly after GDPR audit passes. **Weekly during active market launches.

**Event-triggered:** Pipeline P0: immediate Slack escalation + postmortem within 48 hrs. Hiring windows: activate HR. Total stakeholder time: ~8-9 hrs/week (~20-25%).

---

## 3. People Management Frameworks

### Feedback: SBI Model

All feedback uses Situation-Behavior-Impact-(Development Recommendation):

Example: "In last week's metrics review (S), you presented the funnel analysis without noting that Segment tracking was broken for 3 days during the measurement period (B). Christine used those numbers in board prep and we had to issue a correction (I). Next time, add a data quality caveat to any analysis where the underlying data has known gaps (D)."

### Career Ladder (IC Track)

| Level | Title | Scope | Autonomy |
|---|---|---|---|
| L2 | Analyst | Well-defined analyses. Single stakeholder. | Needs direction on what. Executes independently. |
| L3 | Senior Analyst | Owns a domain. Multi-stakeholder. Mentors L2s. | Self-directs within domain. |
| L4 | Staff / Senior AE | Cross-domain impact. Sets technical standards. | Self-directs across domains. Influences strategy. |

Level = scope + autonomy, not years of experience. Performance rated relative to current level: a high-output L3 is not automatically L4 if they lack L4 behaviors (see Kevin's performance summary).

### PGP vs. PIP

PGP (Personal Growth Plan): aspirational, proactive, everyone has one. PIP (Performance Improvement Plan): corrective, rare, HR-involved, time-bound. Before any PIP: were expectations clear, was SBI feedback given early, was support provided, is there documentation? If not, the problem is my management.

### Communicating Failure Upward

Four steps to Raj when something breaks: (1) Impact: who sees it. (2) What happened: factual. (3) Immediate fix. (4) Systemic fix. If Raj hears about a data problem from someone else first, I have failed at communication.

---

## 4. Stakeholder Engagement

### Priority Tiers

| Tier | Stakeholders | Why | Weekly Time |
|---|---|---|---|
| **P0** | CTO (Raj), Embedded Analysts (3), VP Product (Diane) | Manager, team, sponsor. | ~5.5 hrs |
| **P1** | Legal (Anya), Head of Growth (Marco), Engineering | GDPR deadline, launches, upstream data quality. | ~2 hrs |
| **P2** | CFO (Christine), Sales Ops, PMs, Launch Mgrs | Power/disengaged, data dependency, end users. | ~1 hr |
| **P3** | HR, Ops/Support, Board, EU Regulators | Operational gates, indirect influence. | Ad-hoc |

Tiers shift with events: launches move Marco to weekly, GDPR audit keeps Anya weekly, hiring activates HR.

### Regulatory/ESG

EU expansion exposes DSA, DAC7, Platform Work Directive, and algorithmic fairness concerns that shape current architecture decisions. Full analysis in stakeholder map.

---

## 5. Decision Hygiene

### RACI

| Decision | A (Accountable) | R (Responsible) | C (Consulted) | I (Informed) |
|---|---|---|---|---|
| Define/change board metric | Head of Analytics | AE | VP Product, CFO, Analysts | CTO, Engineering |
| Prioritize request intake | Head of Analytics | Analysts | VP Product / Senior PM | CTO |
| Ship PM-facing dashboard | Head of Analytics | AE | VP Product / Senior PM, Analysts | CTO, CFO |
| New data source / pipeline | Head of Analytics | AE + Engineering | CTO (cost), Legal (PII) | Analysts, VP Product |
| Tooling change (e.g., Mixpanel) | CTO (Raj) | Head of Analytics, AE | VP Product, Engineering | Analysts, CFO |
| Hire team member | CTO (Raj) | Head of Analytics | Senior Analyst, HR | VP Product, CFO |
| Data access / PII handling | Legal (Anya) | Head of Analytics, AE | Engineering | CTO, VP Product |
| Experiment design / launch | Head of Analytics | Analysts | AE, VP Product / Senior PM | CTO, Engineering |

### Type 1 vs. Type 2

Type 1 (irreversible: hiring, vendor commitments, board metric definitions): decide slowly, write a decision memo: (1) Context, (2) Options (min. 3), (3) Recommendation, (4) Risks. Example: Mixpanel renewal (see decision-memo_boga.md). Type 2 (reversible: tool experiments, process changes, dashboards): decide fast, iterate. Bias toward action on Type 2: the backlog of unmade decisions is a bigger risk than a wrong but reversible one.

### Escalation

| Level | Who | When | How |
|---|---|---|---|
| 1 | Head of Analytics | Within team or with stakeholders | Sync meeting or written summary |
| 2 | CTO (Raj) | Cross-functional disagreement I cannot resolve | Decision memo + 15 min in weekly 1:1 |
| 3 | CEO / Exec team | Strategic, company-wide. Not expected year 1. | Decision memo via CTO |

---

## 6. Artifacts Registry

| Artifact | Update Frequency | Owner |
|---|---|---|
| Business glossary (metric definitions + SQL logic) | Ongoing; monthly governance | Head of Analytics |
| Team charter | Quarterly | Head of Analytics |
| Stakeholder map (power/interest, priority tiers) | Quarterly or after reorgs | Head of Analytics |
| Roadmap (RICE scores, Now/Next/Later) | Quarterly refresh | Head of Analytics |
| Decision log (Type 1 decisions) | Ongoing | Head of Analytics |
| 1:1 docs (running notes per report) | Weekly | Each report + HoA |
| Manager log (accomplishments, SBI given, growth evidence per person) | Ongoing after 1:1s | Head of Analytics (private) |
| Pipeline runbook (P0/P1 response, escalation) | Created by AE; updated as infra changes | Analytics Engineer |
| PII flow inventory | Created for Q3 audit; updated when pipelines change | Head of Analytics + Legal |

---

*AI assistance: I used Claude (Opus 4.6) as an iterative thinking partner to develop, pressure-test, and refine the ideas, structure, and language in this document. All analytical judgments, prioritization decisions, and strategic reasoning are my own.*
