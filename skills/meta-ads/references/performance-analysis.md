# Skill 5: Performance Analysis

**Contents:** When to use this skill · Step 1: Confirm Account Type & PCM · Step 2: Pareto Pull (90% of Spend) · Step 3: Establish Baselines from the Pareto Set · Step 4: Diagnose Each Pareto Ad · Step 5: Generate Recommendations · Performance Summary · Recommendations · Minimum required data (by source) · Tool hints

Top-down ad-level audit using the Pareto principle. Identify the ads driving 90% of spend, classify each as keep / pause / test, and produce account-level strategic recommendations.

## When to use this skill

- "Audit my account"
- "Which ads should I pause?"
- "What's working in this campaign?"
- Anytime you need a portfolio view before drilling into creative

## Step 1: Confirm Account Type & PCM

Use the output of **Conversion Metric Focus** (Skill 2). If it hasn't been run yet, run it first. If the account has mixed conversion types, group ad sets by event type and analyze each group with its own PCM.

### Pre-Audit Check: COMPLETE_REGISTRATION on Purchase Objective

If you see any ad set with campaign objective `OUTCOME_SALES` AND optimization event `COMPLETE_REGISTRATION`, apply the **3rd-party-tracker check** (COMPLETE_REGISTRATION section in SKILL.md) before any recommendation on that ad set.

## Step 2: Pareto Pull (90% of Spend)

Pull ad-level insights for the last 30 days. Filter to **active ads** (effective status = ACTIVE) with impressions > 0, sorted by spend desc. If the result set is paginated, **fetch all pages before analyzing** — analyzing only the first page produces wrong totals and wrong CPAs.

Required fields per ad:

- Ad name, ad ID, ad set ID/name
- Spend, impressions, CPM, CTR, clicks
- Actions (for purchase / lead counts)
- Action values (for revenue)
- Purchase ROAS

Then calculate **cumulative spend %** for each ad in spend-descending order. Keep the ads where cumulative % ≤ 90% — these are your Pareto ads. Focus the analysis on them.

## Step 3: Establish Baselines from the Pareto Set

| Baseline | Calculation |
|---|---|
| Pareto avg CPM | mean CPM across Pareto ads |
| Pareto avg CTR | mean CTR across Pareto ads |
| Pareto avg PCM | mean ROAS (ecommerce) or mean CPL / CPR (lead gen / custom) |
| Account avg Hold Rate | from a 90-day account-level pull (only needed for video analysis — see Skill 6) |

These become the comparison points for every individual-ad assessment.

## Step 4: Diagnose Each Pareto Ad

Apply the variance benchmarks (Performance Benchmarks table in `references/metrics.md`):

**High CPM (≥ 30% above Pareto avg) + Low PCM (≥ 30% below avg)**

- Diagnosis: expensive audience, not converting
- Recommendation: pause this ad OR test different targeting

**Low CTR (≥ 30% below Pareto avg) + Low PCM**

- Diagnosis: ad isn't resonating with the audience
- Action: first check comments for negative sentiment
- If comments are fine → recommend copy / creative variations with stronger CTA

**Good metrics but declining trend**

- Diagnosis: likely creative fatigue (check the fatigue signal — frequency rising + CTR falling over 14+ days)
- Recommendation: new creative variations, NOT budget changes

**Good metrics, stable trend**

- Diagnosis: working as intended
- Recommendation: create variations (copy / angle / format / hook) to extend the winning pattern

## Step 5: Generate Recommendations

**Mandatory:** after analysis, produce specific, actionable recommendations.

### Per-Ad Recommendations

For each Pareto ad:

- **What** — specific action (pause, scale, create variation, change targeting)
- **Why** — metrics-based justification (e.g., *"CPM 40% above Pareto avg with 0.3× ROAS"*)
- **How** — concrete next steps for the user to apply in Ads Manager

### Strategic Recommendations

Summarize the top 3–5 account-level moves:

1. **Budget direction** — which campaigns or ad sets to scale (within the 20% cap) vs which to pull back. Respect the budget-reallocation guardrails: only campaign / ad set budgets, never ad-level or per-placement.
2. **Creative strategy** — what's working, what to test next.
3. **Targeting adjustments** — if CPM issues are widespread.
4. **Structure changes** — campaign / ad set consolidation if needed.

### Output Format

```
## Performance Summary

| Ad | Format | Spend | CPM | CTR | ROAS/CPA | Status |
|----|--------|-------|-----|-----|----------|--------|
| [Name] | Image | $X | $X | X% | X | [Scale/Pause/Test] |

Benchmarks (Pareto avg): CPM: $X | CTR: X% | ROAS: X

## Recommendations

### Per-Ad Actions
1. **[Ad Name]**: [Action] — [Justification]
2. **[Ad Name]**: [Action] — [Justification]

### Strategic Recommendations
1. [Plain-language recommendation with metrics basis]
2. [Plain-language recommendation with metrics basis]
3. [Plain-language recommendation with metrics basis]
```

**If creative-level depth is needed** (video hook/hold, image diagnostics, ad copy evaluation), continue to **Skill 6: Creative Analysis**.

## Minimum required data (by source)

| Source | What you need |
|---|---|
| MCP | Ad-level insights over the last 30 days for **active ads with impressions > 0**, sorted by spend desc. Required fields: ad name, ad ID, ad set name/ID, spend, impressions, CPM, CTR, clicks, `actions` (for purchase/lead counts), `action_values` (for revenue), `purchase_roas`. **Paginate all pages before analyzing** — analyzing only page 1 gives wrong totals and CPAs. |
| CSV | Ad-level view export filtered to active ads, last 30 days. Must include: Ad Name, Spend, Impressions, CPM, CTR, Link Clicks, Purchases, Purchases Conversion Value, Purchase ROAS. For lead-gen accounts, swap Purchases / ROAS for Leads / CPL. |
| Screenshot / copy-paste | Workable only if the screenshot already shows the full Pareto set (top N ads by spend) with all required columns. |

## Tool hints

The Pareto cut (top 90% of spend) is the entry point — fetching only top-10 by spend will miss ads that round out the 90% threshold. With MCP, request **all active ads sorted by spend desc** and paginate fully. With CSV, ensure the export was filtered to ACTIVE ads only (paused / archived ads inflate the totals). **Run the COMPLETE_REGISTRATION 3rd-party tracker check from Skill 5 Step 1 before any pause / scale recommendation** — this is the highest-stakes safety check in the framework.
