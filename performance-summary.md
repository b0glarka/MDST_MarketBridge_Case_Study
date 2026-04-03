# Calibration-Ready Performance Summary

| Field | Details |
|-------|---------|
| **Student Name** | Boga Petruska |
| **Date** | 2026-03-23 |
| **Case Context** | Medium (Series B) -- MarketBridge |
| **Subject** | Kevin — L4 Staff Data Scientist |
| **Review Period** | H2 2025 |

---

## Role Context

- **Role Title:** Staff Data Scientist
- **Level:** L4
- **Team / Function:** Experimentation Platform
- **Scope:** Technical lead for the experimentation platform team; responsible for experiment methodology, infrastructure, and cross-functional instrumentation partnerships.
- **Key Expectations at This Level:** An L4 sets technical direction for the team, drives cross-functional initiatives to completion on time, delivers impact at L5 scope, and elevates the L3s around them. "Meets expectations" at L4 means the team is measurably better because this person is on it, not just that their individual output is strong.

---

## Key Accomplishments

| # | Accomplishment | Business Impact |
|---|---------------|-----------------|
| 1 | Designed and rolled out a Bayesian experimentation framework replacing the previous frequentist approach | Reduced average experiment duration by 30%, unblocking faster product iteration cycles across all teams that run experiments |
| 2 | Partnered with Engineering to instrument 15 new product events, filling critical gaps in the event taxonomy | Unblocked 3 product teams that had been waiting for tracking data to run experiments and measure feature adoption |
| 3 | Presented the experimentation framework at a regional data science meetup | Two candidates cited the talk as a reason they applied, contributing to recruiting pipeline |

---

## Growth & Development

- **New skills or capabilities developed:** Early adopter of AI coding assistants; output volume roughly doubled since adoption.
- **Increased scope or responsibility:** Took ownership of the experimentation methodology across the org, moving from team-level to company-level technical influence.
- **Behavioral growth:** Limited. Team dynamics feedback from L3s has not improved during the review period. Documentation practices remain below team expectations despite repeated requests.
- **Comparison to last review period:** Technical output is stronger. Team collaboration and delivery reliability have declined.

---

## Development Areas

| # | Development Area | Specific Recommendation |
|---|-----------------|------------------------|
| 1 | Team elevation: distributing growth opportunities to L3s instead of hoarding high-visibility work (see SBI below) | Identify one meaningful sub-project within the next initiative and delegate it to an L3 with mentorship, not just task assignment. Manager reviews the delegation plan in weekly 1:1. Success measure: the L3 presents the work to stakeholders, not Kevin. |
| 2 | Delivery discipline: managing scope commitments rather than expanding them unilaterally | For the next project, agree on scope and timeline upfront in writing. Any proposed additions require re-negotiating the deadline with the manager before starting. Track planned vs. actual scope in weekly 1:1s. |
| 3 | AI-assisted code quality and reviewability: ensuring AI-generated code meets team standards and is reviewed with the same rigor as hand-written code | Adopt the team's existing style conventions in all AI-assisted output. Submit all AI-assisted code through standard PR review. Pair with one L3 on the next AI-assisted analysis to calibrate on reviewability standards together. |

**SBI evidence for Development Area #1:**

**Situation:** During the H2 experimentation framework project, which involved both framework design (high-visibility) and data pipeline cleanup and event validation (lower-visibility but necessary).

**Behavior:** Kevin retained the framework design and methodology work for himself and assigned the data pipeline cleanup and event validation tasks to the two L3 data scientists on the team. This was not a one-time delegation decision but a sustained pattern across the full project duration.

**Impact:** Both L3s independently reported feeling like "Kevin's data cleaning crew." One described the dynamic in those exact words. Neither L3 had the opportunity to develop experimentation methodology skills, which is a key growth area for L3-to-L4 progression. The pattern creates a retention risk: L3s who feel they are only given grunt work while their senior colleague takes the interesting problems will leave. It also concentrates experimentation knowledge in one person, creating a bus factor of 1 on the team's most strategically important capability. At L4, the expectation is that the team is better because Kevin is on it. By this measure, the team's experience was worse.

**Development recommendation:** Identify one meaningful sub-project within the next initiative and delegate it to an L3 with mentorship, not just task assignment. Co-scope the work with the L3 upfront, check in on approach (not just output) weekly, and have the L3 present the work to stakeholders. Success measure: by end of Q1, one L3 can describe a project they owned end-to-end under Kevin's guidance, and Kevin can articulate what that L3 learned.

**SBI evidence for Development Area #2:**

**Situation:** During the H2 experimentation framework project, which had a committed delivery date agreed with the manager and Engineering stakeholders.

**Behavior:** Kevin expanded scope three times without re-negotiating the timeline. He added sequential testing, then an additional reporting module, then a Bayesian power calculator. When his manager flagged the first expansion, Kevin agreed to hold scope but added another feature the following week. He attributed the resulting 6-week delay to "scope changes from Engineering," but the manager's log shows all three expansions were self-initiated.

