# Data Infrastructure Decision Brief

| Field | Details |
|-------|---------|
| **Student Name** | Boga Petruska |
| **Date** | 2026-03-23 |
| **Case Context** | Medium (Series B) -- MarketBridge |

---

## 1. Current State

**What exists today:**

| Layer | Tool | Status |
|---|---|---|
| Sources | PostgreSQL (product), Salesforce (supply-side), Stripe (payments), NetSuite (finance) | Four disconnected source systems. Finance and supply-side data are not integrated with product data. |
| Event Collection | Segment (~340 events) | Under-maintained. ~30% of events are redundant, misconfigured, or irrelevant. Built by an engineer who left. |
| Ingestion | Fivetran (PostgreSQL, Stripe, Salesforce, SaaS tools) | Functional but unmonitored. Breakages go unnoticed for days. No alerts configured. |
| Storage | BigQuery (warehouse) + PostgreSQL read replica (ad-hoc analyst queries) | Two parallel access patterns. Analysts query the read replica directly with no shared conventions. |
| Transform | dbt (~20 staging models, abandoned 6 months ago, several broken) | Not running. Predecessor started it, left after 8 months. Team is skeptical of infrastructure projects that don't get finished. |
| Semantic Layer | None | Three definitions of "active user." Product counts initiated bookings, Finance counts completed paid transactions. No business glossary. |
| Visualization | Mixpanel (product analytics) + ad-hoc SQL via DataGrip/DBeaver/psql | PMs have stopped trusting Mixpanel because numbers conflict with SQL. No self-serve capability. Mixpanel contract renewal in 6 weeks. |
| Observability | None | Zero alerting. Zero freshness monitoring. Zero schema change detection. |
| Governance | None formalized | No shared metric definitions, no data owners, no access controls, no peer review, no coding standards. Each analyst maintains their own SQL and Google Sheets. |
| Privacy/Compliance | Gaps flagged by Legal | Consent records incomplete. Data deletion manual and inconsistent. No PII flow inventory. GDPR audit in Q3. EU data residency required for Berlin/Amsterdam but entire stack is US-based. |

**Monthly cost:** $25,000 total for all data tooling. Costs doubled YoY.

**Biggest pain point:** No single source of truth. The missing semantic layer is the root cause of nearly every downstream problem. Mixpanel and SQL give different answers to the same question. PMs debate numbers instead of acting on them. Board metrics conflict across presentations. Analysts spend 80% of their time on ad-hoc requests because stakeholders cannot self-serve from dashboards they don't trust. Until there is one agreed definition of each metric, implemented in one place (dbt), every dashboard, report, and analysis is built on sand.

---

## 2. AI Impact

