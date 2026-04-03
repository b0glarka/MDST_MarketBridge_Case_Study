# Scoring Rubric

**Student Name:** Boga Petruska\
**Date:** 2026-03-16\
**Case Context:** Medium (Series B) -- MarketBridge\
**Target Role:** Analytics Engineer\
**Target Level:** Mid (Senior offer if candidate demonstrates Expert-level Technical Execution and Definition Rigor)

---

## Scoring Dimensions

*6 dimensions, each mapped to specific 90-day outcomes and key responsibilities from the job description. The hiring bar is 3 (Proficient) on all dimensions. A score of 2 on any single dimension is acceptable only if compensated by 4s elsewhere and the dimension is not Technical Execution or Definition Rigor (those two are non-negotiable at 3+).*

### Dimension Definitions and Behavioral Anchors

| Dimension | Maps To | 1 - Novice | 2 - Developing | 3 - Proficient | 4 - Expert |
|:---|:---|:---|:---|:---|:---|
| **Technical Execution (dbt, SQL, pipeline)** | Outcomes #1, #4, #5 | SQL has errors in joins or aggregations; no experience with dbt or similar transformation tools; cannot explain how a DAG works; does not consider data quality or testing | SQL is correct but unoptimized; has used dbt but only tutorials or small projects (<10 models); aware of testing but has not implemented it systematically; needs hand-holding on warehouse-specific features | Production dbt experience with 30+ models; writes clean, tested, documented SQL; understands incremental models, snapshots, and macro patterns; can diagnose a broken dbt project by reading the DAG and logs; comfortable with BigQuery (or equivalent warehouse) performance tuning | Has designed dbt projects from scratch for multiple organizations; contributes to dbt community packages or writes custom macros; can evaluate and recommend monitoring tooling; deep warehouse optimization expertise; has migrated between data platforms |
| **Communication Clarity** | Outcomes #3, #4 | Cannot explain technical decisions to a non-technical audience; documentation is absent or incomprehensible; writes model descriptions that only they can understand | Can explain what a model does but not why it matters; documentation exists but is inconsistent; struggles to frame technical trade-offs in business terms (e.g., explains the Mixpanel audit as a technical comparison without connecting to cost or PM workflow impact) | Writes clear model documentation that an analyst can use without asking questions; can present the Mixpanel audit findings to the CTO in business terms (cost, risk, PM impact); schema YAML descriptions are useful, not boilerplate | Documentation is a first-class artifact, not an afterthought; can write a one-page decision memo that a CFO would find persuasive; proactively creates onboarding guides and runbooks without being asked |
| **Definition Rigor (business glossary translation)** | Outcome #1 | Implements metric logic without questioning the definition; does not notice when a business definition is ambiguous or contradicts the data; builds whatever is asked without validation | Notices ambiguity in definitions but does not raise it or resolves it by guessing; implements one stakeholder's version without checking whether others agree; tests for correctness against the code logic but not against the business intent | Reads a business glossary entry and identifies gaps or contradictions before writing code; asks "what happens at the boundary?" questions (e.g., "does a cancelled-then-rebooked transaction count as one or two?"); builds models that match the agreed definition and flags when upstream data makes the definition unreliable | Has led metric definition alignment processes across teams; can facilitate a conversation between Product and Finance about what "active user" means and translate the outcome into model logic the same day; treats the semantic layer as a contract between data and the business |
| **Mess Tolerance (inherited infrastructure)** | Outcomes #1, #2, #5; Weakness #6 | Has only worked with greenfield projects or well-maintained codebases; becomes frustrated or paralyzed when confronted with undocumented, partially broken infrastructure; wants to rewrite everything from scratch before doing anything useful | Can work with messy systems but defaults to workarounds rather than fixes; documents problems but does not prioritize remediation; may underestimate how long cleanup takes or overestimate how quickly they can replace legacy systems | Has inherited and improved someone else's data infrastructure; can read an abandoned dbt project, identify what works, what is broken, and what should be deleted; makes pragmatic decisions about what to fix now vs. later; comfortable with "good enough for now" when appropriate | Has a repeatable methodology for infrastructure triage; can walk into a new environment, produce a written assessment in the first week, and execute a phased remediation plan; has done this at multiple companies and can pattern-match common failure modes |
| **Intellectual Curiosity** | Outcome #2 | Answers only what is asked; does not explore upstream data sources; treats the Segment audit as a checklist exercise rather than an investigation | Shows curiosity about individual problems but does not connect them; might notice a broken Segment event but not investigate whether other events from the same source are also broken | Systematically explores beyond the immediate problem; during the Segment audit, would independently investigate whether broken events correlate with the engineer's departure or a specific product release; asks "what else might be affected?" | Generates insights the team had not considered; would notice that the Fivetran sync schedule and BigQuery compute costs are correlated and propose a cost optimization; proposes monitoring approaches before being asked |
| **Collaboration Signal** | Outcome #2 (knowledge transfer); Weakness #3 | Works in isolation; does not seek input from analysts or stakeholders; treats the dbt project as "their code" rather than a shared team resource | Receptive to feedback but does not proactively build relationships; would accept the senior analyst's help on Salesforce joins but not actively seek it or structure the knowledge transfer | Actively builds working relationships with the analyst team; approaches the senior analyst's Salesforce knowledge as something to learn and document together, not extract; seeks input from PMs on dashboard design before shipping; participates in code review as both reviewer and reviewee | Creates shared ownership of the data platform; establishes norms (PR reviews, documentation standards, naming conventions) that the analyst team adopts willingly; makes the senior analyst feel like a co-builder, not a knowledge source being mined |