**Impact:** The framework launched 6 weeks late. Engineering had staffed integration work based on the original timeline and had to re-plan. Two product teams that were waiting for the framework to run experiments were blocked for an additional 6 weeks. At L4, delivering on commitments and managing scope are core expectations, not stretch goals. The pattern of agreeing to hold scope and then expanding anyway also erodes trust with the manager.

**Development recommendation:** For the next project, write scope and timeline in a shared document before starting. Any proposed addition requires a conversation with the manager before work begins, including a proposed trade-off (what gets cut or delayed to make room). Track planned vs. actual scope in weekly 1:1s. Success measure: next project delivers within one week of the committed date with no unilateral scope additions.

**SBI evidence for Development Area #3:**

**Situation:** During routine code review of Kevin's experimentation framework contributions in Q4.

**Behavior:** Kevin submitted AI-assisted code that did not follow the team's established style conventions and was harder for L3 reviewers to parse. In one instance, an L3 reviewer found a subtle statistical error in AI-generated confidence interval calculations that Kevin had not caught before committing. When the L3 raised the reviewability concern, Kevin responded: "AI makes me faster and the quality is fine. People just need to adapt."

**Impact:** The statistical error, if undetected, would have produced incorrect confidence intervals in the experimentation dashboard used by product teams to make launch decisions. The L3 spent a full day diagnosing and fixing the issue. The "people just need to adapt" response shifted the quality burden onto junior team members and dismissed a legitimate concern about code standards. At L4, Kevin is expected to set the quality bar, not lower it. Higher personal velocity that creates review burden and quality risk for the team is not a net positive.

**Development recommendation:** All AI-assisted code goes through the standard PR review process with no exceptions. Before submitting, Kevin refactors AI output to match team style conventions. Pair with one L3 on the next AI-assisted analysis to agree on what "reviewable" looks like. Success measure: zero AI-related code quality issues flagged in review for two consecutive sprints, and L3 reviewers report that Kevin's PRs are no harder to review than before AI adoption.

---

## Rating Recommendation

**Your Recommendation:** Below Expectations

**Justification:** Kevin's technical output is impressive in isolation: the Bayesian experimentation framework is a genuine contribution that reduced experiment duration by 30%, and the cross-functional instrumentation work unblocked three product teams.

However, the L4 bar requires more than strong individual output. Three factors place Kevin below expectations at his level:

1. The experimentation framework launched 6 weeks late due to self-inflicted scope expansion, not external blockers. Delivery reliability is a core L4 expectation.
2. Two L3 team members independently reported feeling relegated to low-value work while Kevin retained all high-visibility tasks. An L4 who hoards growth opportunities is failing the level's team-elevation requirement.
3. Kevin's AI-assisted code introduced a statistical error caught by a peer and created reviewability friction for the team, while Kevin's response ("people just need to adapt") showed a lack of accountability for team-wide code quality.

Any one of these would be a coachable development area. Together, they form a pattern: Kevin is delivering strong L3-level IC work while not meeting L4 behavioral expectations around delivery, team development, and communication.

**Honest assessment of prior feedback:** Kevin will likely feel blindsided by a Below Expectations rating, and not entirely without reason. The manager raised scope concerns in the August 1:1 and Kevin acknowledged them, but the conversation focused on the specific feature addition, not on the broader pattern of unilateral scope expansion as an L4 behavioral gap. The L3 feedback about growth opportunity hoarding was shared with the manager but was not relayed to Kevin in explicit SBI terms during the review period. The AI code quality issue was discussed after the incident, but framed as a one-time correction rather than a development area. In short: the manager saw the pattern forming but did not name it clearly enough, early enough. Kevin received signals but not a direct message that his L4 standing was at risk. This is a management failure that must be owned in the review conversation. It does not change the rating, which is based on observed behaviors and impact. But it means the review conversation must acknowledge: "I should have been more direct with you sooner, and I will be going forward." The development plan starts now with full clarity, not retroactive blame for feedback Kevin did not fully receive.

---

## Supporting Evidence

| Date | Source | Note |
|------|--------|------|
| 2025-08-15 | Manager observation | Experimentation framework scope expanded for the third time. Kevin proposed adding sequential testing without re-negotiating the timeline. Discussed in 1:1; Kevin agreed to hold scope but added another feature the following week. |
| 2025-09-30 | Stakeholder feedback (Engineering Lead) | "The instrumentation partnership was smooth. Kevin was easy to work with and the event taxonomy is solid." Positive signal on cross-functional collaboration with Engineering. |
| 2025-10-20 | Direct report feedback (L3 #1) | "I've been doing data cleaning for the experimentation project for two months. I asked Kevin if I could take on the A/B test design for one experiment and he said he'd 'get to it faster himself.'" |
| 2025-11-05 | Direct report feedback (L3 #2) | Identified a statistical error in AI-generated code that Kevin had committed without thorough review. The error affected confidence interval calculations in the experimentation dashboard. Caught before reaching stakeholders, but required a full day of L3's time to diagnose and fix. |
| 2025-12-01 | Manager observation | Experimentation framework README remains 2 pages. Team has requested runbooks three times since launch. Kevin has not produced them. Framework knowledge is concentrated in Kevin, creating a single point of failure. |
