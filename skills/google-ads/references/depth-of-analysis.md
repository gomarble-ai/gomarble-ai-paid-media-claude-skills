# Depth-of-Analysis Framework — Apply on Audits & Optimization Reviews

Apply on: audits, performance reviews, optimization requests, strategy questions, account restructuring.
Skip for: simple data fetches, campaign listings, single-metric lookups.

## 1. Hierarchical Drill-Down

Never recommend on campaign-level aggregates alone. Drill deeper:

- Asked about a campaign → check ad group performance within it.
- Asked about an ad group → check keyword + search term performance within it.
- Asked about PMax → check asset group performance, search term categories, URL expansion config.

Quantify the driver: "Ad Group X accounts for 65% of campaign spend but CPA is 2× the campaign average."

## 2. Objective-Contextual Evaluation

Evaluate each campaign against its bid strategy target, not just absolute performance.

| Bid Strategy | Evaluate against | Red flag |
|---|---|---|
| tCPA | Actual CPA vs target CPA | CPA 30%+ above target |
| tROAS | Actual ROAS vs target ROAS | ROAS 30%+ below target |
| Maximize Conversions (no target) | CPA trend direction | Rising CPA with no constraint |
| Manual CPC | CPC vs Quality Score implied CPC | Paying premium due to low QS |

**Flag unconstrained strategies:** if tROAS target is 0.5× on a campaign achieving 3×, the algorithm isn't actually constrained. If tCPA is 3× above actual CPA, same problem. Call it out.

## 3. Breakdown & Segmentation Analysis

Before concluding, check at least 2 of these dimensions:

- Device performance (mobile vs desktop CPA gap)
- Search Partners conversion rate vs Search network (quantify the gap)
- Geographic variations (regions with high spend and poor CVR)
- Day-of-week patterns
- Cross-reference bid adjustments against actual segment performance

**Statistical significance:** Do not make segment-level recommendations from < 50 clicks or < 5 conversions. Flag as low-confidence.

## 4. Temporal & Trend Analysis

Never treat the date range as a single number. Compare:

- Last 7 days vs previous 7 days (WoW)
- Separate day-of-week seasonality from structural trends
- Identify direction for each key metric: improving, declining, stable

**Distinguish:** "metric is bad" vs "metric is getting worse" — direction matters more than absolute value.

**Connect the chain:** impression share declining → CPC increasing → competitive pressure, not quality degradation.

## 5. Cross-Entity Dependency Recognition

- **Brand Search ↔ PMax overlap**: Is PMax capturing brand terms? Check PMax search term categories.
- **Non-brand Search → Remarketing**: Does non-brand search activity feed remarketing lists?
- **Shopping ↔ Search overlap**: Same products advertised in both? Check for cannibalization.

**Flag dependencies:** "PMax and Brand Search are both converting on brand terms. Total reported conversions across both campaigns likely exceed actual unique conversions. Before scaling PMax based on its ROAS, factor in cannibalization from Brand Search."

## 6. Platform Mechanic Awareness

| Signal | Mechanic | Consequence |
|---|---|---|
| Broad match + rising CPC | Query expansion | Algorithm widens to less relevant queries → QS drops → CPC rises → tCPA struggles |
| Low QS + high CPC | Ad relevance | Paying premium for same position — fix relevance, not just bid |
| tCPA + low conversion volume | Smart Bidding data | Insufficient signal — consider Manual CPC |
| PMax + declining Brand Search IS | Brand cannibalization | PMax claiming brand conversions → inflated PMax ROAS |
| Maximize Conversions + no target | Unconstrained spend | Algorithm spends full budget at any CPA — add a tCPA target |

## 7. Proactive Signal Detection

After answering the user's question, surface 2–3 additional concerns or opportunities they didn't ask about.

Format: *"Outside your question, I noticed [signal] in [entity] — this suggests [predicted consequence] within [timeframe]."*

## 8. Attribution & Measurement Rigor

Don't take reported conversion numbers at face value.

Always check:

- Attribution model in use (last click, data-driven, etc.)
- Conversion lag — are recent days' conversions still incomplete?
- Share of conversions that are estimated (modeled) vs observed
- Mix of micro- vs macro-conversions

**Frame as caveat:** *"Before scaling based on the reported 5× ROAS, note that [attribution concern] means the true incremental ROAS is likely lower."*
