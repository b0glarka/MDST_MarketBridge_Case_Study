# RACI Matrix

| Field | Your Entry |
|---|---|
| **Student Name** | Boga Petruska |
| **Date** | 2026-04-02 |
| **Case Context** | Medium (Series B) -- MarketBridge |

---

## RACI Matrix

| Decision / Activity | Head of Analytics (me) | Analytics Engineer | Embedded Analysts (3) | CTO (Raj) | VP Product (Diane) / Senior PM | CFO (Christine) | Legal (Anya) | Engineering |
|---|---|---|---|---|---|---|---|---|
| 1. Define or change a board-facing metric | A | R | C | I | C | C | I | I |
| 2. Prioritize analytics request intake | A | I | R | I | C | -- | -- | -- |
| 3. Ship a new PM-facing dashboard | A | R | C | I | C | I | -- | -- |
| 4. Approve new data source or pipeline | A | R | I | C | I | -- | C | R |
| 5. Mixpanel sunset / tooling change | R | R | I | A | C | I | -- | C |
| 6. Hire a new team member | R | -- | C | A | I | I | -- | -- |
| 7. Data access and PII handling | R | R | I | I | I | -- | A | C |
| 8. Experiment design and launch | A | C | R | I | C | -- | I | I |

---

## Key Decisions

### 1. Metric Definitions and Changes

- **What:** Defining or changing how a board-facing metric is calculated (e.g., "completed transaction," "active user," "churn"). This is the decision that caused the 487K vs. 523K board incident.
- **R:** Analytics Engineer. Translates the agreed definition into dbt model logic, writes tests, documents in schema YAML.
- **A:** Head of Analytics (me). I own the glossary process and sign off on the final definition. No metric goes to the board without my approval.
- **C:** VP of Product (Diane) or Senior PM: validates the definition reflects product intent. CFO (Christine): validates financial metric alignment. Embedded Analysts: flag implementation concerns or upstream data issues.
- **I:** CTO (Raj), Engineering, downstream dashboard consumers.
- **Why this structure:** The previous failure mode was that no one owned metric definitions. Product, Finance, and Growth each defined metrics independently. Making the Head of Analytics accountable with cross-functional consultation prevents this from happening again.

### 2. Prioritization of Analytics Requests

- **What:** Deciding which ad-hoc analysis requests the team takes on this week/sprint, and which get deferred, scoped down, or redirected to self-serve.
- **R:** Embedded Analysts. They triage incoming requests, estimate effort, and flag conflicts with planned work.
- **A:** Head of Analytics (me). I make the final call when requests compete, especially when requests from Diane and Marco conflict.
- **C:** VP of Product (Diane) or Senior PM. As the primary request source, they need to understand trade-offs when their requests are deprioritized.
- **I:** CTO (Raj).
- **Why this structure:** Analysts currently operate as ticket-takers with no prioritization framework. Making them responsible for triage (with my accountability for final decisions) gives them agency while ensuring strategic alignment.

### 3. New Dashboard or Report Going to Production

- **What:** Approving a new dashboard for stakeholder consumption, built on dbt models with trusted data.
- **R:** Analytics Engineer. Builds the dashboard on the dbt semantic layer, ensures data quality.
- **A:** Head of Analytics (me). I sign off that the dashboard uses glossary-approved metrics and is ready for stakeholder use.
- **C:** VP of Product (Diane) or Senior PM: validates that the dashboard answers the questions they need answered. Embedded Analysts: review data logic and flag edge cases.
- **I:** CTO (Raj), CFO (Christine) if board-adjacent.
- **Why this structure:** The previous failure mode was dashboards shipped without validation against agreed definitions. The AE builds, I validate against the glossary, and the PM confirms it meets their needs.

### 4. Approve New Data Source or Pipeline

