# Skill 3: Performance Max (PMax) Optimization

**Contents:** When to use this skill · Maturity Gate (BLOCKING) · Data to gather · Phase 1 — Evaluate Performance · Phase 2 — Scale (only if Phase 1 confirms profitability) · PMax Limitations (do NOT recommend these) · Prohibitions · Output Format · Minimum required data (by source) · Tool hints

PMax is machine-learning-led: multi-channel (Search, Display, YouTube, Gmail, Discover), asset-driven, with limited granular control. It requires maturity before optimization.

## When to use this skill

- Audit or optimize an existing PMax campaign
- Decide whether PMax is worth keeping vs. shifting spend to Search/Shopping
- Plan scaling for a profitable PMax campaign
- Diagnose why PMax ROAS is below Search ROAS

## Maturity Gate (BLOCKING)

Campaign must meet **one** of:

- Age ≥ 30 days (ideally 60)
- Total conversions ≥ 50

**If neither met → WAIT. Do not optimize.** ML has not stabilized.

**Exception:** if the campaign is clearly burning money (ROAS < 0.3× target after spend ≥ 3× AOV), recommend pausing — even pre-maturity.

## Data to gather

Ask the user to share — or pull from whatever data source is available — over the **last 30 days** (use 60 days for trend analysis):

**Campaign performance:** Campaign ID, name, status, start date, impressions, clicks, CTR, cost, conversions, conversion value. Filter to PMax campaigns.

**Asset group details:** Campaign ID, asset group ID, name, status.

**Asset performance labels:** For each asset (image, video, headline, description) within each asset group, the performance label: BEST / GOOD / LOW / PENDING / UNSPECIFIED.

**Device performance:** Cost, conversions, conversion value, clicks, impressions per device (mobile / desktop / tablet) for each PMax campaign.

**Geographic performance:** Cost, conversions, conversion value per location (top 200 by cost).

**Time series:** Daily cost, conversions, conversion value over the last 60 days for trend analysis.

**Search term insights (PMax-aggregated):** Category labels, clicks, impressions, conversions, cost. Note: PMax provides aggregated categories only, not individual terms.

**PMax vs Search comparison:** Cost, conversions, conversion value for both PMax AND Search campaigns over the same window.

**Ask for:** Target ROAS, target CPA, initial budget (for scaling caps), priority locations.

## Phase 1 — Evaluate Performance

### Step 1: PMax vs Search Comparison

Calculate ROAS for each channel type and compare:

| PMax ROAS Ratio | Assessment | Action |
|---|---|---|
| < 0.5× Search ROAS | Poor | Monitor closely; consider pausing if not improving |
| 0.5 – 0.9× Search ROAS | Below par | Optimize assets and negatives before any scaling |
| ≥ 0.9× Search ROAS | Healthy | Proceed with optimization; eligible for scaling |
| > Search ROAS | Outperforming | Prioritize scaling |

**Also check for brand cannibalization:** review PMax search term categories. If brand terms appear, correlate PMax conversion growth with Brand Search impression share decline over the same window. Flag inflated PMax ROAS.

### Step 2: Asset Performance Analysis

Group by asset type (images, videos, headlines, descriptions). For each asset:

| Label | Action |
|---|---|
| **BEST** | Create variations with similar style/messaging. This is working — make more like it. |
| **GOOD** | Keep, monitor. No changes needed. |
| **LOW** | Remove from asset group. Replace with variations of BEST performers. |
| **PENDING / UNSPECIFIED** | Wait for more data (typically 14+ days). |

### Step 3: Device & Location

**Device:**

| Device CPA vs Account | Action |
|---|---|
| > 1.5× account CPA | Check site/funnel usability on that device first. If no issues → consider -50% bid adjustment or exclusion. |
| > 2× account CPA | Strong candidate for exclusion after confirming no technical issues. |
| CVR < 0.5× account CVR | Check landing page experience on that device. |

**Location:**

| Location CPA vs Account | Action |
|---|---|
| > 1.5× account CPA | Consider excluding |
| > 2× account CPA | Exclude |
| Spend but 0 conversions | Wait for more data, OR exclude if spend ≥ 2× AOV |

**Always check for technical/usability issues before excluding a device or location.**

### Insights Tab Review (qualitative)

If the user has access to the PMax Insights tab in the Google Ads UI:

- **Audience Insights:** which audience types are getting majority of clicks (cannot see conversion performance directly — infer by click volume).
- **Asset Insights:** overlap of assets and audiences. Use this to plan new asset groups for high-performing segments.

## Phase 2 — Scale (only if Phase 1 confirms profitability)

### Scaling Prerequisites

**All** must be true before scaling:

- Campaign profitable for 14–30 consecutive days
- ROAS ≥ target (default 300% if not specified)
- CPA ≤ target
- Performance trends stable or improving WoW

### Budget Scaling

Increase daily budget by **20–50%** every 14–30 days.

