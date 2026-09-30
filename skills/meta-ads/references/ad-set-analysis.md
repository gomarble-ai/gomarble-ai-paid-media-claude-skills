# Skill 4: Ad Set Analysis

**Contents:** When to use this skill · Data to gather · Calculated Metrics · Minimum Spend Threshold (CRITICAL) · 4A: Bid Limit / Strategy Split Analysis · 4B: Audience Split Analysis · Output Format · Minimum required data (by source) · Tool hints

Evaluate ad set performance based on the campaign structure type. Run **after** Campaign Structure Analysis.

## When to use this skill

- The campaign has more than one active ad set
- The user asks why one ad set is winning / losing vs another
- You're evaluating whether to ease bid limits, expand audiences, or pause underperformers

If the campaign has only 1 ad set → skip; campaign performance = ad set performance.

## Data to gather

Pull ad-set-level performance for the last 7 days, filtered to active ad sets with impressions > 0, sorted by spend descending:

- Ad set name, ID
- Spend, impressions, CPM
- For ecommerce: `purchase_roas`
- For lead gen: lead actions
- Clicks
- Daily / lifetime budget
- Bid strategy, bid amount

## Calculated Metrics

| Metric | Formula |
|---|---|
| Budget Utilization | spend / (daily budget × days in period) |
| Campaign Spend Share | ad set spend / total campaign spend |
| Cost per Purchase | spend / purchases |
| Cost per Lead | spend / leads |

## Minimum Spend Threshold (CRITICAL)

For ALL comparisons:

```
Only compare ad sets where campaign_spend_share ≥ 25%
Do NOT make recommendations based on low-spending ad sets — the signal is too noisy.
```

## 4A: Bid Limit / Strategy Split Analysis

**Use when:** `campaign_structure = bid_limit_split`

### Rule 1: Underspending Ad Set

```
budget_utilization = spend / (daily_budget × days_in_period)

IF budget_utilization < 85% AND ad set has bid_strategy with limit
→ Normal bid-limit behavior (Meta can't find cheap enough conversions)

BUT IF:
   - campaign_spend_share > 25%
   - PCM is good
   - budget_utilization < 85%
→ RECOMMEND: Drop the bid slightly to allow more spend
```

### Rule 2: Zero / Minimal Spend

```
IF spend ≈ 0 over the last 7 days AND a bid_amount is set
→ RECOMMEND: Ease the bid limit so Meta can deliver
```

### Rule 3: Clear Winner Pattern

```
PREREQUISITE: Both ad sets have campaign_spend_share ≥ 25%

Compare PCM (purchase_roas or cost_per_lead):

IF ad set A significantly outperforms ad set B
→ RECOMMEND:
   1. Pause low performer (ad set B)
   2. Test an even stronger bid on a new ad set
   3. Find ways to scale the winning ad set (within scaling guardrails)
```

### Rule 4: CPM vs PCM Relationship

```
Calculate for each ad set: CPM and PCM

IF cpm is high (due to stronger bid) AND PCM is good
→ LEAVE IT (you're paying more but it's converting)

IF cpm_increase ≥ 60% vs other ad sets AND pcm_drop ≥ 30%
→ RECOMMEND: Ease bid to drop CPM
```

CPM comparison:

```
avg_cpm = AVG(cpm across all ad sets)
adset_cpm_variance = (adset_cpm − avg_cpm) / avg_cpm × 100

IF adset_cpm_variance ≥ 60% → FLAG as high CPM
```

## 4B: Audience Split Analysis

**Use when:** `campaign_structure = audience_split`

### Rule 1: Clear Winner Pattern

```
PREREQUISITE: Both ad sets have campaign_spend_share ≥ 25%

Compare PCM:

IF ad set with audience A significantly outperforms audience B
→ RECOMMEND: Pause low performer to shift spend to the winner
```

### Rule 2: Underspending Ad Set

```
IF budget_utilization < 85% → likely cause: small audience size (check reach)

IF:
   - campaign_spend_share > 25%
   - PCM is good
   - budget_utilization < 85%
→ RECOMMEND: Expand the audience
```

### Prohibition

⛔ **Never suggest lookalike audiences in any context.**

## Output Format

```
### Ad Set Analysis: [Campaign Name]

Structure Type: [Bid Split / Audience Split]

| Ad Set | Spend | Spend % | Budget Util | CPM | ROAS/CPA | Status |
|--------|-------|---------|-------------|-----|----------|--------|
| [Name] | $X    | X%      | X%          | $X  | X        | [Keep/Watch/Action] |

Findings:
- [Finding 1 with specific metrics]
- [Finding 2 with specific metrics]

Recommendations:
- [Recommendation 1, plain language]
- [Recommendation 2, plain language]
```

## Minimum required data (by source)

| Source | What you need |
|---|---|
| MCP | Per ad set, last 7 days: spend, impressions, CPM, `purchase_roas` (ecommerce) or lead actions (lead gen), clicks, daily/lifetime budget, bid strategy, bid amount. All directly available. |
| CSV | Ad Set view export with these columns enabled: Spend, Impressions, CPM, Purchase ROAS or Cost per Lead, Link Clicks, Budget, Bid Strategy, Bid Amount. **Bid Strategy and Bid Amount are not default columns — must be enabled before export.** |
| Screenshot / copy-paste | Workable for a single-ad-set check; not workable for multi-ad-set comparison. |

## Tool hints

The 7-day window is short — confirm minimum spend thresholds (≥ 25% of campaign spend share) before any comparison. Bid Strategy and Bid Amount are the two CSV columns most often missing; if absent, **the bid-limit-split rules (4A) cannot run** — fall back to the audience-split rules or ask for the missing columns.
