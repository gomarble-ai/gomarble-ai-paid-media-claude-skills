# Data Sources

Where each signal comes from, and how Ads Manager CSV columns map to the API fields the skills use.

## Data Source Compatibility Matrix

Use to plan which signals you can get from which source before running any skill.

| Signal | MCP (GoMarble / Meta / etc.) | CSV (Ads Manager export) | Screenshot |
|---|---|---|---|
| Spend, impressions, clicks, CTR, CPM, reach, frequency | ✅ direct | ✅ default columns | ✅ if shown |
| Purchase count (deduplicated) | ✅ via `actions` array — apply Purchase De-Duplication rule | ✅ "Purchases" column (Meta already deduplicates — **skip the dedup rule**) | ⚠️ if shown |
| Purchase ROAS | ✅ `purchase_roas` field | ✅ "Purchase ROAS" column (must be enabled) | ⚠️ |
| Revenue / conversion value | ✅ `action_values` | ✅ "Purchases Conversion Value" column | ⚠️ |
| Video Plays | ✅ `video_play_actions` | ✅ "Video Plays" column | ❌ rarely shown |
| 3-Second Video Plays | ✅ via `actions` (`video_view` action) | ✅ "3-Second Video Plays" column (already pre-computed — **skip the action-name distinction**) | ❌ rarely shown |
| ThruPlays | ✅ via `actions` | ✅ "ThruPlays" column | ❌ rarely shown |
| Hook Rate / Hold Rate | ❌ must compute from the above | ❌ must compute from the above | ❌ |
| Promoted object / `custom_event_type` | ✅ from ad set object | ❌ NOT in default CSV exports — **ask user to confirm per ad set / campaign** | ❌ |
| Campaign objective, ad set bid strategy, bid amount | ✅ direct | ⚠️ requires "Bid Strategy" + "Bid Amount" columns enabled (often not default) | ⚠️ |
| Full targeting object (audiences, interests, custom audiences) | ✅ via ad set object | ❌ NOT in CSV — **must be described by user or pulled via MCP** | ⚠️ if visible |
| EMQ Score | ❌ not in standard insights APIs — **manual check in Events Manager** | ❌ same | ❌ same |
| Audience Segment breakdown (New / Engaged / Existing) | ✅ insights with `breakdowns=['user_segment_key']` | ⚠️ requires a *separate* breakdown export | ❌ |
| Placement breakdown (Feed / Stories / Reels / etc.) | ✅ `breakdowns=['publisher_platform','platform_position']` | ⚠️ requires separate breakdown export | ❌ |
| Age / gender breakdown | ✅ `breakdowns=['age','gender']` | ⚠️ separate export | ❌ |
| Geographic / device breakdown | ✅ via breakdowns | ⚠️ separate export | ❌ |
| Ad creative content (video file, image, copy) | ✅ via creative endpoint (e.g. `facebook_get_ad_creative_details`) | ❌ never in CSV — **must be shared separately** | ⚠️ |
| Comments / sentiment | ❌ requires manual check in Ads Manager or the Page | ❌ same | ⚠️ if shown |
| Attribution window settings | ✅ via ad set `attribution_spec` | ⚠️ requires "Attribution Setting" column | ❌ |
| Daily time-series (for trend / fatigue detection) | ✅ insights with `time_increment=1` | ⚠️ requires day-by-day export | ❌ |
| 3rd-party tracker config (Profitmetrics / Triple Whale etc.) | ✅ inferred from `custom_event_type` on PURCHASE campaign objective | ❌ **must ask user explicitly** — see the COMPLETE_REGISTRATION check in SKILL.md | ❌ |

✅ = available and reliable. ⚠️ = available but requires extra export / setup. ❌ = not available from this source.

---

## Meta CSV Column Translation

When the source is a CSV export from Ads Manager, the column names rarely match the API field names used throughout the skills. Use this table to translate. (Column names vary slightly by language and export template — match by meaning, not by exact string.)

| Skill / API reference | Typical Ads Manager CSV column |
|---|---|
| `spend` | "Amount spent (USD)" / "Amount Spent" / "Spend" |
| `impressions` | "Impressions" |
| `reach` | "Reach" |
| `frequency` | "Frequency" |
| `cpm` | "CPM (cost per 1,000 impressions)" |
| `ctr` | "CTR (all)" or "CTR (link click-through rate)" |
| `clicks` | "Link clicks" or "Clicks (all)" |
| `purchase` / `omni_purchase` (deduped) | "Purchases" (Meta has already deduplicated) |
| `purchase_roas` | "Purchase ROAS (return on ad spend)" |
| Revenue (conversion value) | "Purchases Conversion Value" |
| `video_view` action (3-second views) | "3-Second Video Plays" (already pre-computed) |
| ThruPlays | "ThruPlays" |
| Video Plays | "Video Plays" |
| Leads | "Leads" or "On-Facebook Leads" + "Off-Facebook Leads" — confirm with user which is the conversion event |
| Campaign objective | "Campaign Objective" (often not in default export — must enable) |
| Bid strategy | "Bid Strategy" (often not in default export — must enable) |
| Daily / lifetime budget | "Budget" or "Campaign Budget" / "Ad Set Budget" |
| Attribution window | "Attribution Setting" |
| `custom_event_type` / promoted_object | ❌ NOT in CSV — ask user to confirm |

**Rule for Claude:** if a CSV column maps to a pre-computed metric (Purchases, 3-Second Video Plays, ThruPlays), use it directly and skip the upstream dedup / action-array rules. Those rules exist to clean raw API data.
