# Skill 6: Creative Analysis

**Contents:** When to use this skill · Inputs You Need · Step 1: Format-Agnostic Diagnostics (Apply to Every Ad) · Step 2: Video-Specific Diagnostic Scenarios · Step 3: Format-Specific Rules · Step 4: Pattern Recognition Across Top Performers · Step 5: Variation Strategy · Decision Tree Summary (Video) · Output Format · Minimum required data (by source) · Tool hints

Deep creative analysis with diagnostic scenarios for video ads, plus image and catalog format rules. Run **after** Performance Analysis when more depth is needed on specific Pareto ads.

## When to use this skill

- Video hook / hold metrics are off
- "Why isn't this creative working?"
- Need to plan variations of winners
- The user wants to understand a specific ad in depth

## Inputs You Need

Before applying this skill:

- Ad-level video metrics (video plays, ThruPlays, 3-second views — using the **video_view action** inside the actions array, NOT `video_p25_watched_actions`)
- Account-level Hold Rate baseline from a 90-day account-level pull
- The Pareto set of ads (from Skill 5)
- The actual creative content for each Pareto ad — for video, the visuals and audio; for image, the visual; for all formats, the copy (headline, primary text, CTA). The user can share screenshots, video files, or descriptions.

## Step 1: Format-Agnostic Diagnostics (Apply to Every Ad)

| Profile | Diagnosis | Recommendation |
|---|---|---|
| High CPM (≥ 30% above Pareto avg) + Low PCM (≥ 30% below) | Expensive audience, not converting | Pause ad |
| Low CTR (≥ 30% below Pareto avg) + Low PCM | Not resonating | Check comments first; if fine, test variations with stronger CTA |
| Good metrics (within 20% of avg + PCM above avg) | Working | Create variations (copy / angle / format) |

## Step 2: Video-Specific Diagnostic Scenarios

Apply Hook Rate / Hold Rate / CTR benchmarks (from `references/metrics.md`) to classify each Pareto video ad.

### Scenario 1: Good Hook, Poor Hold

| Metric | Status | Range |
|---|---|---|
| Hook Rate | Strong | ≥ 40% |
| Hold Rate | Poor | < Account Avg |
| CTR | Average | 0.65 – 1.24% |
| PCM | Poor | Below target |

**Interpretation:** Hook is stopping scroll, but people drop off after 3 seconds. They're missing key information.

**Recommendations:**

