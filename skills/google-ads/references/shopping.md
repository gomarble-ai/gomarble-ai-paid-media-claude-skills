# Skill 2: Shopping Campaign Optimization

**Contents:** When to use this skill · Step 0: Feed Health (BLOCKING) · Data to gather · Step 1: Item-Level Classification · Step 2: Product Group Structure · Step 3: Search Term Negatives · Step 4: Budget & Bid Decisions · Step 5: Device & Location (last) · Step 6: Campaign Kill Conditions · Prohibitions · Output Format · Minimum required data (by source) · Tool hints

Product-led optimization: validate feed → classify items → manage structure → scale or cut.

## When to use this skill

- Audit or optimize Shopping / Performance Max for Retail campaigns
- Identify wasted spend at the SKU level
- Decide which products to promote, downgrade, or kill
- Diagnose why Shopping ROAS is below target

## Step 0: Feed Health (BLOCKING)

Before any optimization, verify:

- ≥ 80% of products approved in Merchant Center
- Purchase conversion tracking is active (conversion value > 0 in data)
- Prices and availability are accurate (requires Merchant Center check or manual verification)

**If any check fails → STOP all optimization. Fix the feed first.** Ask the user to confirm Merchant Center status before continuing.

## Data to gather

Lookback window: **14 days** if the account has ≥ 100 purchases/month, otherwise **30 days**.

Ask the user to share — or pull from whatever data source is available:

**Account-level AOV:** total conversion value ÷ total conversions over the lookback window.

**Item-level performance:** Per product: product ID, product title, brand, cost, conversions, conversion value, clicks, impressions. Sort by cost descending (top 200).

**Campaign-level:** Campaign ID, name, status, daily budget, cost, conversions, conversion value, filtered to Shopping campaigns and ENABLED status.

**Search terms:** Search term, cost, clicks, conversions for the Shopping campaigns (top 200 by cost).

**Daily budget utilization:** Daily cost over the last 14 days for each Shopping campaign.

**Ask for target ROAS.** Default: historical 30-day ROAS.

## Step 1: Item-Level Classification

Sort items by cost (highest first). For each item:

| Classification | Condition | Action |
|---|---|---|
| **KILL** | Cost ≥ 2× AOV AND conversions = 0 | Exclude item ID immediately. No learning window. |
| **DOWNGRADE** | ROAS < 0.7× target AND cost ≥ 0.5× AOV | Lower bid or exclude. Spending but underperforming. |
| **PROMOTE** | Conversions ≥ 2 AND ROAS ≥ target | Isolate into its own product group / campaign to protect budget. |

Items not matching any rule: monitor, no action needed.

## Step 2: Product Group Structure

- Maximum 3 product groups per campaign.
- Split ONLY when economics differ (different margins, price bands, seasonal risk).
- If groups don't have meaningfully different ROAS targets → consolidate.

## Step 3: Search Term Negatives

Add negatives ONLY for wrong-intent terms:

- **Price objection:** free, cheap, budget, discount code, coupon
- **DIY / repair:** diy, repair, fix, how to, tutorial
- **Used / second-hand:** used, second hand, refurbished, pre-owned
- **Products not in feed:** compare search terms to product titles; negate terms for products you don't sell
- **Irrelevant attributes:** colors / sizes not offered

**Do NOT negate high-intent commercial terms even if they haven't converted yet.**

## Step 4: Budget & Bid Decisions

### SCALE (increase budget 10–20%)

**All** must be true:

- Campaign ROAS ≥ target
- Budget utilization ≥ 90% on 10+ of the last 14 days
- Top 20% of SKUs by conversions account for ≥ 60% of spend (winners are getting the budget)

### CUT / CAP (reduce budget or exclude SKUs)

**Any** true:

- Campaign ROAS < target
- SKUs with ROAS < 0.7× target receiving increasing spend share WoW

→ Reduce budget OR exclude underperforming SKUs first, then reassess.

## Step 5: Device & Location (last)

Only analyze if segment spend ≥ 2× AOV (enough data to judge).

- Exclude device/location ONLY if ROAS ≤ 0.6× account average AND no operational explanation (e.g. mobile site is broken).
- Check for technical issues before excluding (site speed, checkout flow).

## Step 6: Campaign Kill Conditions

Pause the Shopping campaign if:

- ROAS < 0.6× target after total spend ≥ 2× AOV
- Shopping ROAS consistently worse than Search ROAS over 30+ days

## Prohibitions

- Never optimize by CTR alone — Shopping is ROAS-driven.
- Never let cheap, low-converting SKUs dominate spend.
- Never scale without confirming winners are getting the budget.

## Output Format

```
### Feed Health
- Merchant Center approval rate: X%
- Conversion tracking: [active / inactive]
- Status: [OK to proceed / blocked]

### Item Classification Summary
- KILL: N items, $X estimated monthly savings
- DOWNGRADE: N items, $X estimated savings
- PROMOTE: N items, suggested isolation strategy
- Monitor: N items

### Search Term Negatives
- Recommended additions: [list]
- Estimated savings: $X/day

### Budget Recommendation
- Current: $X/day
- Recommended: $X/day (+/- X%)
- Rationale: [SCALE / CUT / HOLD with reasons]

### Expected 7-day ROAS Impact
- Current ROAS: X.XX (Target: X.XX)
- Projected ROAS after kills/negatives: X.XX
```

## Minimum required data (by source)

| Source | What you need |
|---|---|
| MCP | (1) Account-level AOV (total conv. value / total conversions over lookback). (2) Item-level performance via `shopping_performance_view` (top 200 by cost). (3) Campaign-level Shopping metrics filtered to ENABLED. (4) Search terms for Shopping campaigns. (5) Daily cost segmentation for last 14 days via `segments.date`. (6) Merchant Center approval rate — **manual user check**, not in MCP. |
| CSV | Three separate exports: (1) Campaign Performance for Shopping campaigns; (2) **Products report** for item-level performance; (3) Search Terms report for Shopping. Plus a daily-segmented export for budget utilization. Merchant Center approval rate is a manual check the user must do in Merchant Center. |
| Screenshot / copy-paste | Not workable for full Shopping audit — too many entity-level joins required. |

## Tool hints

The feed-health gate (Step 0) **blocks all optimization** if Merchant Center approval rate is unknown. This is never in MCP or CSV — always ask the user to confirm. The Products report at item level is the second most-missed export (after PMax assets) — many users share a Campaigns export and ask for product-level recommendations that can't be made from it.
