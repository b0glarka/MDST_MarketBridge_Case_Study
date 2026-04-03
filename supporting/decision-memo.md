# Decision Memo

| Field | Your Entry |
|---|---|
| **Student Name** | Boga Petruska |
| **Date** | 2026-04-02 |
| **Case Context** | Medium (Series B) -- MarketBridge |
| **Decision Title** | Mixpanel contract renewal: renew, sunset, or migrate |
| **Decision Owner (A)** | Head of Analytics (me), with CTO (Raj) approval required |
| **Status** | Under Review |

---

## Context

MarketBridge's Mixpanel contract renews in approximately 6 weeks. The product team uses Mixpanel for event-based product analytics (funnels, retention, feature adoption). However, PMs have stopped trusting Mixpanel because its numbers conflict with SQL queries against the BigQuery warehouse. The root cause is not Mixpanel itself but the lack of a shared semantic layer: Mixpanel counts events using its own definitions, while analysts query BigQuery with different logic, and Finance reports from NetSuite with a third set of definitions. This is the same problem that produced the 487K vs. 523K transaction count gap at the board meeting.

The decision cannot wait. If the contract lapses without a plan, the product team loses its only self-serve analytics tool (broken as it is) with no replacement ready. If we auto-renew at full price, we lock in ~$84K/year (~$7K/month, our Growth plan tier at current event volume) for a tool the team does not trust, while simultaneously paying for the BigQuery + dbt infrastructure that is intended to replace it. The CTO has explicitly stated that net-new tooling requires a sunset plan for something else. Mixpanel is the largest single line item in our $25K/month tooling budget, representing roughly 28% of data stack spend.

Complicating factor: the Analytics Engineer who would build the dbt-based replacement has not been hired yet. Any option that depends on the AE must account for a 4-6 week hiring timeline plus onboarding.

---

## Options Considered

### Option A: Renew Mixpanel at full annual rate

| Dimension | Assessment |
|---|---|
| **Description** | Sign a standard 12-month renewal. Product team keeps using Mixpanel as-is. No disruption to current workflows. |
| **Pros** | Zero disruption. No migration risk. PMs retain a familiar tool. Buys time to build the dbt replacement without pressure. |
| **Cons** | Locks in ~$84K/year for a tool the team does not trust. At 28% of total data stack spend, this is not a rounding error. Removes urgency to build the replacement. Contradicts Raj's cost rationalization mandate. Sends the wrong signal: we are paying for two systems that do the same thing. |
| **Estimated Effort** | S (contract signature only) |
| **Dependencies** | CTO budget approval. |

### Option B: Let Mixpanel lapse, go warehouse-only immediately

| Dimension | Assessment |
|---|---|
| **Description** | Do not renew. Product team queries BigQuery directly (via analyst requests or a BI tool like Looker/Metabase) starting immediately. |
| **Pros** | Maximum cost savings. Forces the team to invest in the dbt + BI replacement. Clean break. |
| **Cons** | The dbt semantic layer does not exist yet. The AE is not hired. PMs would have zero self-serve analytics capability for 3-4 months (hiring + onboarding + build time). Diane's team would be entirely dependent on analyst ad-hoc requests during this gap, which is the exact problem we are trying to solve. This option trades a trust problem for an access problem. |
| **Estimated Effort** | S (do nothing), but the downstream cost is XL: analyst team absorbs all PM analytics requests for months. |
| **Dependencies** | Requires analyst team to absorb the entire PM analytics workload with no additional capacity. |

### Option C: Month-to-month renewal at reduced rate while building the replacement

| Dimension | Assessment |
|---|---|
| **Description** | Negotiate a month-to-month extension (or 3-month bridge contract) at a reduced rate. Use this window to hire the AE, build the dbt semantic layer for the top 10-15 metrics, and ship the first PM-facing dashboard on trusted data. Sunset Mixpanel once PMs have a replacement they trust. |
| **Pros** | Maintains PM self-serve access during the transition. Creates a clear sunset timeline tied to a deliverable (not a date). Demonstrates cost discipline to Raj (reduced rate, not full renewal). Estimated bridge cost: ~$15-21K total (3-4 months at ~$4-5K/month negotiated rate, down from ~$7K/month). Aligns with the roadmap: hire AE (month 1), build dbt models (months 2-3), ship PM dashboard (month 3-4), sunset Mixpanel (month 4-5). |
| **Cons** | Temporary cost overlap: paying for both Mixpanel (reduced) and the dbt + BI stack during the transition. Requires successful negotiation with Mixpanel on pricing. Depends on hiring the AE within the expected timeline; if hiring takes longer, the bridge extends and costs accumulate. |
| **Estimated Effort** | M (negotiation + migration planning, 2-3 weeks of Head of Analytics time; AE executes the build over months 2-4) |
| **Dependencies** | Mixpanel willing to negotiate month-to-month terms. AE hired within 4-6 weeks. dbt semantic layer delivered within 3 months of AE start. |

---

## Recommendation

I recommend Option C: month-to-month renewal at reduced rate while building the replacement.

The core argument is not about saving money on Mixpanel. It is about three things:

