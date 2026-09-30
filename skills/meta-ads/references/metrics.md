# Metric Glossary — Canonical Definitions

Used across every skill. Two critical rules that belong to this glossary — **Purchase De-Duplication** and the **COMPLETE_REGISTRATION on PURCHASE objective** check — live in SKILL.md so they are always loaded.

## Currency Note

Meta API budget values are typically in **cents** (integer). $50 = 5000 cents. If you see raw integer budget values from an API or export, divide by 100 to display. **Confirm account currency before showing monetary values — never assume USD.**

## Direct Metrics

| Metric | Notes |
|---|---|
| Spend | Total spend in account currency |
| CPM | Cost per 1,000 impressions |
| CTR | Click-through rate (decimal or %) |
| Impressions | |
| Clicks | |
| Reach | Unique users reached |
| Frequency | Average impressions per user |
| Video Plays | Initial impressions of the video |
| 3-Second Views | "video_view" actions — hook engagement (this is inside the `actions` array, not a separate field) |
| ThruPlays | 15-second or completed video watches |
| Purchases | Use ONE purchase action type only — see Purchase De-Duplication below |
| Leads | Lead events |
| Revenue | Conversion value for purchases |
| Purchase ROAS | Returned directly by Meta |

## Calculated Metrics

| Metric | Formula |
|---|---|
| Hook Rate | (3-second views / video plays) × 100 — **API/MCP source: use the `video_view` action inside the actions array, NOT `video_p25_watched_actions`.** **CSV source: use the "3-Second Video Plays" column directly — it's already pre-computed; the action-name distinction does not apply.** |
| Hold Rate | (ThruPlays / 3-second views) × 100 — for CSV, use "ThruPlays" ÷ "3-Second Video Plays" columns directly. |
| Cost Per Purchase | spend / purchases |
| Cost Per Lead (CPL) | spend / leads |
| Cost Per Result (CPR) | spend / specific custom-event count |
| Conversion Rate (CVR) | conversions / clicks × 100 |
| Budget Utilization | spend / (daily budget × days in period) |
| Campaign Spend Share | entity spend / parent total spend (require ≥ 25% before comparing ad sets) |
| Pareto Set | Sort ads by spend desc; keep ads where cumulative spend ≤ 90% |

## Account Type → Primary Conversion Metric (PCM)

Read the **promoted object / conversion event** from each ad set. **Never infer from campaign or ad set names** — names frequently don't match the actual config.

| Custom Event Type | Account Type | PCM |
|---|---|---|
| PURCHASE | Ecommerce | Purchase ROAS |
| LEAD | Lead generation | Cost per Lead |
| COMPLETE_REGISTRATION | Registration | Cost per Registration |
| OTHER (custom event) | Custom conversion | Cost per Result for that specific event |

If the promoted object is missing → **ask the user**. Never assume.

**Mixed accounts**: group ad sets by their custom event type. Each group gets its own PCM. Do not mix conversion types across groups.

## Performance Benchmarks

| Metric | Good | Average | Poor |
|---|---|---|---|
| Hook Rate | ≥ 40% | 26–39% | < 25% |
| Hold Rate | > Account Avg + 25% | ≈ Account Avg | < Account Avg |
| CTR | ≥ 1.25% | 0.65 – 1.24% | < 0.65% |
| CPM variance vs Pareto avg | ≤ 20% | 20 – 60% | > 60% |
| PCM variance vs Pareto avg | Above avg | ± 20% | > 30% below |
| Budget utilization | ≥ 85% | — | < 85% |
| Min ad-set spend share for comparison | ≥ 25% of campaign | — | — |

For Hold Rate, compute the account average from a 90-day account-level pull (video fields aggregated) before applying the comparison.

## Statistical Significance Floors

| Decision | Minimum signal |
|---|---|
| Per-ad-set performance judgment | 3–5 conversions / week |
| Per-segment recommendation (placement, age, device) | ≥ 100 impressions AND ≥ 3 conversions |
| Pause ad on high CPA | ≥ 3 conversions if non-zero, OR spend ≥ 2× ad-set CPA target if zero |
| Ad set learning-phase exit | Spend ≥ 2× AOV OR 4× CPA, whichever is higher |

## Diagnostic Signals (used in skills below)

| Signal | Meaning |
|---|---|
| Frequency rising AND CTR falling over 14+ days | Creative fatigue |
| CBO with one ad set holding 80%+ of budget | Algorithm working as intended — do NOT pause the dominant ad set on small-sample noise |
| High frequency alone (no CTR drop) | Not fatigue |
| Cost cap + rising CPM | Either delivery squeeze OR audience saturation — separate before acting |

## Video Funnel

```
Video Plays → Hook Rate → 3-Second Views → Hold Rate → ThruPlays
```
