# Interview Loop Design

**Student Name:** Boga Petruska\
**Date:** 2026-04-02\
**Case Context:** [x] Medium (Series B)\
**Target Role:** Analytics Engineer\
**Target Level:** Mid (Senior offer if justified by performance)

---

## Interview Stages

### Stage Overview

| Stage | Interviewer | Focus Area | Duration | Format | Signal Being Tested |
|:---|:---|:---|:---|:---|:---|
| 1. HR Screen | HR (recruiting function) | Logistics, compensation alignment, basic qualifications | 20 min | Phone/Video | Comp expectations within range, availability within 4 weeks, baseline role fit. Filters out misaligned candidates before any hiring team time is spent. |
| 2. Work Sample | N/A (asynchronous) | Technical skill, definition rigor, data quality handling, communication | 3 hours (candidate time) | Take-home | Core job capability. Primary filter: most candidates select out here. See work-sample_boga.md. |
| 3. Hiring Manager Deep Dive | Head of Analytics (me) | Work sample review, role fit, 90-day priorities, definition rigor under pressure | 45 min | Video | Can they defend their work sample decisions? Will they thrive in the MarketBridge environment? |
| 4. Technical Scenario | Senior Embedded Analyst (presenting scenario designed by Head of Analytics) | Mess tolerance, live problem-solving, collaboration signal | 45 min | Video | How do they handle unstructured infrastructure problems? Do they treat the analyst as a peer? Head of Analytics reviews evaluation. |
| 5. Cross-Functional Interview | Senior PM (from Diane's product team) | Collaboration with end users, business sense, communication clarity | 30 min | Video | Do they understand the PM is a consumer of analytics, not a technical approver? Do they ask about business context before proposing solutions? |

**Why this loop, not more stages:**

MarketBridge is a Series B with 2 open headcount slots and a 6-week Mixpanel renewal deadline. A 6-stage loop with a skip-level and values interview is appropriate for a large enterprise, not for a company that needs an AE in seat within 4-6 weeks. The CTO (Raj) is the skip-level, but adding a separate stage for him extends the timeline by a week and tests signals (judgment, values) that the other stages already cover. Instead, Raj reviews all scorecards and joins the debrief with veto power. If he has specific concerns after reading the scores, he can request a 20-minute follow-up call before the offer goes out.

**Where candidates filter out:**

The HR screen is a lightweight logistics check. Most candidates who apply with relevant experience will pass it. The work sample is the real filter: it tests the four most important rubric dimensions simultaneously and requires 3 hours of focused effort. Candidates who lack production dbt experience, cannot handle messy data, or cannot communicate to non-technical stakeholders will be clearly visible in the work sample scores. This design means my time (Stage 3), the Senior Analyst's time (Stage 4), and the Senior PM's time (Stage 5) are only spent on candidates who have already demonstrated core competence.

**Total candidate time commitment:** 20 min screen + 3 hours work sample + 45 min review + 45 min manager + 30 min cross-functional = approximately 5.5 hours across 5 business days. This is respectful for a mid-level role.

---

## Stage Details

### Stage 1: HR Screen

HR handles the initial screen. At a ~150-person Series B, there is no dedicated recruiter, but someone in HR covers recruiting as part of their responsibilities. The hiring manager (me) provides HR with a one-page brief covering:

- Compensation range (60th-75th percentile for AE roles + equity)
- Required qualifications checklist (3+ years AE/DE experience, production dbt, strong SQL)
- Availability requirement (start within 4 weeks)
- A brief role summary to share with candidates

The goal is to filter on logistics and basic qualifications before any hiring team time is spent. HR confirms compensation alignment, availability, and that the candidate's background matches the required qualifications. HR also gives candidates a brief, honest preview of the role: "This is a new analytics engineering position on a four-person analytics team. The team currently has a Head of Analytics and three embedded analysts. You would be the first person in a dedicated AE role, building the data infrastructure that the analyst team relies on."

**Pass criteria:** Compensation aligned, available within timeline, meets required qualifications on paper. If all three, HR checks in with the Head of Analytics (quick Slack or email confirmation, not a meeting) before sending the work sample. This ensures the hiring manager has visibility into who is advancing and can flag any concerns from the resume before candidate time is spent on the exercise.

### Stage 2: Work Sample (Asynchronous)

See [work-sample_boga.md](work-sample_boga.md) for the full exercise, dataset description, and evaluation rubric.

The work sample is the most important stage. It tests four of six rubric dimensions (Technical Execution, Definition Rigor, Mess Tolerance via data quality handling, Communication via the stakeholder memo). Candidates who score below 3 on the work sample do not advance, regardless of interview performance.

**Logistics:**
- HR sends the work sample within 24 hours of passing the screen (after quick check-in with Head of Analytics).
- Candidate has 5 business days to submit.
- Head of Analytics scores the work sample before Stage 3. Senior Analyst scores independently before Stage 4.

### Stage 3: Hiring Manager Deep Dive (Head of Analytics)

I see the candidate first, before any other interviewer. This is deliberate. As a new Head of Analytics, I need to form my own assessment of every candidate before other voices enter the process. I review the work sample submission, conduct the interview, and decide whether the candidate advances to Stages 4 and 5.

**Structure:**
- 10 min: Work sample review. Candidate walks through their approach (not re-reading the memo, but explaining their decision process). I probe specific choices: "Why did you handle the duplicate payments this way?" "You proposed X as the unified definition. What would change if Christine pushed back?"
- 15 min: Live definition rigor exercise. Present a new scenario not in the work sample: "Growth says churn is any user who hasn't booked in 30 days. Product says churn is any user who deleted their account. Finance says churn is any user whose LTV stopped growing. You need one definition for the board deck due Friday. Walk me through how you'd handle this." Evaluate whether they ask clarifying questions, identify the business decision embedded in the definition choice, and propose a path to resolution.
- 10 min: Mess tolerance probe. "You join on Monday. By Wednesday, a Fivetran sync has broken, an analyst needs help with a Salesforce query, a PM is asking when her dashboard will be ready, and you haven't started the dbt audit yet. Walk me through your Wednesday." Evaluate whether they triage by impact, communicate proactively, or try to do everything simultaneously.
- 5 min: Honest conversation about the role. Discuss the maintenance burden (month 1 is 50/50 firefighting and building), the Mixpanel timeline, the analyst team's current state. Gauge reaction.
- 5 min: Candidate questions.

### Stage 4: Technical Scenario (Senior Embedded Analyst)

The Senior Analyst presents a live infrastructure scenario designed by the Head of Analytics. The Senior Analyst does not independently design the exercise or set the evaluation criteria. I define the scenario, the questions, and the scoring rubric dimensions to evaluate. The Senior Analyst runs the conversation and submits their scorecard, which I review alongside my own assessment.

**Why the Senior Analyst, with these guardrails:**

1. It tests whether the candidate treats the analyst as a peer. If the candidate talks down to the analyst or dismisses their questions, that is a Collaboration Signal red flag. This person will work alongside the analyst team daily.
2. The Senior Analyst has institutional knowledge of the messy infrastructure that I (as a new hire) do not yet fully have. Their read on whether the candidate's approach is realistic or naive is valuable input.
3. It gives the Senior Analyst a meaningful role in the hiring process, which builds buy-in for the new hire.
4. But: the Senior Analyst's evaluation is input to my decision, not a standalone gate. I am new and still building alignment with this team. I cannot delegate hiring judgment to someone whose calibration I haven't yet validated.

**Scenario (designed by Head of Analytics, presented by Senior Analyst):**

The Senior Analyst describes the current state of a real infrastructure problem (anonymized if needed): "We have a Salesforce-to-BigQuery pipeline that one analyst built and maintains. The joins are undocumented. Sometimes records appear duplicated after a sync, and we're not sure if it's a Fivetran issue or a Salesforce trigger issue. The pipeline breaks about once a month, and only one person knows how to fix it. You're the new AE. What's your first week look like with this problem?"

- 15 min: Candidate works through the problem with the analyst. Evaluate: Do they ask about the current state before proposing changes? Do they respect the existing work? Do they propose documentation and knowledge sharing, or do they propose replacing the pipeline?
- 15 min: Analyst asks follow-up questions from a prepared list. "What if the analyst who built it pushes back on changing anything?" "How would you document this so someone else can maintain it?" "What would you monitor to know if the pipeline broke?"
- 10 min: Candidate asks questions about the team, the infrastructure, daily work.
- 5 min: Buffer.

### Stage 5: Cross-Functional Interview (Senior PM)

A Senior PM from Diane's team evaluates whether this person can be a productive partner for the product team. The Senior PM is the right interviewer because they are the actual daily consumer of the AE's output (dashboards, metric definitions, self-serve analytics). Diane as VP of Product is too senior to spend 30 minutes interviewing a mid-level IC hire outside her own department; her time is better spent reviewing the debrief outcome and approving the hire if the Senior PM gives a positive signal.

**What this stage tests and does not test:**

The Senior PM is an end user of the analytics platform, not a technical evaluator. This stage tests whether the candidate can collaborate with someone who uses dashboards and metrics to make product decisions but does not know (and should not need to know) how dbt models, SQL joins, or pipeline monitoring work. The candidate should:
- Ask what decisions the PM makes with the data, not assume they know
- Explain technical trade-offs in business terms, not database terms
- Recognize that the PM's role is to define what they need to see, not to approve how it is built
- Understand that "the PM wants a dashboard" is a business requirement to be translated, not a technical specification to be implemented literally

A candidate who expects the PM to validate their data modeling choices or approve schema decisions is misunderstanding the relationship. A candidate who dismisses the PM's input because "they don't understand the data layer" is equally wrong.

**Structure:**
- 5 min: The Senior PM describes a real scenario. "I need a dashboard that shows me weekly conversion funnel by metro area. The last analyst built one in Mixpanel but the numbers don't match what I see in our SQL reports. I've stopped trusting it."
- 15 min: Candidate asks clarifying questions and proposes an approach. Evaluate: Do they ask what decisions the dashboard informs? Do they ask about the definition of "conversion"? Do they propose a timeline? Do they acknowledge the trust problem? Do they explain what they would need from the PM vs. what they would handle independently?
- 10 min: Open discussion about working together. How would they handle requests? What does "self-serve" mean in practice? What should the PM expect in the first 90 days vs. what they should not expect? How would the candidate communicate when something is delayed or when the data reveals a problem with how a metric has been defined?

---

## Debrief Protocol

### Before the Debrief

1. All interviewers submit scorecards independently within 24 hours of their interview, using the scorecard from rubric_boga.md.
2. No discussion of the candidate between interviewers before scorecards are submitted.
3. Head of Analytics collects all scorecards, reviews for patterns, and shares the anonymized score grid with all participants 1 hour before the debrief.
4. CTO (Raj) receives the score grid and work sample submission. He does not interview but reviews the materials and joins the debrief.

### During the Debrief (30 minutes)

| Step | Duration | What Happens |
|:---|:---|:---|
| 1. Score Share | 5 min | Head of Analytics displays all scores (anonymized initially). Team sees the pattern before hearing opinions. |
| 2. Round Robin | 15 min | Each interviewer shares their recommendation and top 2 observations. Start with the Senior Analyst (most junior in the room) to prevent anchoring by the hiring manager or CTO. No interruptions. |
| 3. Discussion | 5 min | Focus on areas of disagreement. Where did interviewers see different things? Common disagreement area: Definition Rigor scores between the CTO (who weights cost/architecture) and the PM (who weights daily usability). |
| 4. Decision | 5 min | Head of Analytics states the decision and reasoning. This is not a vote. Raj has veto power but must articulate the specific dimension and evidence driving the veto. |

### Decision Options

- **Strong Hire:** Move to offer immediately. At least one "strong hire" recommendation and no "strong no hire." Meets the minimum threshold (avg 3.0+, no dimension below 2, Technical Execution and Definition Rigor both at 3+).
- **Hire:** Move to offer. Majority positive, concerns are addressable with onboarding or coaching. Meets minimum threshold.
- **No Hire:** Reject with specific, respectful feedback. Concerns outweigh strengths for this role at this time.
- **Strong No Hire:** Reject. Fundamental mismatch on a critical dimension.

---

## Candidate Communication Plan

| Trigger | Action | Owner | Channel | Timeline |
|:---|:---|:---|:---|:---|
| Application received | Acknowledgment with expected timeline | HR | Email | Within 48 hours |
| After screen (pass) | Work sample sent with instructions, timeline, and contact for questions | HR (using materials from Head of Analytics) | Email | Within 24 hours of screen |
| After screen (no pass) | Rejection with brief reason | HR | Email | Within 3 business days |
| Work sample received | Confirmation of receipt | HR | Email | Within 24 hours |
| Interview days scheduled | Calendar invites with: who they will meet, what to expect in each stage, no trick questions | HR | Email + Calendar | 3+ business days before interviews |
| After final interview | Status update, even if "still in debrief" | Head of Analytics | Email | Within 48 hours |
| Offer | Verbal offer call (Head of Analytics), followed by written offer | Head of Analytics + HR | Phone + Email | Within 3 business days of debrief |
| Rejection (after interviews) | Personalized email with specific, actionable feedback | Head of Analytics | Email | Within 3 business days of debrief |

**Rejection after work sample:**

> Hi [Name],
>
> Thank you for completing the work sample exercise for the Analytics Engineer role at MarketBridge. We appreciate the time you invested.
>
> After review, we decided to move forward with candidates whose experience more closely aligns with [specific area, e.g., "reconciling conflicting metric definitions across teams" or "working with inherited, partially documented data infrastructure"]. Your [specific strength, e.g., "SQL was clean and well-structured"] stood out to our team.
>
> We would welcome the opportunity to consider you for future roles.

**Rejection after interviews:**

> Hi [Name],
>
> Thank you for interviewing with our team for the Analytics Engineer position. We enjoyed the conversation about [specific topic from their interview].
>
> After deliberation, we decided to move forward with another candidate. The decision was close, and we particularly valued your [specific strength]. Ultimately, we prioritized [specific factor, e.g., "hands-on experience navigating metric definition conflicts in a cross-functional environment"].
>
> We would be glad to stay in touch.

**Note on ownership:** HR owns logistics and early-stage communication (screen through scheduling). The Head of Analytics takes over for post-interview communication (status updates, offers, personalized rejections). This split keeps the hiring manager focused on evaluation while ensuring candidates get timely responses. Target: no candidate waits more than 3 business days without hearing from us at any stage.

---

## Decision Framework

### Decision Authority

- **Final decision maker:** Head of Analytics (hiring manager)
- **Veto power:** CTO (Raj), as skip-level. Must articulate the specific rubric dimension and evidence. "I just don't think they're strong enough" is not a valid veto.
- **Escalation:** If the hiring manager and CTO disagree after discussing evidence, the hiring manager's decision stands. Raj hired the Head of Analytics to build the team; overriding hiring decisions undermines that delegation. If Raj feels strongly, the conversation is about whether the Head of Analytics is calibrated correctly, not about this specific candidate.

### Handling Split Decisions

| Scenario | Action |
|:---|:---|
| All interviewers agree (hire or no-hire) | Proceed with consensus. |
| Majority hire, one dissent | Head of Analytics evaluates the dissent. If the concern is on Technical Execution or Definition Rigor (non-negotiable dimensions), investigate further. If on Intellectual Curiosity or Collaboration Signal, proceed with hire and note the gap for onboarding. |
| Majority no-hire, one strong advocate | Default to no-hire. One enthusiastic voice does not overcome multiple concerns. |
| Even split | Head of Analytics makes the call based on role priorities. Document reasoning. Consider a brief follow-up conversation on the contested dimension. |
| Concern about a coachable skill (e.g., Communication Clarity) | Hire with a 30-day development focus. Document the gap and the plan. |
| Concern about judgment, integrity, or Definition Rigor | Do not hire. These are not coachable in the short term, and Definition Rigor is non-negotiable for this role. |

### Reference Checks

Conduct after the interview loop, before the offer.

- Ask: "What does this person need from their manager to be successful?"
- Ask: "They will inherit a half-built dbt project and need to reconcile conflicting metric definitions across Product, Growth, and Finance. Does that sound like a situation where they would thrive?"
- Ask: "If you were hiring for this specific role, would you hire them? Why or why not?"
- Use references to confirm signals from interviews, not to generate new ones. If references contradict a strong interview signal, investigate.

---

# Internal Use Only

---

## Weaknesses and Risks of This Hire

*Moved from job description. Based on patterns observed at mid-level AE hires in Series B companies of similar size and growth stage. Share with interview panel before the debrief, not with candidates.*

### 1. Infrastructure tunnel vision: builds clean models nobody uses.
A mid-level AE's instinct is to build beautiful dbt models with perfect testing coverage. The risk is that they spend 90 days refactoring the staging layer while PMs still can't get a dashboard they trust. Outcome #3 (the PM-facing dashboard) is designed to counteract this, but you need to actively manage the balance. If week 6 check-ins show lots of model progress but no dashboard in sight, intervene.

**Mitigation:** The 90-day outcomes deliberately front-load the Mixpanel audit (day 30) and interleave the dashboard delivery with the dbt buildout. Hold weekly 1:1s that explicitly track both infrastructure work and stakeholder-facing deliverables.

### 2. Avoids the political work of metric definition alignment.
The hardest part of outcome #1 is not writing the dbt model. It is sitting in a room where Christine says "completed transaction" means payment received and Diane says it means booking confirmed, and translating that disagreement into a model that both trust. A mid-level AE will often defer to whoever spoke last, or build both definitions as separate models and let someone else decide. That defeats the purpose.

**Mitigation:** The JD explicitly calls out "push back when a definition is ambiguous or contradictory" as a required qualification. The work sample tests this directly: candidates must reconcile three conflicting definitions and propose a unified one. The hiring manager deep dive (Stage 4) tests it live with a new scenario.

### 3. Underestimates the Salesforce complexity and the relationship with Sales Ops.
The Salesforce-to-BigQuery data integration is the messiest part of the stack, and the senior analyst who understands it may not be eager to hand over that knowledge (it is their job security). A mid-level AE who has only worked with clean, well-documented source systems will struggle with the Salesforce data model and may deprioritize it in favor of more tractable problems.

**Mitigation:** Outcome #2 explicitly includes Salesforce pipeline documentation. In onboarding, pair the AE with the senior analyst for structured knowledge transfer sessions. Monitor the relationship: if the senior analyst feels threatened rather than supported, the knowledge transfer will stall. Stage 4 (Senior Analyst presents the Salesforce infrastructure scenario) is designed to surface this dynamic early.

### 4. Scope creep toward data engineering.
At a Series B with no dedicated data engineering team, the boundary between analytics engineering and data engineering is blurry. The AE will be pulled toward infrastructure work: Fivetran connector configuration, BigQuery cost optimization, Segment event schema management.

**Mitigation:** Define the boundary explicitly in onboarding: "You own the transformation layer and monitoring. Engineering owns the infrastructure layer. You file tickets for infra changes; you don't make them yourself." The bi-weekly Engineering sync is the handoff point.

### 5. Retention risk after 12-18 months.
A mid-level AE who successfully cleans up MarketBridge's data infrastructure will have a strong resume update and increased market value. At a Series B, you cannot compete on compensation with larger companies once this person has "built the data platform at a Series B marketplace" on their LinkedIn.

**Mitigation:** Equity vesting schedule that rewards staying through the growth phase, a clear career path (mid to senior AE, or into a lead/management role as the team grows), and genuine ownership of the platform. The strongest retention lever is that this person gets to own something meaningful, not be a cog.

### 6. May not adapt well to the "keep the lights on" parallel track.
The JD is framed around building new things. But the reality of the first 90 days includes keeping existing, broken things running: answering why Mixpanel and SQL disagree, fixing Fivetran syncs, helping analysts with ad-hoc queries.

**Mitigation:** Be honest in the interview about the maintenance burden (Stage 4, mess tolerance probe). Frame it as: "Month 1 is 50/50 firefighting and building. Month 2 is 30/70. Month 3 should be 10/90." If a candidate cannot tolerate the early maintenance phase, they are not the right fit regardless of technical skill.

---

## Evaluation Criteria

Use these dimensions to self-assess your interview loop design. For official grading criteria, see `assessment/grading-rubrics.md` (Hiring Packet component, 20%).

| Criterion | What We Are Looking For |
|:---|:---|
| **Stage Design** | Does each stage have a clear, distinct purpose? Is there redundancy? Is the total process respectful of candidate time? |
| **Signal Coverage** | Across all stages, are you evaluating technical skill, communication, collaboration, judgment, and culture add? No gaps? |
| **Debrief Rigor** | Is the debrief protocol designed to prevent anchoring and groupthink? Are scores collected independently? |
| **Candidate Communication** | Is the communication plan specific and timely? Would a candidate feel respected throughout the process? |
| **Decision Framework** | Is it clear how decisions are made, especially in ambiguous cases? Is the hiring manager empowered to decide? |

---

*AI assistance: I used Claude (Opus 4.6) as an iterative thinking partner to develop, pressure-test, and refine the ideas, structure, and language in this document. All analytical judgments, prioritization decisions, and strategic reasoning are my own.*
