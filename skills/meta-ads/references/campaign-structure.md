# Skill 3: Campaign Structure Analysis

**Contents:** When to use this skill · Data to gather · Step 1: Identify Retargeting Campaigns · Step 2: Match the Active Structure to One of These Patterns · Output · Minimum required data (by source) · Tool hints

Identify the strategic pattern behind how the account splits spend across campaigns. Different structures need different evaluation rules.

## When to use this skill

- Account audits
- When the user asks "is my campaign structure right?"
- Before doing ad-set-level analysis (the structure type changes what comparisons are valid)

## Data to gather

For each active (non-retargeting) campaign:

- Objective, bid strategy, daily/lifetime budget, status
- Ad-set level: bid strategy, optimization goal, promoted object (the conversion event), budget, attribution window, full targeting object
- Spend distribution at the campaign level over the last 30 days, sorted by spend desc

**Targeting fields to inspect on each ad set:**

| Field | Purpose |
|---|---|
| Age min / max | Demographics |
| Genders | Demographics |
| Geo locations | Geo targeting |
| Custom audiences | Retargeting detection |
| Detailed / flexible targeting (interests, behaviors) | Interest targeting |
| Publisher platforms / placement positions | Placement strategy |
| Languages | Language targeting |

## Step 1: Identify Retargeting Campaigns

Check the targeting custom audiences for: website visitors, past purchasers, video viewers, page engagers.

```
IF targeting.custom_audiences contains retargeting audiences
→ LABEL as "Retargeting Campaign"
→ EXCLUDE from structure analysis
```

## Step 2: Match the Active Structure to One of These Patterns

### Pattern A: Primary vs Testing

**Criteria:**

```
campaign_budget_share = campaign_budget / total_non_retargeting_budget

IF Campaign A:
   - budget_share < 30%
   - ad_count ≥ 5
AND Campaign B:
   - budget_share ≥ 40%
   - ad_count < Campaign A's ad_count
   - 70%+ of ads also exist in Campaign A
→ CONFIRMED: Primary vs Testing structure
```

### Pattern B: Bid Limit Split

**Criteria:**

For campaigns/ad sets (excluding retargeting), compare the targeting objects and bid configurations.

```
IF targeting is IDENTICAL across splits
AND bid_strategy OR bid_amount DIFFERS
→ CONFIRMED: Bid Limit Split
```

### Pattern C: Audience Split

**Criteria:**

For campaigns/ad sets (excluding retargeting), compare interest spec, custom audiences, demographics.

```
IF audiences DIFFER between splits
→ CONFIRMED: Audience Split

NOTE: Different bids/budgets across audience splits is OK.
```

### Pattern D: Too Many Campaigns (Custom Pattern)

**When:** more than one campaign and the structure doesn't fit A, B, or C.

**Investigate using creative inspection** — review the actual creative content of ads in each campaign and look for:

- Video vs Image split
- Catalog vs Static split
- UGC page vs Brand page
- Different products
- Different personas / angles
- Partnership ads vs direct

**Also check:**

- Website URLs across creatives — different funnels / landing pages / domains
- Attribution windows on each ad set — different windows often indicate different testing setups

## Output

Set `campaign_structure`:

- `primary_testing`
- `bid_limit_split`
- `audience_split`
- `custom_pattern: [description]`

This determines which Ad Set Analysis rules apply.

## Minimum required data (by source)

| Source | What you need |
|---|---|
| MCP | Full ad set objects: bid strategy, optimization goal, promoted object, budget, `attribution_spec`, **full targeting object** (custom_audiences, interests, demographics, placements). All directly available. |
| CSV | **Mostly blocked.** CSV exports do not include the full targeting object. You can identify campaign-level pattern from spend distribution + budget, but the targeting-identical-vs-different test (Patterns B and C) cannot be run from CSV alone. **Ask the user to describe targeting per ad set** or pull from MCP. |
| Screenshot / copy-paste | Ask the user to walk through targeting per ad set in plain language. |

## Tool hints

This skill is the most MCP-dependent of the six. The structural patterns (Bid Limit Split, Audience Split) hinge on comparing full targeting specs across ad sets — something the Ads Manager CSV simply doesn't export. If MCP isn't available, ask the user to describe each ad set's audience in their own words, then map manually.