- **What:** Adding a new data source to BigQuery (e.g., a new Fivetran connector, a new Segment event stream) or making a material change to an existing pipeline.
- **R:** Analytics Engineer (transformation layer) and Engineering (infrastructure layer). The AE owns the dbt models; Engineering owns Fivetran config and BigQuery admin.
- **A:** Head of Analytics (me). I decide whether the data source is needed and prioritize it against other work.
- **C:** CTO (Raj): cost implications (Fivetran connector pricing, BigQuery compute). Legal (Anya): PII and data residency implications, especially for EU data sources.
- **I:** Embedded Analysts, VP of Product.
- **Why this structure:** The boundary between AE work and Engineering work is the most likely source of scope creep (Weakness #4 from the hiring packet). Explicit R assignments for each layer prevent the AE from becoming a de facto data engineer.

### 5. Mixpanel Sunset / Tooling Change

- **What:** Deciding to renew, downgrade, or sunset a major analytics tool. Currently: the Mixpanel contract renewal decision (see decision memo).
- **R:** Head of Analytics (me): owns the analysis, recommendation, and migration plan. Analytics Engineer: executes the technical migration (builds dbt replacement, validates parity).
- **A:** CTO (Raj). Major tooling decisions with budget implications require his approval. I recommend, he decides.
- **C:** VP of Product (Diane): PM team is the primary user of Mixpanel, so their workflow impact must be considered. Engineering: infrastructure implications of migration.
- **I:** Embedded Analysts, CFO (Christine).
- **Why this structure:** Raj is accountable because this is a Type 1 decision with budget implications that exceed my authority. I am responsible for the analysis and recommendation, but he owns the final call. This is consistent with the stakeholder map: I frame proposals in cost terms for Raj.

### 6. Hire a New Team Member

- **What:** Defining the role, running the interview loop, and making the hire for the 2 open headcount slots.
- **R:** Head of Analytics (me). I define the JD, design the interview loop, run the debrief, and make the hiring decision (see hiring packet).
- **A:** CTO (Raj). As my manager and the person who controls headcount, he has final approval (and veto power per the interview loop design).
- **C:** Embedded Analysts (Senior Analyst participates in Stage 4 of the interview loop). HR (logistics, comp bands, offer letters).
- **I:** VP of Product (Diane), CFO (Christine).
- **Why this structure:** The Head of Analytics is responsible for building the team, but hiring at this level requires CTO approval because it uses a hiring freeze exception. The Senior Analyst is consulted (not accountable) per the interview loop guardrails: their input is valued but the hiring decision is mine.

### 7. Data Access and PII Handling

- **What:** Granting access to sensitive data, making decisions about PII in analyses, and ensuring compliance with GDPR and EU data residency requirements.
- **R:** Head of Analytics (me): sets data access policies for the analytics team. Analytics Engineer: implements access controls, PII tagging, and data deletion pipelines in the dbt layer.
- **A:** Legal (Anya). She is ultimately accountable for compliance outcomes. Her sign-off is required for any change to PII handling, data retention, or cross-border data flows.
- **C:** Engineering: implements infrastructure-level access controls (BigQuery IAM, Fivetran connector permissions).
- **I:** CTO (Raj), VP of Product (Diane), Embedded Analysts.
- **Why this structure:** The Q3 GDPR audit makes Anya the accountable party for all PII decisions. I am responsible for ensuring the analytics team's workflows comply, but she owns the compliance outcome. This is the "privacy by design" principle from the team charter: embed privacy into the process, don't treat it as a gate.

### 8. Experiment Design and Launch

- **What:** Approving the design of an A/B test or experiment (sample size, duration, success criteria, statistical methodology).
- **R:** Embedded Analysts. They design the experiment, calculate sample sizes, define success criteria, and run the analysis.
- **A:** Head of Analytics (me). I sign off on the statistical methodology and ensure the experiment is properly powered and designed before it launches. No experiment goes live without my review.
- **C:** Analytics Engineer: ensures the data pipeline supports the experiment's measurement needs. VP of Product (Diane) or Senior PM: validates the business hypothesis and agrees on the success criteria.
- **I:** CTO (Raj), Engineering (if the experiment requires instrumentation changes), Legal (Anya, if the experiment involves PII or EU users).
- **Why this structure:** Experimentation is a Later initiative on the roadmap, but when it arrives, the Head of Analytics must own the statistical rigor. The previous failure mode (no shared standards) means experiments without oversight will produce unreliable results. Analysts do the work; I ensure the methodology is sound.

---

## Escalation Path

### When to Escalate

- The A and a C fundamentally disagree after discussion (e.g., Diane wants a metric defined one way, Christine wants it defined another, and neither will budge after I facilitate the conversation)
- A decision is blocked because no one claims accountability
- A Type 1 (irreversible) decision needs higher authority than the designated A
- A stakeholder outside the RACI tries to override the decision (e.g., a PM requests a dashboard change that contradicts a glossary-approved definition)

### Escalation Levels

| Level | Who | When | How |
|---|---|---|---|
| **Level 1** | Head of Analytics (me) | First attempt to resolve within the team or with the disagreeing stakeholders. Most metric definition disputes and prioritization conflicts should resolve here. | Sync meeting or brief written summary of the disagreement and my proposed resolution. |
| **Level 2** | CTO (Raj) | Cross-functional disagreement that I cannot resolve (e.g., Product and Finance disagree on a board-facing metric definition and both refuse my proposed compromise). | One-page decision memo (see decision memo template) with options and my recommendation. 15-minute meeting in our weekly 1:1. |
| **Level 3** | CEO / Executive team | Strategic disagreement with company-wide implications (e.g., whether to invest in a data platform vs. outsource analytics). Not expected to occur in the first 12 months. | Decision memo to executive sponsor via CTO. |

### Escalation Principles

- **Escalate with options, not problems.** Always bring at least two options and my recommendation. Never escalate a question without a proposed answer.
- **Escalate promptly.** A decision blocked for two weeks is worse than escalating on day two. The team cannot afford the previous pattern of decisions dying in ambiguity.
- **Escalate in writing.** Verbal escalations get lost. A one-paragraph summary ensures everyone has the same context and creates a record for the decision log.
- **No skipping levels.** Level 1 must be attempted before Level 2. If I escalate to Raj without first trying to resolve it myself, I am delegating my job upward.
- **Escalation is not failure.** Some disagreements genuinely require a higher authority to resolve. Escalating a Product vs. Finance metric definition dispute to the CTO is the right call when both sides have legitimate claims.

---

*AI assistance: I used Claude (Opus 4.6) as an iterative thinking partner to develop, pressure-test, and refine the ideas, structure, and language in this document. All analytical judgments, prioritization decisions, and strategic reasoning are my own.*
