# Work Sample Exercise

**Student Name:** Boga Petruska\
**Date:** 2026-04-02\
**Case Context:** Medium (Series B) -- MarketBridge\
**Target Role:** Analytics Engineer\
**Target Level:** Mid (Senior offer if justified by performance)

---

## Exercise Description

Last quarter, MarketBridge's board received two transaction counts in the same meeting: 487,000 from Finance (NetSuite) and 523,000 from Product (Mixpanel). The 7.4% gap stalled the Atlanta market launch decision and contributed to the previous Head of Analytics leaving. You will receive a one-month data extract from one metro area that reproduces this problem. Your task is to compute the "completed transactions" metric under each stakeholder's definition, diagnose why the numbers differ, propose a single unified definition implemented as a dbt-style SQL model, and write a short memo explaining your recommendation to three non-technical stakeholders.

---

## Business Context

MarketBridge is a Series B marketplace processing approximately 500,000 transactions per month across 15 metro areas. The company connects service providers with consumers, taking a commission on each completed booking. Your first priority as Analytics Engineer is building a dbt semantic layer that produces one number for each core metric, agreed upon across Product, Growth, and Finance.

The VP of Product (Diane) defines a "completed transaction" as: any booking where the consumer confirmed and the provider accepted, regardless of whether payment has been processed.

The CFO (Christine) defines a "completed transaction" as: any booking where payment has been received and the refund window (72 hours) has closed without a refund request.

The Head of Growth (Marco) uses a third definition internally: any booking where the consumer confirmed, excluding transactions later flagged as fraudulent.

No one has formally agreed on which definition is correct. The previous analyst built dashboards using Diane's definition. The finance team reports to the board using Christine's definition. Marco's growth reports use his own version. All three call the metric "completed transactions."

---

## Dataset Description

The candidate will receive three CSV files representing a one-month extract (January 2026) for a single metro area (Chicago):

1. **bookings.csv** (approximately 12,000 rows): booking_id, consumer_id, provider_id, booking_created_at, booking_confirmed_at, provider_accepted_at, service_category, booking_amount_cents, metro_area

2. **payments.csv** (approximately 10,500 rows): payment_id, booking_id, payment_amount_cents, payment_status (succeeded, failed, refunded, pending), payment_processed_at, refund_requested_at

3. **flags.csv** (approximately 400 rows): flag_id, booking_id, flag_type (fraud_suspected, duplicate, test_account, cancelled_by_consumer, cancelled_by_provider), flagged_at, resolved_at, resolution (confirmed_fraud, false_positive, pending, null)

**Note:** Provide a synthetic dataset that is realistic enough to support multiple valid analytical approaches. The dataset should be constructible from the schema above using a script, or provided as static CSVs.

---

## Questions to Answer

