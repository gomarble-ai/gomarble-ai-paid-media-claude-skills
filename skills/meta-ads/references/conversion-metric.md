# Skill 2: Conversion Metric Focus

Determine account type and set the **Primary Conversion Metric (PCM)** that all subsequent analysis will use. **Run this second on any audit, immediately after the Health Check.**

## When to use this skill

- Once per account, at the start of analysis
- Whenever account-level KPIs are ambiguous
- When new campaigns are added that may use a different conversion event

## Data to gather

For each active campaign in the account:

- Campaign objective (e.g., OUTCOME_SALES, OUTCOME_LEADS, OUTCOME_TRAFFIC)
- The optimization event at the ad set level — the actual `custom_event_type` of the promoted object. **Never infer from campaign or ad set names.**
- The list of conversion actions used

## Decision Logic

For each live campaign:

```
IF majority conversion event = PURCHASE         → ECOMMERCE
IF majority conversion event = LEAD             → LEAD GENERATION
IF custom conversion event (OTHER)              → CUSTOM CONVERSION (treat standalone; do not group with other types)
```

**Mixed accounts:** group ad sets by their event type and apply each group's PCM separately. Do not mix conversion types into one aggregate.

## Set PCM by Account Type

### Ecommerce

| Metric | Type | Source |
|---|---|---|
| Purchase ROAS | Primary (PCM) | `purchase_roas` field, deduplicated per the Purchase De-Duplication rule |
| Cost per Purchase | Secondary | spend / purchase count |
| Conversion Rate | Secondary | purchases / clicks |
| Revenue | Secondary | conversion value for purchase events |

### Lead Generation

| Metric | Type | Source |
|---|---|---|
| Cost per Lead | Primary (PCM) | spend / lead count |
| Conversion Rate | Secondary | leads / clicks |

### Custom Conversion

| Metric | Type | Source |
|---|---|---|
| Cost per Result | Primary (PCM) | spend / count of the specific custom event |
| Conversion Rate | Secondary | custom events / clicks |

> **Note:** For custom conversion campaigns, metrics are scoped to that specific conversion event only. No other conversion events should be included in the analysis for that campaign.

## Output

Set internally:

- `account_type`: `ecommerce`, `lead_gen`, or `custom_conversion`
- `primary_metric`: `purchase_roas`, `cost_per_lead`, or `cost_per_result_<custom_event>`

These flow into every later skill.

## Minimum required data (by source)

| Source | What you need |
|---|---|
| MCP | Per active campaign: campaign objective + per-ad-set `promoted_object.custom_event_type`. Directly available. |
| CSV | "Campaign Objective" + "Performance Goal" / "Optimization Event" columns (often not in default exports — must be enabled). If unavailable, **ask the user to confirm the conversion event for each campaign** before proceeding. |
| Screenshot / copy-paste | Ask user to confirm directly per campaign. |

## Tool hints

The most reliable signal is `promoted_object.custom_event_type` on the ad set object. Campaign / ad set *names* lie often — never infer the conversion event from a name. If using MCP, fetch the ad set object explicitly. If using CSV without the optimization-event column, this entire skill blocks until the user confirms.