| Scenario | Action |
|---|---|
| Profitable 14+ days, trends stable | Increase 20–50% |
| Post-scaling CPA > 1.2× target | PAUSE scaling, optimize assets/negatives, reassess after 30 days |
| Post-scaling ROAS < 0.8× target | PAUSE scaling, optimize, reassess after 30 days |
| Consistently profitable 90+ days | Can exceed 2–3× initial budget cap |

**Hard cap:** do not exceed 2–3× initial monthly budget until 90+ days of consistent profitability.

### Location Expansion

- Only after core locations profitable for 30+ days.
- Expand to similar / adjacent markets.
- Create separate asset groups for new locations if targeting differs.
- Monitor new locations independently for 30 days before further expansion.

### Audience Expansion

- Start with **Observation** mode for new audience signals.
- Monitor performance for 14+ days.
- Switch to **Targeting** mode only if performance holds.
- Do NOT force audience preferences without data.

### Asset Expansion

Based on BEST-performing assets from evaluation:

| Asset Type | Expansion Rule |
|---|---|
| Images | Add 5–10 total, similar style to BEST, different angles/contexts |
| Headlines | Variations of BEST — same theme, different wording. Test different CTAs. |
| Descriptions | Variations of BEST — same value props, different framing |
| Videos | Test 30-second formats if shorter videos are BEST |
| New asset groups | For high-performing audience segments identified in Insights |

## PMax Limitations (do NOT recommend these)

- No keyword targeting
- No budget per asset group
- No placement control
- No demographic control
- No channel-level budget control
- Search term data is aggregated categories only, not individual terms

## Prohibitions

- Never optimize before 30 days OR 50 conversions (unless burning money)
- Never scale before 14 days of profitability
- Never increase budget > 50% in one step
- Never scale beyond 2–3× initial budget before 90 days of profitability
- Never continue scaling if CPA > 1.2× target OR ROAS < 0.8× target
- Never remove BEST or GOOD performing assets
- Never force device/location exclusions without checking for technical issues first

## Output Format

```
### Current State
- Campaign age: X days (Ready: Yes/No)
- Total conversions: X (Minimum met: Yes/No)
- Status: [Ready for optimization / Still stabilizing]

### Performance vs Search
- PMax ROAS: X.XX (Target: X.XX)
- Search ROAS: X.XX
- Ratio: X.XX (PMax is XX% of Search performance)
- Assessment: [Outperforming / Acceptable / Underperforming / Poor]

### Asset Group Analysis
- BEST assets: [list with action — create variations]
- GOOD assets: [list — keep, monitor]
- LOW assets: [list — remove and replace]
- PENDING assets: [list — wait]

### Device Performance
- Per-device CPA vs account; flagged exclusion candidates

### Location Performance
- Top locations by spend; flagged exclusion candidates

### Scaling Recommendation
- Days profitable: X
- Recommendation: [SCALE / OPTIMIZE FIRST / PAUSE]
- If SCALE: current $X/day → recommended $X/day (+X%); cap at $X/month
- If OPTIMIZE FIRST: reason and required fixes
- If PAUSE: reason

### Expansion Opportunities (if applicable)
- Locations, audiences, asset variations to test

### Expected Outcomes (30-day horizon)
- CPA: $X → $X
- ROAS: X.XX → X.XX
- Monitoring priorities
```

## Minimum required data (by source)

PMax has the **largest data-source gap** of any skill. Many users share a campaign-level export and ask for asset and search-term recommendations that simply cannot be made from it.

| Source | What you need |
|---|---|
| MCP (with GAQL) | (1) Campaign performance over 30d (60d for trend) via `campaign`; (2) **Asset group structure** via `asset_group`; (3) **Asset performance labels** via GAQL on `asset_group_asset` with `performance_label` field; (4) **Search term insights** via GAQL on `campaign_search_term_insight`; (5) Device segment via `segments.device`; (6) Geographic segment via `geographic_view`; (7) PMax vs Search comparison — pull both with same date range. |
| CSV | **Requires four to five separate exports** that users frequently miss: (a) Campaign Performance for PMax campaigns; (b) **Asset Report from the PMax campaign page** (gives BEST / GOOD / LOW labels); (c) **Search Terms Insights from the PMax campaign page** (gives aggregated categories — NOT the regular Search Terms report); (d) Devices segment; (e) Locations segment. Plus a Search-campaigns export with same window for the PMax vs Search ROAS comparison. |
| Screenshot / copy-paste | Not workable for full PMax audit. Possibly workable for a single yes/no question (e.g. "is my PMax mature enough to optimize?"). |

**Before running this skill on CSV data**, explicitly check whether the user has the Asset Report and Search Term Insights. If they don't, ask them to pull both before continuing — or fall back to the MCP path.

## Tool hints

PMax's "limitations" cut both ways: the platform exposes less, but Google Ads API still has the resources Claude needs. The two resources that turn an incomplete PMax audit into a complete one are `asset_group_asset` (for performance labels) and `campaign_search_term_insight` (for the aggregated category data). Both require GAQL. If the connected MCP supports arbitrary GAQL (e.g. GoMarble's `google_ads_run_gaql`), use it. The CSV alternative — running two separate UI reports from the PMax campaign page — is the most common point of friction in PMax audits and worth flagging early in the conversation.
