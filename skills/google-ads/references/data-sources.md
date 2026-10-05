# Data Sources

Where each signal comes from, and how Google Ads UI CSV columns map to the API / GAQL fields the skills use.

## Data Source Compatibility Matrix

Use to plan which signals you can get from which source before running any skill.

| Signal | MCP (GoMarble etc. with GAQL) | CSV (Google Ads UI exports) | Screenshot |
|---|---|---|---|
| Campaign performance (cost, conversions, conversion value, clicks, impressions, CTR, avg CPC) | ✅ via standard `metrics.*` fields | ✅ default Campaign report | ✅ if shown |
| Cost in account currency | ✅ but `cost_micros` returned by API — **divide by 1,000,000** | ✅ already in account currency — **skip the micros rule** | ✅ |
| Average CPC | ✅ in account currency (no conversion) | ✅ in account currency | ✅ |
| Search Impression Share, IS Lost (Rank), IS Lost (Budget) | ✅ via `metrics.search_impression_share`, `search_rank_lost_impression_share`, `search_budget_lost_impression_share` | ✅ but column names vary ("Search lost IS (rank)" / "Impr. share lost (rank)") — match by meaning | ⚠️ |
| Top of Page Rate / Absolute Top of Page Rate | ✅ via `metrics.top_impression_percentage`, `absolute_top_impression_percentage` | ✅ default Search columns | ⚠️ |
| Search term report | ✅ via `search_term_view` resource | ✅ separate "Search Terms" report — **not in the Campaigns export** | ❌ |
| Keyword-level performance | ✅ via `keyword_view` resource | ✅ separate "Keywords" report | ⚠️ |
| Quality Score components (Expected CTR / Ad Relevance / Landing Page) | ✅ via `ad_group_criterion.quality_info.*` | ⚠️ requires Quality Score columns enabled in the Keywords report | ❌ |
| Bid strategy + target | ✅ via `campaign.bidding_strategy_type` + `target_cpa.target_cpa_micros` / `target_roas.target_roas` | ⚠️ requires Bid Strategy + Target columns enabled (often not default) | ⚠️ |
| Daily budget utilization | ✅ via `segments.date` aggregation | ⚠️ requires day-by-day segmented export | ❌ |
| Shopping item-level performance | ✅ via `shopping_performance_view` | ✅ separate "Products" report | ❌ |
| Merchant Center approval rate | ❌ requires manual check in Merchant Center | ❌ same | ❌ same |
| PMax asset performance labels (BEST / GOOD / LOW / PENDING / UNSPECIFIED) | ✅ via GAQL on `asset_group_asset` with `performance_label` | ❌ **NOT in default exports** — requires Asset Report (separate UI report) | ❌ |
| PMax search term insights (aggregated categories) | ✅ via GAQL on `campaign_search_term_insight` | ❌ **NOT in default exports** — requires Search Terms Insights from the PMax campaign page | ❌ |
| PMax asset group structure (asset group ID, name, status) | ✅ via `asset_group` | ⚠️ partial — visible in PMax campaign page but not always in exports | ⚠️ |
| Device performance | ✅ via `segments.device` | ✅ separate "Devices" segment export | ⚠️ |
| Geographic performance | ✅ via `geographic_view` | ✅ separate "Locations" report | ⚠️ |
| Time-of-day / day-of-week | ✅ via `segments.day_of_week` / `hour` | ✅ separate "Time" segment export | ⚠️ |
| Auction Insights (competitor share) | ⚠️ limited via API (`auction_insight_domain`) | ✅ separate "Auction Insights" UI report | ⚠️ |
| Conversion type / value source | ✅ via `conversion_action` resource + `segments.conversion_action_category` | ⚠️ requires "Conversion action" segment + "All conv. value" enabled | ❌ |
| Keyword Planner data (volume, top-of-page bid, competition) | ✅ via `google_ads_keyword_discover` / `google_ads_keyword_metrics` (GoMarble) | ✅ via Keyword Planner export | ❌ |

✅ = available and reliable. ⚠️ = available but requires extra export / column / segment enabled. ❌ = not available from this source.

---

## Google Ads CSV Column Translation

When the source is a CSV export from the Google Ads UI, column names rarely match the API field names used throughout the skills. Use this table to translate. Column names vary slightly by language, account version, and export template — **match by meaning, not exact string**.

| Skill / API reference | Typical Google Ads CSV column |
|---|---|
| `metrics.cost_micros` | "Cost" (already in account currency in CSV — micros rule does not apply) |
| `metrics.conversions` | "Conversions" |
| `metrics.conversions_value` | "Conv. value" or "All conv. value" |
| `metrics.clicks` | "Clicks" |
| `metrics.impressions` | "Impr." |
| `metrics.ctr` | "CTR" |
| `metrics.average_cpc` | "Avg. CPC" |
| `metrics.search_impression_share` | "Search impr. share" |
| `metrics.search_rank_lost_impression_share` | "Search lost IS (rank)" / "Impr. share lost (rank)" |
| `metrics.search_budget_lost_impression_share` | "Search lost IS (budget)" / "Impr. share lost (budget)" |
| `metrics.top_impression_percentage` | "Top impr. rate" / "Search top IS" |
| `metrics.absolute_top_impression_percentage` | "Abs. top impr. rate" / "Search abs. top IS" |
| `metrics.value_per_conversion` (ROAS = this / cost) | "Conv. value / cost" or compute as Conv. value ÷ Cost |
| `campaign.bidding_strategy_type` | "Bid strategy type" (must enable) |
| `target_cpa.target_cpa_micros` | "Target CPA" |
| `target_roas.target_roas` | "Target ROAS" |
| `campaign.budget_amount_micros` | "Budget" or "Daily budget" |
| `ad_group_criterion.quality_info.quality_score` | "Quality Score" (must enable in Keywords report) |
| `ad_group_criterion.quality_info.creative_quality_score` | "Ad relevance" (must enable) |
| `ad_group_criterion.quality_info.post_click_quality_score` | "Landing page experience" (must enable) |
| `ad_group_criterion.quality_info.search_predicted_ctr` | "Expected CTR" (must enable) |
| `asset_group_asset.performance_label` | ❌ NOT in standard CSV — requires Asset Report from the PMax campaign |
| `campaign_search_term_insight.*` | ❌ NOT in standard CSV — requires Search Terms Insights from PMax campaign page |

**Rule for Claude:** if the source is CSV, **costs are already in account currency** — never apply the divide-by-1,000,000 rule. That rule only fires on raw API/MCP data.