**Guidance on scoring:**
- **1 (Novice):** Below the bar for this level. Clear no-hire signal on this dimension.
- **2 (Developing):** Approaching the bar but not yet there. Acceptable only if other dimensions are strong and this is not Technical Execution or Definition Rigor.
- **3 (Proficient):** Meets expectations for this level. This is the hiring bar.
- **4 (Expert):** Exceeds expectations. Rare. A candidate scoring 4 on Technical Execution and Definition Rigor may be operating at Senior level and should be evaluated for a Senior AE offer.

**Minimum hire threshold:** Average score of 3.0 across all dimensions, with no dimension below 2, and Technical Execution + Definition Rigor both at 3 or above. A candidate with a 2 on Mess Tolerance but 4s on Technical Execution and Definition Rigor is a borderline hire worth discussing. A candidate with a 2 on Definition Rigor regardless of other scores is a no-hire for this specific role.

---

## Interview Scorecard

*Complete one scorecard per interviewer per candidate. Scores must be submitted independently before the debrief meeting.*

### Interviewer Information

- **Interviewer Name:** _______________
- **Interviewer Role in Loop:** [ ] Hiring Manager / [ ] Technical Peer / [ ] Cross-Functional Partner / [ ] Skip-Level
- **Candidate Name:** _______________
- **Date of Interview:** _______________
- **Interview Format:** [ ] In-person / [ ] Video / [ ] Work Sample Review

### Dimension Scores

| Dimension | Score (1-4) | Evidence / Observations |
|:---|:---|:---|
| Technical Execution (dbt, SQL, pipeline) | ___ | |
| Communication Clarity | ___ | |
| Definition Rigor (business glossary translation) | ___ | |
| Mess Tolerance (inherited infrastructure) | ___ | |
| Intellectual Curiosity | ___ | |
| Collaboration Signal | ___ | |

### Overall Assessment

- **Overall Score (average):** ___
- **Meets minimum threshold?** [ ] Yes (avg >= 3.0, no dim < 2, Tech Exec + Def Rigor >= 3) / [ ] No
- **Recommendation:** [ ] Strong Hire / [ ] Hire / [ ] No Hire / [ ] Strong No Hire
- **Key Strengths (top 2):**
  1.
  2.
- **Key Concerns (top 2):**
  1.
  2.
- **Would this candidate be effective in the MarketBridge environment specifically?** (Consider: messy infrastructure, skeptical analyst team, multiple impatient stakeholders, cost-conscious CTO, 6-week Mixpanel deadline)
  -
- **Additional Notes:**

---

## Calibration Notes

*Use this section during the pre-interview norming session. Score a practice candidate together and document where the team aligns and disagrees.*

### Norming Exercise

