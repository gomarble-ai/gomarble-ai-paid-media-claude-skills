# Skill 1: Initial Health Check

Validate account setup before any optimization work. **Run this first on any audit.** If checks fail, fixing setup is the top priority — optimization on a broken setup wastes effort.

## When to use this skill

- First step of any account audit
- Before recommending any structural change
- When CPA or ROAS suddenly degrades and tracking issues are plausible

## Step 1: Event Match Quality (EMQ) Score Check

EMQ score is **not directly available via standard insights APIs.** The user must check it manually in Events Manager.

**What to do:**

1. First determine the primary conversion event (from the ad set's optimization goal — covered in Skill 2).
2. Ask the user to manually check: **Events Manager → Data Sources → [Pixel] → Event Match Quality** for that event.
3. Apply the threshold:

| EMQ Score | Status | Action |
|---|---|---|
| ≥ 8.5 | Good | Proceed with analysis |
| < 8.5 | ALERT | Stop and notify the user before optimizing |

**Alert wording when EMQ < 8.5:**

> ⚠️ **CRITICAL:** Your EMQ Score for [Purchase / Lead] is below 8.5.
>
> This means your Pixel is not set up correctly. Likely consequences:
> - Lower conversion rate than possible
> - Higher cost per result than necessary
>
> **Recommendation:** Reach out to a technical expert and fix this as TOP PRIORITY before any other optimization work.

## Step 2: Audience Segments Configuration Check

Audience segment breakdown (New / Engaged / Existing) is **available via insights breakdowns**, but the underlying engaged/existing audience setup is managed in Audience Manager and isn't directly readable via standard APIs.

**What to do:**

1. Pull account-level insights for the last 30 days, broken down by **user segment** (the breakdown that splits New / Engaged / Existing).
2. If the breakdown returns empty or is missing segments, alert the user:

> ⚠️ **Setup needed:** Audience Segments are not configured.
>
> Why this matters: you can see spend breakdown between existing customers and new audience, at campaign / ad set / ad level. Without this, you can't tell where money is actually going.
>
> Note: this does NOT affect targeting — only improves reporting.
>
> Setup guide: Facebook Business Help → Audience Segments configuration.

## Step 3: Decide whether to proceed

| Result | Action |
|---|---|
| EMQ ≥ 8.5 AND segments configured | Proceed to Conversion Metric Focus |
| EMQ < 8.5 | Recommend fixing pixel before any optimization |
| Segments not configured | Flag for setup; can proceed with limited reporting |

## Minimum required data (by source)

| Source | What you need |
|---|---|
| MCP | Account-level insights for last 30 days with `breakdowns=['user_segment_key']` to confirm segments are configured. EMQ requires manual user check. |
| CSV | A breakdown export by user segment (if available). EMQ requires manual user check. |
| Screenshot / copy-paste | Not recommended for this skill — too many missing pieces. Ask for at minimum a screenshot of Events Manager → EMQ for the primary event. |

## Tool hints

EMQ Score is **never** in standard insights data — it always requires a manual check in Events Manager → Data Sources → [Pixel]. Audience Segment configuration is observable from any source via the user-segment breakdown; if the breakdown returns empty, segments are unset.
