# Skill 1: Search Campaign Optimization

**Contents:** When to use this skill · Data to gather · Step 1: Classify Each Search Term (Q1 – Q5) · Step 2: Classify Auction Pressure · Step 3: Decision Matrix · Step 4: CPC Inflation Diagnosis · Step 5: Scaling Prerequisites · Step 6: Brand & Competitor Logic · Recommendations to Make · Weekly Execution Order (immutable) · Prohibitions · Output Format · Minimum required data (by source) · Tool hints

A systematic approach to Google Ads Search via query classification, auction-pressure diagnosis, and rule-based decision logic.

**Workflow:** Data → Classification → Pressure Analysis → Decision → Action.

## When to use this skill

- Audit or optimize a Search campaign
- Diagnose why CPA / ROAS / impression share is changing
- Decide whether to scale, hold, or cut a Search campaign
- Identify wasted spend in search terms

## Data to gather

Ask the user to share — or pull from whatever data source is available — the following for the relevant Search campaigns over the **last 30 days**, filtered to ENABLED campaigns only.

**Campaign-level auction metrics:**

- Search impression share
- IS Lost (Rank)
- IS Lost (Budget)
- Top of Page Rate
- Absolute Top of Page Rate
- Average CPC
- Cost, conversions, conversion value, clicks, impressions

**Search-term report:** Each search term with impressions, clicks, cost, conversions, conversion value, sorted by cost descending (top 200 by spend).

**Keyword-level data:** Keyword text, match type, keyword impression share, IS Lost (Rank), avg CPC, conversions, cost.

**CPC trend:** Average CPC for the last 7 days AND the prior 7 days, so WoW change can be calculated.

**User inputs to request (if not already known):**

- Target CPA (or target ROAS for ecommerce). Default: historical 30-day average.
- Brand name (so brand vs non-brand terms can be classified)
- Competitor names (optional)
- Priority geographies (optional)

## Step 1: Classify Each Search Term (Q1 – Q5)

| Tier | Name | Condition |
|---|---|---|
| **Q1** | Profitable | Conversions ≥ 2, OR CPA ≤ target, OR ROAS ≥ target |
| **Q2** | Promising | Conversions = 0 AND cost < 0.5× target CPA AND no Q5 signals |
| **Q3** | Unproven | Conversions = 0 AND cost between 0.5×–1× target CPA |
| **Q4** | Losing | Cost ≥ 1× target CPA with 0 conversions, OR CPA ≥ 1.5× target, OR ROAS ≤ 0.7× target |
| **Q5** | Invalid | Query contains: free, cheap, diy, how to, job, salary, course, pdf, meaning, used, repair |

**Q5 terms are eliminated regardless of cost.** Calculate spend share per tier.

**Intent signal patterns** (for classifying Q1 vs Q5 when ambiguous):

- **High intent (→ Q1):** buy, purchase, order, pricing, price, cost, near me, delivery, shipping, discount, coupon, subscribe, sign up, get started, demo, trial, quote, consultation, book, schedule
- **Mid intent (→ Q2 / Q3):** best, top, review, vs, versus, compare, alternative, recommendation, worth it
- **Low intent (→ Q4 / Q5):** what is, how to, tutorial, guide, learn, definition, meaning, example
- **Negative intent (→ Q5):** free, diy, repair, fix, used, second hand, jobs, career, salary, template, sample

## Step 2: Classify Auction Pressure

### Rank Pressure

| Rank Pressure = HIGH if **any** true |
|---|
| IS Lost (Rank) ≥ 30% |
| Search IS ≤ 50% AND IS Lost (Rank) > IS Lost (Budget) |
| Top of Page Rate ≤ 60% on Q1 queries |
| Absolute Top ≤ 20% on Q1 queries |

| Rank Pressure = LOW if **all** true |
|---|
| IS Lost (Rank) ≤ 20% |
| Top of Page Rate ≥ 70% |
| Absolute Top ≥ 30% on Q1 queries |

### Budget Pressure

| Budget Pressure = HIGH if **all** true |
|---|
| IS Lost (Budget) ≥ 20% |
| IS Lost (Budget) > IS Lost (Rank) |
| CPA ≤ target CPA |
| ≥ 60% of spend from Q1–Q3 |

| Budget Pressure = LOW if **any** true |
|---|
| IS Lost (Budget) < 10% |
| CPA > target CPA |
| Q4 + Q5 spend ≥ 25% |

## Step 3: Decision Matrix

| Query Mix | Rank Pressure | Budget Pressure | Action |
|---|---|---|---|
| Q1-heavy | Low | High | Increase budget 10–20% |
| Q1-heavy | High | Low | Increase bids 5–10% OR improve ad relevance |
| Q1-heavy | High | High | Fix rank first, then budget |
| Q1-heavy | Low | Low | Hold — no changes needed |
| Q2–Q3 heavy | Low | High | Limited budget test |
| Q4+ present | High | Any | Cap or cut spend |
| Q5 present | Any | Any | Negate immediately |

**Search IS alone:** Low Search IS means nothing on its own. Only act when Q1 share ≥ 50% AND IS Lost (Rank or Budget) explains it.

**IS Lost (Rank) logic:**
- If majority Q1, CPA ≤ target, Rank Pressure HIGH → increase bids 5–10% **or** improve ad relevance.
- If CPA > target → do NOT raise bids. Instead tighten queries: promote Q1 to Exact, kill Q3/Q4 leakage.

**IS Lost (Budget) logic:**
- If CPA stable, Q1–Q3 share ≥ 60%, Budget Pressure HIGH → increase budget 10–20%.
- Otherwise fix queries first.