**Primary lens: Infrastructure** (AI as an accelerant for the team's core capability gap)
**Secondary lens: Governance** (AI as a compliance risk that must be contained before it can be leveraged)

The secondary lens comes first because it is a precondition: you cannot benefit from AI infrastructure if a data handling mistake triggers a GDPR incident three months before the audit. But it is fast and cheap to address, so it clears the path for the real strategic question: how does AI change what this team can deliver?

### 2a. Governance guardrail (precondition, week 1)

The team almost certainly uses AI coding assistants (Claude, Copilot, ChatGPT) for SQL, analysis drafts, and data exploration. There is no policy governing this. MarketBridge handles PII (homeowner addresses, service professional earnings, payment data) and is 3 months from a GDPR audit.

The risk: an analyst pastes a SQL query containing customer email addresses or provider earnings into an AI prompt. That data leaves the company's infrastructure and is sent to a third-party API without a lawful basis, a data processing agreement, or documentation. Under GDPR, that is a reportable incident.

**Action:** Draft an AI usage policy in week 1. No PII, no financial data, no Confidential/Restricted data in external AI tools. Anya reviews DPAs for whichever AI tools the team standardizes on. Practical guidance, not a ban: use AI for code patterns, SQL syntax, methodology questions. Use anonymized or synthetic data when debugging.

**Cost:** Zero (staff time + Legal review). Enterprise AI coding assistant plans (~$19/user/month, ~$80-100/month for 4-5 users) are negligible against the $25K/month tooling budget.

**Timeline:** Policy drafted and approved within 2 weeks. This is a memo and a Legal review, not a project.

### 2b. Infrastructure: AI as accelerant for the dbt rebuild (primary lens)

The strategic question is not "should we use AI?" The team already does. The question is: how does AI change the speed and cost of building the infrastructure we're missing?

MarketBridge's core infrastructure gap is the semantic layer: 20 abandoned dbt models, no business glossary, no metric definitions. The AE hire is the primary solution. AI changes the economics of that rebuild.

**AI-assisted dbt development:**

The AE will use AI coding assistants as part of their daily workflow. Applied to MarketBridge's dbt rebuild, this means:

- Auditing and fixing the 20 existing staging models: AI can read broken models, diagnose upstream schema changes, and propose fixes. What would take 2-3 days of manual investigation per model compresses to hours.
- Generating schema YAML documentation: dbt requires YAML files describing every model, column, and test. This is high-value but tedious work. AI generates the boilerplate; the AE reviews and corrects against business definitions.
- Writing dbt tests: for each model, tests for not-null, unique, accepted values, referential integrity. AI generates the standard test suite; the AE adds business-logic tests that require domain knowledge.
- Segment event audit: reviewing 340 events to identify redundant, broken, and missing tracking. AI can parse event schemas and flag anomalies; the analyst validates against product context.

**Build-vs-buy assessment (applying the four questions from Block E):**

| AI Capability | Core differentiator? | Commodity? | Team to maintain? | TCO | Decision |
|---|---|---|---|---|---|
| AI coding assistant (Copilot/Claude) | No | Yes | N/A (SaaS) | ~$100/month | Buy. Immediate productivity gain for AE and analysts. |
| LLM-powered data querying (natural language to SQL) | No | Emerging | No | $200-500/month + integration effort | Not yet. Requires the semantic layer to exist first. Without trusted dbt models underneath, LLM-generated SQL queries inherit the same metric chaos we're trying to fix. Revisit in Q3-Q4 once the glossary covers the top 15 metrics. |
| AI-assisted anomaly detection (data observability) | No | Yes | No | $0 (Elementary, dbt-native) to $1,500/month (Monte Carlo) | Buy Elementary now (free, runs inside dbt). Consider Monte Carlo at scale. But first: configure the alerting that already exists in Fivetran and dbt tests. |
| Custom ML/AI models for product features | Yes (if MarketBridge builds recommendation/matching) | No | Not with current team | High | Not now. This is a Later initiative. The analytics team's job is metrics and insights, not production ML. |

**The sequencing argument:** AI accelerates infrastructure work, but it does not skip it. The AE still needs to build the dbt models. AI makes that 30-40% faster (based on typical productivity gains from coding assistants on structured, repetitive work like dbt model writing and test generation). That means the dbt rebuild that might take 3 person-months compresses to ~2 person-months. This directly affects the roadmap: initiative #1 (single source of truth) delivers faster, which unblocks initiative #5 (first PM dashboard) sooner, which moves the North Star (self-serve adoption) earlier.

What AI does not accelerate: cross-functional metric definition sign-off. Getting Diane, Christine, and Marco to agree on what "active user" means is a human negotiation. AI makes the implementation faster once the definition is agreed.

### 2c. Architectural awareness: EU AI regulatory exposure (no action now)

The EU AI Act is in phased implementation. If MarketBridge uses algorithmic ranking for "premium placement" of service professionals, this may fall under transparency requirements. Not an immediate action item, but the dbt semantic layer design should not foreclose the ability to audit and explain algorithmic outputs in 12-18 months. Flag to Anya during the next Legal sync alongside GDPR, DSA, and DAC7.

---

## 3. VP Proposal (BLUF)

Raj, the board sees conflicting numbers because we have no single source of truth. I need the AE hire approved at competitive comp and $100/month for AI coding tools to rebuild our dbt layer in 2 months instead of 3, an Engineering SLA on schema changes so pipelines stop breaking silently, and an AI usage policy approved with Legal before the team handles MarketBridge data in these tools (zero cost, just Anya's review). Total incremental cost: ~$2,500/month, offset by the Mixpanel downgrade the AE enables. Without this, board metrics keep conflicting, pipeline breakages surface in executive meetings before we know, and uncontrolled AI usage becomes a GDPR finding in Q3.

**Supporting detail (for discussion, not the pitch):**

| Ask | Cost | What it delivers |
|---|---|---|
| AE hire at competitive comp | $20-30K/year above budgeted level | Completes abandoned dbt project. One definition per board metric. Enables Mixpanel sunset. |
| Enterprise AI coding assistant (5 users) | ~$100/month | Compresses dbt rebuild by ~1 month. AE uses it to audit 20 broken models, generate tests, document schemas. |
| Engineering bidirectional SLA | $0 (30-min monthly sync) | They notify us 2 sprints before schema changes. We review impact within 3 business days. Fivetran alerts configured as part of dbt rebuild. |
| AI usage policy + DPA review | $0 (staff time + Legal) | Precondition before expanding AI tool usage. No PII in external prompts. Closes a gap the Q3 GDPR auditor would flag. |

---

*AI assistance: I used Claude (Opus 4.6) as an iterative thinking partner to develop, pressure-test, and refine the ideas, structure, and language in this document. All analytical judgments, prioritization decisions, and strategic reasoning are my own.*
