# Metric Glossary — Canonical Definitions

Used across every skill. Two glossary rules — the **micros currency conversion** and **account-type inference** — live in SKILL.md so they are always loaded.

## Direct Metrics

| Metric | Notes |
|---|---|
| Cost | Total spend in account currency |
| Conversions | Includes all configured conversion actions unless filtered |
| Conversion value | Revenue for value-based conversions |
| Clicks | |
| Impressions | |
| Average CPC | Already in account currency |
| CTR | Decimal (0.05 = 5%) |
| Search IS | Search impression share |
| IS Lost (Rank) | Share of impressions lost due to ad rank (quality + bid) |
| IS Lost (Budget) | Share of impressions lost because campaign hit daily budget |
| Top of Page Rate | Share of impressions appearing above organic results |
| Absolute Top Rate | Share of impressions appearing as the first ad |

## Calculated Metrics

| Metric | Formula |
|---|---|
| CPA | cost / conversions |
| ROAS | conversion value / cost (decimal multiple, e.g. 3.5 = 3.5×) |
| CVR | conversions / clicks × 100 |
| AOV | total conversion value / total conversions |
| CPC trend WoW | (this_week_cpc − last_week_cpc) / last_week_cpc × 100 |
| CPC trend MoM | (this_month_cpc − last_month_cpc) / last_month_cpc × 100 |
| Spend share | entity_cost / total_cost × 100 |

## Maturity & Statistical-Significance Gates

| Gate | Threshold | Rationale |
|---|---|---|
| Smart Bidding minimum (Search) | ≥ 30 conversions / 30 days | Below this, tCPA/tROAS lacks signal |
| Smart Bidding minimum (PMax / Shopping) | ≥ 50 conversions / 30 days | Wider channel mix needs more signal |
| PMax maturity gate | Age ≥ 30 days (ideally 60) OR conversions ≥ 50 | Required before any PMax optimization |
| Segment-level recommendation | ≥ 50 clicks AND ≥ 5 conversions | Below this → flag as low-confidence |
| Scaling step cap | ≤ 20% per move (Search/Shopping); ≤ 50% per move on mature PMax | |
| Lookback for Shopping | 14 days if ≥ 100 purchases/month, else 30 days | |

## PMax vs Search ROAS Comparison

Apply only after the PMax maturity gate passes.

| PMax ROAS Ratio | Assessment | Default Action |
|---|---|---|
| < 0.5× Search ROAS | Poor | Monitor closely; consider pausing if not improving |
| 0.5 – 0.9× Search ROAS | Below par | Optimize assets and negatives before any scaling |
| ≥ 0.9× Search ROAS | Healthy | Optimize; eligible for scaling |
| > Search ROAS | Outperforming | Prioritize scaling |

## PMax Asset Performance Labels

Google labels each PMax asset (it does NOT expose cost/conversion data per asset).

| Label | Interpretation | Default Action |
|---|---|---|
| BEST | Top performer in its asset group | Create variations with similar style |
| GOOD | Acceptable | Keep, monitor |
| LOW | Underperforming | Remove; replace with BEST variations |
| PENDING / UNSPECIFIED | Insufficient data | Wait 14+ days |

## Shopping Item Classification (used in the Shopping skill)

| Classification | Trigger |
|---|---|
| KILL | cost ≥ 2× AOV AND conversions = 0 |
| DOWNGRADE | ROAS < 0.7× target AND cost ≥ 0.5× AOV |
| PROMOTE | conversions ≥ 2 AND ROAS ≥ target |

## Quality Score Components (when CPC is high)

Decompose Quality Score into:

- Expected CTR
- Ad relevance
- Landing page experience

Identify which component is dragging and recommend fixes for that component. **Do not recommend bid changes alone to compensate for low Quality Score.**