**Top / Absolute Top:**
- Use only on Q1 queries.
- If CVR at Top ≥ 1.15× rest → defend the position.
- No CVR delta = ego tax. Ignore.

## Step 4: CPC Inflation Diagnosis

When CPC is rising WoW:

| Symptom | Root Cause | Action |
|---|---|---|
| CPC ↑ AND IS Lost (Rank) ↑ | Competition increased | Bid increase allowed ONLY if CPA ≤ target |
| CPC ↑ AND new Q4/Q5 terms appearing | Match type leakage | Add negatives, tighten match types |
| CPC ↑ AND CTR ↓ | Ad relevance degraded | Improve ad copy, NOT bids |

**Only competition justifies bid increases.** Cases 2 and 3 require query or creative fixes.

## Step 5: Scaling Prerequisites

Scale ONLY if **all** true:

- Q1 queries isolated (Exact or tight Phrase match)
- CPA stable or improving over 14+ days
- IS Lost (Budget) ≥ 20%
- CPC WoW% increase < CVR WoW% increase (efficiency improving faster than costs)

If CPC rising faster than CVR → false scale signal. Do not increase budget.

## Step 6: Brand & Competitor Logic

**Brand defense** (when brand CPC ↑, Absolute Top ↓, competitor overlap ↑):

- Raise bids only on exact-match brand terms
- Tighten match types on brand campaigns
- Add competitor terms as negatives in non-brand campaigns

**Competitor campaigns:** Default state is OFF. Enable only if CPA ≤ 1.2× target AND Rank Pressure = LOW. Otherwise pause.

## Recommendations to Make

When the user is ready to act, recommend the change in plain terms. The recommendation itself is the deliverable — the user applies the change manually in the Google Ads UI. Examples:

- *"Increase the daily budget on Campaign X from $Y to $Y × 1.15 (15% increase). Hold here for 14 days and re-evaluate."*
- *"Raise the keyword-level max CPC on these 5 Q1 keywords by 5–10%. Keep the other keywords' bids unchanged."*
- *"Add the following terms to the campaign's negative keyword list: free, diy, how to, repair, [...]"*
- *"Create a new ad group containing the top 8 Q1 search terms as Exact-match keywords. Add those same terms as negatives in the original ad group to prevent overlap."*

## Weekly Execution Order (immutable)

1. Prune Q4/Q5 queries
2. Reclassify remaining queries
3. Recompute auction pressure
4. Make bid / budget moves
5. Fix ad relevance

## Prohibitions

- Never increase budget to fix low IS without classifying queries first
- Never increase bids with Q4/Q5 terms present
- Never chase Absolute Top without CVR proof
- Never let Broad match dominate auction signals
- Never increase bids AND budget simultaneously

## Output Format

```
### Current State
- Total spend: $X over 30 days
- Query distribution: Q1 (X%), Q2–Q3 (Y%), Q4–Q5 (Z%)
- CPA: $XX (Target: $XX) — [XX% over/under target]
- Rank Pressure: HIGH / LOW
  - IS Lost (Rank): X%
  - Top of Page Rate: X%
  - Absolute Top: X%
- Budget Pressure: HIGH / LOW
  - IS Lost (Budget): X%
  - CPA vs Target: [status]
  - Q1–Q3 spend: X%

### Query Classification Summary
- Q1 (X% of spend): top profitable terms
- Q2–Q3 (Y% of spend): top promising/unproven terms
- Q4–Q5 (Z% of spend): terms to negate; estimated savings $X/day

### CPC Inflation Analysis
- Current CPC: $X
- Prior period CPC: $X
- Change: X% WoW
- Diagnosis: [Case 1 / 2 / 3]
- Root cause: [...]

### Recommended Action (from decision matrix)
Execution order:
  1. ...
  2. ...
  3. ...

Tactical moves:
  - Bid/budget adjustments with entity references
  - Negatives to add (list)
  - Isolation recommendations

### Expected Outcomes (7-day horizon)
- CPA: $XX → $XX
- IS Lost (Rank): X% → X%
- IS Lost (Budget): X% → X%
- Q1 spend share: X% → X%
```

## Minimum required data (by source)

| Source | What you need |
|---|---|
| MCP | Last 30 days, filtered to ENABLED Search campaigns: (1) campaign-level metrics (cost, conversions, conv. value, clicks, impressions, search IS, IS Lost Rank/Budget, Top of Page Rate, Abs Top Rate, avg CPC) via the `campaign` resource; (2) search-term performance via `search_term_view` (top 200 by cost); (3) keyword-level via `keyword_view`; (4) CPC trend by segmenting last 7d vs prior 7d. |
| CSV | **Requires three separate exports** from the Google Ads UI: (1) Campaign Performance report with auction metrics columns enabled; (2) Search Terms report (top 200 by cost); (3) Keywords report. Plus a week-over-week breakdown if not in the campaign export. |
| Screenshot / copy-paste | Workable only for a quick sanity-check on one campaign. The Q1–Q5 classification needs the full search-term list. |

## Tool hints

The Q1–Q5 classification engine needs the **full search-term list, not just top performers**. With MCP, query `search_term_view` and paginate to 200 rows by cost desc. With CSV, the user must run a separate Search Terms export — not the Campaigns export. Auction metrics (Search IS, IS Lost Rank/Budget, Top of Page Rate, Abs Top Rate) are in the Campaigns export but require the auction columns to be enabled — many users miss this and share a CSV with only spend / conversions.