1. KEEP the intro / hook (it's working)
2. CHANGE seconds 3+ completely

Tactics:

- Move value prop order around
- Show product sooner
- Get to "how this helps you" faster
- Avoid stagnant clips — use variety
- Quick B-roll + testimonial + selfie style mix
- Keep value props concise (not 10 seconds each)
- Ensure seconds 3+ relate back to the hook's problem / promise

### Scenario 2: Average Everything

| Metric | Status | Range |
|---|---|---|
| Hook Rate | Average | 26 – 39% |
| Hold Rate | Average | ≈ Account Avg |
| CTR | Average | 0.65 – 1.24% |
| PCM | Poor | Below target |

**Interpretation:** Nothing stands out. Room for improvement everywhere. Priority 1 — improve the hook first. If they don't stop, they won't purchase.

**Recommendations:**

1. **Priority:** rebuild the hook / intro first. Inspect the creative for:
   - Is the visual relevant to the target audience?
   - Is the intro speaking to the wrong customer?
   - Can it be more direct?
   - Can it relate to the customer better?
2. THEN: build the remaining clips to improve hold rate.

**Warning:** don't go click-baity. The hook must be relevant to the actual customer.

### Scenario 3: Poor Hook

| Metric | Status | Range |
|---|---|---|
| Hook Rate | Poor | < 25% |
| Hold Rate | Any | — |
| CTR | Any | — |
| PCM | Poor | Below target |

**Interpretation:** People aren't even stopping to watch. Nothing else matters until the hook is fixed.

**Recommendations:**

1. Watch the actual video
2. Document the current hook (visual + audio)
3. Compare to hooks in top-performing ads (review those too)
4. Rebuild the hook based on what works

Hook elements to test:

- Different visual opening
- Different text overlay
- Different audio hook
- Problem statement vs benefit statement
- Question vs statement

### Scenario 4: Great Hook + Great Hold, Poor CTR

| Metric | Status | Range |
|---|---|---|
| Hook Rate | Good | ≥ 40% |
| Hold Rate | Good | > Account Avg + 25% |
| CTR | Poor | < 0.65% |
| PCM | Poor | Below target |

**Interpretation:** People are watching the whole video but not clicking. CTA is weak or unclear.

**Recommendations:**

1. Check comments for negative sentiment
2. If comments are fine → strengthen the CTA

CTA improvements:

- More prominent visual CTA
- Clearer verbal CTA
- Urgency / scarcity element
- Better landing-page alignment

## Step 3: Format-Specific Rules

### Single Image

- High CPM (30%+ above Pareto avg) + Low PCM → recommend pausing the ad
- Low CTR (30%+ below avg) + Low PCM → check comments; if fine, test stronger-CTA variations
- Good metrics → create variations (copy, angle, or format)

### Single Video

Apply Scenarios 1–4 based on Hook / Hold / CTR profile, plus:

- High CPM + Low PCM → pause
- Low CTR + Low PCM → check comments, then test stronger-CTA variations

### Advantage+ Catalog Ads

**Limitation:** Meta does NOT provide conversion data per product ID. Workaround:

- Build a Pareto of product IDs by spend
- Use spend + CTR as a proxy — higher spend + higher CTR = likely better performer

- High CPM + Low PCM → pause ad, test a different product set. Also check: if 1–2 product IDs are pushing CPM up, recommend removing those products from the set.
- Low CTR + Low PCM → identify low-CTR products from spend/impressions data, recommend removing them from the set.

## Step 4: Pattern Recognition Across Top Performers

Among the top Pareto ads, review the creative content of each and identify shared patterns:

- Common angle patterns (which selling points repeat across winners)
- Common format patterns (image vs video vs carousel)
- Common hook patterns (videos — what stops the scroll)
- Common copy patterns (tone, length, structure)

Use winning patterns to guide new variation creation.

## Step 5: Variation Strategy

### When an ad is performing well

Create variations in this order:

1. Copy variations (same angle, different words)
2. Angle variations (different selling point)
3. Format variations (same message, different format)
4. Hook variations (videos — same body, different hooks)

### When an ad is performing poorly

| Issue | Action |
|---|---|
| Hook Rate poor | Rebuild hook using winning hooks |
| Hook good, Hold poor | Rebuild middle section |
| Hook good, Hold good, CTR poor | Strengthen CTA |
| All metrics poor | Test a completely new approach |

## Decision Tree Summary (Video)

```
START
  │
  ├─ Hook Rate < 25%?
  │    └─ YES → Rebuild hook completely (Scenario 3)
  │
  ├─ Hook Rate 26–39%?
  │    └─ YES → Improve hook first, then content (Scenario 2)
  │
  └─ Hook Rate ≥ 40%?
       │
       ├─ Hold Rate < Account Avg?
       │    └─ YES → Rebuild middle section (Scenario 1)
       │
       └─ Hold Rate good but CTR < 0.65%?
            └─ YES → Strengthen CTA (Scenario 4)
```

## Output Format

```
### Creative Analysis: [Ad Name]

Creative Profile:
| Element     | Analysis      |
|-------------|---------------|
| Angle       | [description] |
| Persona     | [description] |
| Format      | [description] |
| Visual Hook | [description / N/A for image] |
| Audio Hook  | [description / N/A for image] |
| CTA         | [description] |

Metric Diagnosis:
| Metric    | Value | Benchmark         | Status        |
|-----------|-------|-------------------|---------------|
| Hook Rate | X%    | Good ≥ 40%        | [Good/Avg/Poor] |
| Hold Rate | X%    | Acct Avg: Y%      | [Good/Avg/Poor] |
| CTR       | X%    | Good ≥ 1.25%      | [Good/Avg/Poor] |
| ROAS/CPA  | X     | [Target]          | [Good/Poor]   |

Benchmarks used:
- Account avg Hold Rate (90d): X%
- Pareto avg CPM: $X
- Pareto avg CTR: X%

Scenario Match: [1 / 2 / 3 / 4 / N/A for non-video]
Root Cause: [description]

Top Performers — Common Patterns:
- Angle: [pattern]
- Format: [pattern]
- Hook: [pattern, videos]
- Copy: [pattern]

Recommendations (plain language, for the user to apply in Ads Manager):
1. [Specific recommendation with metrics justification]
2. [Specific recommendation with metrics justification]
3. [Specific recommendation with metrics justification]
```

## Minimum required data (by source)

| Source | What you need |
|---|---|
| MCP | Ad-level video metrics: `video_play_actions`, `actions` (containing `video_view` = 3-second), ThruPlay events. Account-level 90-day pull for Hold Rate baseline. Creative content via creative endpoint (e.g. `facebook_get_ad_creative_details`). |
| CSV | Ad-level export with "Video Plays", "3-Second Video Plays", and "ThruPlays" columns enabled. Plus a separate 90-day account-level aggregate pull for Hold Rate baseline. **Creative content (the actual video / image / copy) is NEVER in a CSV — must be shared separately.** |
| Screenshot / copy-paste | Works for spot-checking a single ad's video metrics if visible. Creative content can come from a video file upload or a description. |

## Tool hints

This skill needs **two kinds of data**: numeric (Hook/Hold/CTR) and qualitative (the actual creative). Numeric works fine from any source as long as video columns are enabled. Qualitative requires the user to share files or text — no export captures creative content. Build a checklist before starting: numeric metrics ✓, 90-day Hold Rate baseline ✓, the actual ad creative ✓. Without all three, the skill outputs framework, not diagnosis.