1. **Migration accountability.** A full renewal removes the urgency to build the dbt replacement. The team has been living with broken infrastructure for over a year; a 12-month renewal signals that another year of "Mixpanel and SQL give different answers" is acceptable. A bridge contract with a sunset trigger creates a deadline the AE and I are accountable to.

2. **No tool without a successor.** Raj's stated principle is that net-new tooling requires a sunset plan. The reverse should also hold: we should not renew a tool we plan to replace unless the renewal is explicitly structured as a bridge. Renewing Mixpanel at full price while building its replacement in dbt is paying for two systems that serve the same function, which is exactly the cost discipline problem Raj wants to fix.

3. **Protecting PM access during the transition.** Option B (let Mixpanel lapse) is the cheapest option but creates a 3-4 month gap where PMs have zero self-serve analytics. Diane's team would be entirely dependent on analyst ad-hoc requests during this gap, which is the problem we are trying to solve. Trading a trust problem for an access problem damages the most important stakeholder relationship we have.

The cost case supports the strategic case: a bridge contract (~$15-21K total over 3-4 months at a negotiated rate) is significantly cheaper than a full renewal (~$84K/year), and after sunset, we permanently eliminate the largest single line item in the data stack budget (28% of $25K/month). That savings offsets the AE comp increase Raj needs to approve.

The strongest argument against Option C is execution risk: if the AE hire is delayed or the dbt build takes longer than expected, the bridge extends and costs accumulate. The mitigation is that the sunset trigger is tied to a deliverable (5+ PM weekly active users on the replacement dashboard), not a date. If the replacement is not ready, we extend the bridge rather than either auto-renewing for 12 months or cutting PMs off.

**Sunset trigger:** Mixpanel is cancelled when the first PM-facing dashboard on dbt models has 5+ weekly active PM users (90-day outcome #3 from the AE job description). This ties the sunset to a deliverable, not an arbitrary date.

---

## Risks and Mitigations

| Risk | Likelihood (H/M/L) | Impact (H/M/L) | Mitigation |
|---|---|---|---|
| Mixpanel refuses month-to-month terms | L | M | SaaS vendors strongly prefer a reduced-rate bridge over losing the account entirely. MarketBridge is a growth-stage logo Mixpanel would want to retain. Fallback: negotiate a 3-month bridge contract (~$15-21K). If they refuse any flexibility, evaluate a 6-month contract at current rate (~$42K). Even the worst case is half the cost of a full renewal. |
| AE hiring takes longer than 4-6 weeks | M | H | If AE is not hired by week 8, extend the Mixpanel bridge. The sunset date is tied to a deliverable, not a calendar date, so the plan adapts. Begin dbt audit work internally (Head of Analytics + Senior Analyst) to reduce AE ramp time. |
| dbt replacement takes longer than 3 months after AE starts | M | M | Scope the first PM dashboard to the 5 most-requested metrics, not all 15. A focused dashboard on trusted data is better than a comprehensive one that slips. |
| PMs resist switching from Mixpanel to the new dashboard | L | H | Involve 2-3 PMs in the dashboard design process. Let them validate that the new tool answers the same questions Mixpanel does. Diane's sponsorship is the lever: if she adopts it, her PMs follow. |
| Raj rejects any cost overlap | L | H | Frame the overlap as a bridge, not an addition: "We spend ~$15-21K over 3-4 months while building the replacement. After sunset, we permanently eliminate ~$84K/year, the largest line item in the data stack. Net first-year savings even after the bridge cost." |

---

## Decision Type

**This is a Type 1 decision.**

The Mixpanel contract renewal is irreversible once signed (12-month commitment) or irreversible once lapsed (data access lost, PM workflows disrupted). Even the month-to-month option, while more reversible than Options A or B, commits us to a migration path that shapes the next 6 months of team priorities and the AE's first 90 days.

**Implications:**
- Requires CTO (Raj) approval, not just Head of Analytics decision.
- The Mixpanel technical audit (90-day outcome #4 from the AE JD) must be completed by the AE within 30 days of start to validate the sunset assumptions. If the audit reveals that Mixpanel provides capabilities that cannot be replicated via dbt + BI tool, the sunset timeline may need to extend.
- Decision deadline: 2 weeks before contract expiration to allow negotiation time.
- Revisit at the 90-day AE check-in: is the dbt replacement on track? If not, extend the bridge.

---

## Approval and Record

| Action | Person | Date | Notes |
|---|---|---|---|
| **Drafted by** | Head of Analytics (me) | Week 1 | Based on current-state audit and data infra decision brief |
| **Consulted** | CTO (Raj), VP of Product (Diane), CFO (Christine) | Week 2 | Raj for budget/cost. Diane for PM impact. Christine for financial reporting implications. |
| **Decided by** | CTO (Raj) with Head of Analytics recommendation | Week 3 | 2 weeks before contract expiration |
| **Communicated to** | Analytics team, PM team, Engineering | Week 3 | Announce the plan, sunset timeline, and what PMs should expect |
| **Review date** | 90 days after AE start | -- | Is the dbt replacement on track? Adjust sunset timeline if needed. |

---

*AI assistance: I used Claude (Opus 4.6) as an iterative thinking partner to develop, pressure-test, and refine the ideas, structure, and language in this document. All analytical judgments, prioritization decisions, and strategic reasoning are my own.*
