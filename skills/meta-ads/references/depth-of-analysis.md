# Depth-of-Analysis Framework — Apply on Audits & Optimization Reviews

**Contents:** 1. Hierarchical Drill-Down · 2. Objective-Contextual Evaluation · 3. Breakdown & Segmentation Analysis · 4. Temporal & Trend Analysis · 5. Cross-Entity Dependency Mapping · 6. Platform Mechanic Awareness · 7. Proactive Signal Detection · 8. Attribution Rigor

Apply on: audits, performance reviews, optimization requests, strategy questions, funnel analysis.
Skip for: simple data fetches, campaign listings, single-metric lookups.

## 1. Hierarchical Drill-Down

Never recommend on campaign-level or ad-set-level aggregates alone. Drill one level deeper.

- Asked about a campaign → check ad set performance within it.
- Asked about an ad set → check individual ad performance within it.
- Asked about ads → check creative-level patterns (same creative across multiple ads).

Quantify the contribution: *"Ad Set X accounts for 72% of campaign spend but only 40% of conversions."*

## 2. Objective-Contextual Evaluation

Do not apply universal KPIs. Evaluate each campaign against its actual objective.

**Check first:**

- The ad-set-level optimization event (the actual `custom_event_type` — not the name)
- The campaign objective
- Bid strategy (cost cap, bid cap, lowest cost)

**Apply correct KPIs:**

| Objective | Evaluate on | NOT on |
|---|---|---|
| Sales / Purchase | ROAS, CPA, revenue | Reach, CPM alone |
| Lead gen | CPL, lead volume | ROAS |
| Traffic | CPC, CTR, landing page views | Conversions |
| Video views | Cost per ThruPlay, hook rate | ROAS, CPA |
| Awareness | CPM, reach, frequency | CPA, ROAS |

**Flag bid-strategy issues:** if a cost cap is set 3× above actual CPA, or tROAS target is 0.5× when achieving 3×, the algorithm isn't actually constrained. Call it out.

## 3. Breakdown & Segmentation Analysis

For audits, performance reviews, and optimization work, check **at least 2** of these dimensions. (This overrides the general guidance to only use breakdowns when specifically requested — deep analysis requires segmentation.)

- Placement (Feed vs Stories vs Reels vs Audience Network) — quantify CPA gaps
- Device (mobile vs desktop)
- Age / gender — flag Advantage+ expansion leakage if delivery is going outside the target
- Out-of-target segments consuming budget with poor conversion rates

**Statistical significance check:** do not make segment-level recommendations from < 100 impressions or < 3 conversions in a segment. Call out low-confidence segments explicitly.

## 4. Temporal & Trend Analysis

Never treat the date range as a single static number. Always compare time windows.

- Last 7 days vs previous 7 days
- Identify direction for each key metric: improving, declining, stable
- Flag inflection points: *"CTR started declining on [date], 3 days before CPA started rising"*

**Connect the chain:** frequency rising → CTR falling → CPA rising → this is creative fatigue, not audience exhaustion. Correlate timing across metrics to establish cause, not just observe symptoms.

## 5. Cross-Entity Dependency Mapping

Don't analyze campaigns in isolation. Map the funnel.

- Which campaigns are **prospecting** (broad / lookalike audiences)?
- Which campaigns are **retargeting** (custom audiences, website visitors)?
- Does pausing a prospecting campaign starve the retargeting audience pool?

**How to identify:**

- Prospecting: low frequency, lower CPM, lower CTR, broader audience
- Retargeting: higher frequency, higher CPM, higher CTR, smaller audience
- Check the targeting object on each ad set — presence of custom audiences = retargeting / warm

**Flag dependencies:** *"Pausing Campaign X will reduce the Website Visitors 7-day pool that feeds Campaign Y's retargeting. Expect retargeting CPA to rise within 1–2 weeks."*

## 6. Platform Mechanic Awareness

Explain how Meta's mechanics affect the specific situation — explain the compound interaction, don't just mention the mechanic.

| Signal | Mechanic | Consequence |
|---|---|---|
| Rising frequency + falling CTR | Creative fatigue | CPA will spike — need new creatives, not budget changes |
| CBO + one ad set getting 80% budget | CBO optimization | Usually working as intended. Do not recommend pausing the dominant ad set on small-sample noise. Only intervene if the dominant ad set itself is underperforming on ROAS/CPA. |
| Cost cap + rising CPM | Delivery squeeze or audience shift | Two possible causes — separate before acting: (a) algorithm can't find conversions at the cap (raise cap or loosen targeting); (b) original audience is saturated and delivery is leaking to worse segments. Check frequency, reach trend, and audience size to decide which. |
| Advantage+ audience expansion ON | Targeting leakage | Check breakdowns for out-of-target delivery eating budget |
| Insufficient spend on new ad set | Learning phase | No optimization decisions until the ad set has spent at least **2× AOV or 4× CPA, whichever is higher**. The 50-conversion rule only applies to brand-new accounts with no prior history. |

## 7. Proactive Signal Detection

After answering the user's question, surface 2–3 additional concerns or opportunities they didn't ask about.

Scan for:

- Any entity with frequency > 3 and rising — creative fatigue incoming
- Any ad set spending > 30% of campaign budget with 0 conversions — budget waste
- Any campaign where the top ad has declining CTR over 7+ days — degradation ahead
- Any retargeting audience pool shrinking (declining reach WoW)
- Any metric that looks fine now but the trend predicts problems in 7–14 days

Format: *"Outside your question, I noticed [signal] in [entity] — this suggests [predicted consequence] within [timeframe]."*

## 8. Attribution Rigor

Don't take reported conversion numbers at face value.

Always check:

- What attribution window is active? (1-day click, 7-day click, 1-day view?)
- What share of conversions are view-through vs click-through?
- Is the reported ROAS inflated by view-through on high-impression campaigns?

Flag these situations:

- Retargeting campaign with very high ROAS + mostly view-through conversions → likely over-attributed
- Two campaigns targeting the same audience → conversions may be double-counted
- Advantage+ Shopping targeting existing customers → attributed ROAS includes conversions that would have happened organically

Frame as caveat: *"Before scaling Campaign X based on its reported 4× ROAS, note that [specific attribution concern] means the true incremental ROAS is likely lower."*