- **Practice Candidate/Sample Used:** Give all interviewers the work sample problem (see work-sample template) and have each score independently using this rubric before the calibration session. Use a mock submission that is deliberately ambiguous on Definition Rigor (implements a metric correctly per one stakeholder's definition but ignores a known conflict) to surface whether interviewers agree on what "proficient" looks like for that dimension.
- **Date of Calibration Session:** _______________
- **Participants:** Head of Analytics (hiring manager), CTO (skip-level), senior embedded analyst (technical peer), VP of Product or PM representative (cross-functional partner)

### Score Comparison

| Dimension | Scorer A (Head of Analytics) | Scorer B (Senior Analyst) | Scorer C (CTO) | Scorer D (PM/Cross-functional) | Notes on Disagreement |
|:---|:---|:---|:---|:---|:---|
| Technical Execution | | | | | CTO and Senior Analyst may weight this differently. Align on: are we scoring dbt-specific skill or general data engineering breadth? For this role, dbt-specific skill matters more. |
| Communication Clarity | | | | | PM scorer may have a higher bar here than technical scorers. Align on: we are scoring ability to communicate to PMs, not to engineers. |
| Definition Rigor | | | | | This is the most likely dimension to generate disagreement. The CTO may score it lower because he cares more about cost and architecture. The PM may score it higher because they live with definition chaos daily. Align on: this dimension is about the candidate's ability to handle ambiguity in metric definitions, not their domain knowledge of MarketBridge metrics. |
| Mess Tolerance | | | | | Senior Analyst is the best judge here because they live in the mess. If the Senior Analyst scores a candidate low on this, weight that heavily. |
| Intellectual Curiosity | | | | | |
| Collaboration Signal | | | | | Senior Analyst's score matters most here. This person will work alongside the candidate daily. If the Senior Analyst picks up signals that the candidate would be difficult to work with, that is a strong no-hire signal regardless of technical skill. |

### Calibration Outcomes

- **Where did we agree?**
  -
- **Where did we disagree and why?**
  -
- **What scoring definitions did we clarify or update?**
  -
- **What biases did we identify in ourselves?**
  - Watch for: halo effect from strong SQL performance bleeding into Communication or Collaboration scores. A candidate who writes beautiful SQL but cannot explain their Mixpanel audit findings to Raj is not a 3 on Communication just because their code is clean.
  - Watch for: similarity bias. If the Senior Analyst prefers candidates who use the same tools or have a similar background, flag it. We need someone who can work with the existing stack, not someone who is a clone of the current team.
  - Watch for: overweighting credentials. A dbt certification or BigQuery professional cert is a green flag, not a substitute for demonstrated production experience. Score based on what they show in the work sample, not what is on their resume.

---

## Red Flags & Green Flags

*Pre-defined signals specific to the MarketBridge Analytics Engineer role. These prevent post-hoc rationalization and keep the debrief focused on observable evidence.*

### Red Flags (Investigate Further or Proceed with Caution)

| Signal | Why It Matters | How to Probe |
|:---|:---|:---|
| Wants to rewrite everything from scratch | The dbt project is half-built, not worthless. A "burn it down" instinct wastes the existing work and signals low mess tolerance. We need someone who can triage and extend, not start over. | Ask: "You inherit a dbt project with 20 models, some broken. Walk me through your first week." If they say "delete it and start fresh" without investigating, that is a red flag. |
| Cannot explain a metric definition in business terms | Outcome #1 depends on translating business glossary entries into model logic. If they can only think in SQL, they will build technically correct models that do not match what stakeholders agreed to. | Give them a scenario: "Product counts active users as anyone who logged in. Growth counts active users as anyone who completed a booking. Finance counts active users as anyone who generated revenue. You need one definition. What do you do?" |
| Has never worked with a messy or inherited codebase | MarketBridge's data environment is partially broken, under-documented, and layered with decisions made by people who left. A candidate whose experience is entirely greenfield will struggle. | Ask: "Tell me about a time you inherited someone else's data infrastructure. What did you find? What did you do first?" If they have no answer, probe whether they can handle the MarketBridge environment honestly. |
| Dismissive of analyst team input | The 3 embedded analysts have institutional knowledge and are skeptical of new leadership. A candidate who signals "I am the engineer, they are just analysts" will poison the team dynamic. | Ask: "You join a team with three analysts who have their own SQL workflows and no shared standards. How do you introduce dbt without alienating them?" Listen for respect vs. condescension. |
| Focuses only on tooling, not outcomes | A candidate who spends the entire interview discussing tool preferences (Snowflake vs. BigQuery, Airflow vs. Dagster) without connecting to business outcomes will optimize the stack without delivering value. | Ask: "If you could only ship one thing in your first 90 days, what would it be and why?" If the answer is purely technical (e.g., "migrate to Snowflake"), probe for business justification. |
| No questions about stakeholders or team dynamics | This role requires navigating Raj's cost concerns, Diane's impatience, the senior analyst's Salesforce knowledge, and Anya's privacy requirements. A candidate who only asks about the tech stack is missing half the job. | Note whether the candidate asks about team structure, stakeholder expectations, or organizational dynamics during the interview. |

### Green Flags (Positive Signals to Seek Out)

| Signal | Why It Matters | How to Probe |
|:---|:---|:---|
| Asks "what does this metric mean to the business?" before writing SQL | Indicates Definition Rigor. This person will build models that match stakeholder intent, not just pass dbt tests. | Present the work sample with a deliberately ambiguous metric definition and observe whether they ask clarifying questions or assume. |
| Describes a phased approach to infrastructure cleanup | Shows they understand that you cannot fix everything at once and that sequencing matters. Directly relevant to the 90-day outcomes. | Ask: "You have a broken dbt project, a messy Segment setup, and a Mixpanel renewal in 6 weeks. How do you sequence the work?" |
| References documentation as part of the deliverable, not an afterthought | Outcome #2 is an inventory/documentation deliverable. A candidate who treats documentation as real work (not busywork) will succeed at this. | Ask: "How do you document a data model?" If they describe schema YAML, a README, and stakeholder-facing descriptions, that is a strong signal. |
| Has experience working with finance or operations data alongside product data | The MarketBridge gap between BigQuery (product) and NetSuite/Excel (finance) is a core challenge. A candidate who has bridged this gap before will ramp faster. | Ask: "Have you ever worked with financial data alongside product analytics? What was hard about it?" |
| Proactively mentions cost awareness in infrastructure decisions | Raj's top concern is cost rationalization. A candidate who naturally thinks about BigQuery compute costs, Fivetran sync frequency, and tool consolidation aligns with the CTO's priorities. | Ask: "Your data stack costs have doubled year-over-year. Where do you start investigating?" |
| Shows empathy for the analyst team's current situation | The analysts have been operating without leadership, doing ad-hoc ticket work, with declining morale. A candidate who recognizes this and wants to make their lives better will integrate faster than one who treats them as resources. | Ask: "The analyst team has been without a manager for months and is mostly doing ad-hoc requests. How does your work as an AE change their day-to-day?" |

---

## Dimension Weighting for Final Decision

*Not all dimensions are equally important for this specific role. Use these weights when scores are close and you need to break a tie.*

| Dimension | Weight | Rationale |
|:---|:---|:---|
| Technical Execution | 25% | Non-negotiable foundation. Without strong dbt/SQL skills, nothing else matters. |
| Definition Rigor | 25% | The core differentiator for this role vs. a generic AE hire. Outcome #1 depends entirely on this. |
| Mess Tolerance | 20% | The MarketBridge environment will break candidates who need clean starting points. Third most important because the environment is the environment. |
| Collaboration Signal | 15% | Must work with a skeptical analyst team and demanding stakeholders. A brilliant AE who alienates the team is a net negative. |
| Communication Clarity | 10% | Important but partially compensated by the Head of Analytics owning stakeholder communication. The AE needs to write good docs, not present to the board. |
| Intellectual Curiosity | 5% | Nice to have at this level. A mid-level AE who scores 3 on everything else but 2 on curiosity is still a strong hire. Curiosity becomes more important at the senior level. |

---

## Evaluation Criteria

Use these dimensions to self-assess your rubric. For official grading criteria, see `assessment/grading-rubrics.md` (Hiring Packet component, 20%).

| Criterion | What We Are Looking For |
|:---|:---|
| **Dimension Selection** | Are the scoring dimensions relevant to the role? Do they map to 90-day outcomes? Are there 4-6 dimensions (not too few, not too many)? |
| **Behavioral Anchors** | Are the 1-4 descriptions specific enough that two independent scorers would assign similar scores? |
| **Calibration Readiness** | Could a new interviewer use this rubric with minimal training? Is the norming section filled in thoughtfully? |
| **Red/Green Flags** | Are the flags specific, observable, and tied to job-relevant signals (not personal preferences)? |
| **Completeness** | Is the scorecard filled in with realistic content? Is the calibration section addressed? |

---

*Day 1 draft. To be refined for final portfolio submission by March 30. See `assessment/grading-rubrics.md` for evaluation criteria.*

*AI assistance: I used Claude (Opus 4.6) as an iterative thinking partner to develop, pressure-test, and refine the ideas, structure, and language in this document. All analytical judgments, prioritization decisions, and strategic reasoning are my own.*