1. **Descriptive:** How many "completed transactions" does Chicago have for January 2026 under each of the three stakeholder definitions (Diane's, Christine's, Marco's)? Show your work and state any assumptions you made about edge cases.

2. **Diagnostic:** What explains the gap between the three numbers? Decompose the difference into specific categories (e.g., payments not yet processed, refunds, fraud flags, missing provider acceptance data). Which data quality issues did you encounter, and how did you handle them?

3. **Analytical:** Propose a single unified definition of "completed transaction" that could serve as the company's official metric. Write the SQL (or dbt-style SQL model) that implements it. Explain why your definition is better than picking any single stakeholder's version, and what trade-offs it introduces.

4. **Strategic:** Write a one-page memo (addressed to Diane, Christine, and Marco) that explains the current state of the metric, your proposed unified definition, and what changes in their respective reports. Include a concrete proposal for how you would get all three stakeholders aligned on the unified definition (meeting format, decision process, what each person would need to approve). The memo should be understandable by someone who does not write SQL.

5. **Process design:** You now need to build dbt models for four more metrics: active_user, churn_rate, CAC, and provider_utilization. Based on your experience with the completed_transaction exercise, what process would you recommend for defining and validating these metrics across teams? What would you do differently from how it was done before?

---

## Time Limit and Submission Format

- **Time limit:** 3 hours. We do not expect you to spend more than this, and we mean it. We would rather see a thorough, well-reasoned response to Questions 1-4 than a rushed attempt at all 5.
- **Submission format:** (1) A written memo for Question 4 (1 page, PDF or Markdown), (2) a SQL file or dbt model file implementing your unified definition from Question 3, and (3) a supporting analysis file (notebook, spreadsheet, or annotated SQL) covering Questions 1-2 with your work shown.
- **Due:** 5 business days after receiving the exercise.
- **Questions:** Candidates may email the Head of Analytics with clarifying questions. Responses within 24 hours.

**Important:** We value clear thinking over exhaustive analysis. If you discover data quality issues, document them and explain how they affect your numbers. Do not silently drop rows. Show your reasoning, not just your answer.

---

---

# Internal Use Only (not shared with candidate)

---

## Evaluator Notes

- Question 5 is a differentiator between Proficient (3) and Expert (4) candidates. A strong Q1-Q4 submission with no Q5 is a fully viable hire. Q5 distinguishes candidates who think about process, not just output.
- The dataset contains 5 intentional data quality issues (listed below). Track how many each candidate identifies without prompting. Identifying 3+ is Proficient; identifying all 5 with documented handling is Expert.
- The timezone mismatch (bookings in America/Chicago, payments in UTC) is the hardest to catch because it is not flagged anywhere in the candidate-facing materials. Catching it unprompted is a strong signal for Mess Tolerance.

## Known Data Issues (seeded in dataset, not disclosed to candidate)

1. Approximately 3% of bookings have a booking_confirmed_at timestamp but no corresponding provider_accepted_at (provider acceptance was not tracked consistently before a Segment instrumentation fix in November 2025). These are real bookings that were completed.
2. Approximately 150 bookings have duplicate entries in payments.csv (same booking_id, same amount, same timestamp) due to a webhook retry bug in the Stripe integration. These are not double payments.
3. 47 rows in bookings.csv have booking_amount_cents = 0. Of these, 38 are promotional bookings (legitimate) and 9 are test accounts. Test accounts can be identified by consumer_id starting with "test_".
4. Timestamps in payments.csv are in UTC. Timestamps in bookings.csv are in America/Chicago local time. This is not documented anywhere.
5. 12 bookings have a refund_requested_at timestamp that falls before payment_processed_at (a known Stripe sandbox artifact carried into production during the migration). These are real refunds that should be treated as valid.

## Evaluation Rubric for This Exercise

| Dimension | 1 -- Novice | 2 -- Developing | 3 -- Proficient | 4 -- Expert |
|:---|:---|:---|:---|:---|
| **Problem Framing** | Picks one stakeholder's definition and implements it without acknowledging the others. Does not question the data. | Acknowledges that definitions differ but does not systematically compare them. May implement all three but not explain the gaps. | Implements all three definitions, decomposes the gap, and proposes a unified definition with clear rationale. States assumptions for edge cases. | Reframes the problem: identifies that the real issue is not which definition is "right" but that the company lacks a definition governance process. Proposes both a metric and a process. |
| **Data Quality Handling** | Ignores data issues. Reports numbers that include duplicates, test accounts, or timezone errors without noticing. | Notices some issues (e.g., zero-amount bookings) but misses others (e.g., timezone mismatch, duplicate payments). Handles issues ad hoc without documenting decisions. | Identifies and documents the major data quality issues (duplicates, timezone, missing provider acceptance, test accounts). Explains impact on each definition's count. Handles issues consistently. | Proactively builds data quality checks into the SQL model (e.g., deduplication logic, test account filter, timezone normalization). Documents issues as if creating an audit trail for a future analyst. |
| **Analytical Rigor** | SQL contains errors (wrong joins, incorrect aggregation, missing filters). Numbers do not add up across definitions. | SQL is correct but only for the simplest definition. Does not handle edge cases (refunds before payments, null provider_accepted_at). | SQL correctly implements all three definitions and handles edge cases. Unified definition SQL is clean, tested against known edge cases, and produces a number the candidate can defend. | SQL is production-ready: uses CTEs or staging patterns consistent with dbt conventions, includes comments explaining business logic, handles all known edge cases, and could be dropped into a dbt project with minimal modification. |
| **Communication** | Memo is technical: includes SQL snippets, refers to column names, assumes the reader knows what a LEFT JOIN is. | Memo is understandable but buries the recommendation. Spends most of the space explaining what was done rather than what the reader should do. | Memo leads with the recommendation (BLUF). Explains what changes for each stakeholder. Acknowledges trade-offs. A VP could read it and know what to decide. | Memo is concise, specific, and anticipates objections. Pre-addresses "but my old number was higher" concerns. Includes a clear next step and timeline. Could be sent as-is to the three stakeholders. |
| **Judgment** | No recommendation, or recommends one stakeholder's definition without justification. | Recommends a definition but does not address trade-offs or what each stakeholder loses. | Clear recommendation with rationale, trade-offs acknowledged, and a path for stakeholders to agree. Recognizes that the metric definition is a business decision, not a technical one. | Distinguishes between "the metric we report to the board" and "the metric each team uses for operational decisions." Proposes a hierarchy (one official metric, with team-specific views that reconcile to it). |

---

## Evaluation Criteria

Use these dimensions to self-assess your work sample exercise. For official grading criteria, see `assessment/grading-rubrics.md` (Hiring Packet component, 20%).

| Criterion | What We Are Looking For |
|:---|:---|
| **Realism** | Does the exercise reflect tasks the candidate would actually perform in the role? Is the business context believable? |
| **Respect for Time** | Is the exercise completable in 3 hours? Are expectations about scope clearly communicated? |
| **Escalating Difficulty** | Do the questions move from descriptive to diagnostic to strategic? Can you distinguish strong from weak candidates? |
| **Rubric Alignment** | Does the evaluation rubric cover the dimensions that matter? Could a different evaluator use it and reach similar conclusions? |
| **Case Context Fit** | Is the exercise tailored to MarketBridge, not generic? |

---

*AI assistance: I used Claude (Opus 4.6) as an iterative thinking partner to develop, pressure-test, and refine the ideas, structure, and language in this document. All analytical judgments, prioritization decisions, and strategic reasoning are my own.*
