---
name: meta-ads
description: Audits and optimizes Meta Ads (Facebook + Instagram) accounts at senior-media-buyer depth. Use when the user asks about Meta Ads performance, campaign optimization, creative fatigue, ad set analysis, video creative diagnosis, pixel tracking issues, or wants a Meta Ads audit. Covers EMQ Score health check, conversion metric mapping (ROAS vs CPL vs custom), campaign structure detection, ad set bid-limit and audience-split decision rules, ad-level performance analysis, and Hook Rate / Hold Rate video diagnostic scenarios. Read-and-recommend only — produces analysis the user applies manually in Meta Ads Manager.
---

# Meta Ads Optimization Skills

A consolidated set of skills for analyzing and optimizing Meta Ads (Facebook + Instagram) accounts. These skills are **framework-agnostic** — the analytical logic (Pareto, Hook/Hold scenarios, decision matrices, guardrails) applies regardless of where the data comes from.

The skills define **what to know, what data to look for, how to interpret it, and how to recommend action**. They do not depend on any specific tool integration.

> **Read-and-recommend only.** These skills never make changes to the user's Meta Ads account. Claude reads data and produces recommendations in plain language; the user applies the recommended changes themselves in Meta Ads Manager.

---

## Data Sources Are Not All Equal

Data can come from four kinds of sources, but they have **very different completeness**. Some skill rules silently break on weaker sources. Always identify the source first and consult the **Data Source Compatibility Matrix** in `references/data-sources.md` before applying any rule.

| Priority | Source | Notes |
|---|---|---|
| 1 (preferred) | A connected MCP server exposing Meta Ads data (e.g. GoMarble, Meta official) | Returns raw API fields, action arrays, full targeting, breakdowns. All rules work. |
| 2 | A CSV/Excel export from Ads Manager | Most rules work, but a few are inert — see compatibility matrix. Several signals require *separate* exports (breakdowns, video metrics, ad-level vs ad-set-level views). |
| 3 (narrow questions only) | Screenshots of report tables | Use only for spot questions on metrics that are visibly captured in the screenshot. Skip deep analysis. |
| 4 (last resort) | Direct copy-paste of metric values | Treat as user-asserted; ask for the underlying export when stakes are real. |

---

## How to Use These Skills

1. **Identify the user's intent** — are they asking for an audit, a performance review, a creative deep-dive, or a targeted question? Use the routing table below, then read the reference files it names.
2. **Run the Data Inventory step (Step 0 below)** — confirm what source is being used and what's actually available before invoking any skill.
3. **Gather the required data** — ask the user to share the data the skill needs in their preferred source. The "Minimum required data" section of each skill's reference file lists what's needed.
4. **Apply the analytical framework** — classify, diagnose, decide based on the rules in the relevant skill.
5. **Always check guardrails** before recommending any action.
6. **Output recommendations** in the structured format defined per skill.

If required data is missing or unverifiable, say so explicitly and ask the user for it. **Never fabricate metrics or invent thresholds.**

**When GoMarble MCP is connected:** use its data tools to pull the data, but this skill is the methodology — don't also call GoMarble's `load_skill` tool for the same workflow, since it loads an overlapping framework. The skill stays read-and-recommend: don't call GoMarble's `*_propose_*` tools as part of the analysis. If the user then explicitly asks to make a change, treat that as a separate request.

**Always work from current data** — campaigns change frequently (budget edits, paused ads, new creatives). If the user shared data more than a day or two ago, ask for a fresh pull before making recommendations.

---

## Step 0: Data Inventory (Mandatory Before Any Skill)

Run this once at the start of every analysis. It takes one short turn and prevents wasted effort.

1. **Identify the data source** — MCP / CSV / screenshot / copy-paste. If MCP is connected, use it. If the user attached a file, inspect its columns/fields before asking for more.
2. **State what's available and what's missing** for the requested skill, based on the Data Source Compatibility Matrix in `references/data-sources.md`.
3. **For each missing signal, decide:**
   - **Blocking** — cannot proceed without it; ask user to fetch.
   - **Downgrade** — can proceed with caveats; flag as low-confidence in the output.
   - **Skip** — rule doesn't apply to this source (e.g. Purchase De-Duplication on CSV); note it and move on.
4. **Confirm the date range** in the data matches what the skill expects (typically 30 days; 7d for ad set analysis; 60–90d for trend or Hold Rate baseline).

Output one short paragraph before applying the skill. Example:
> *"Using your GoMarble MCP. I have ad-level insights with `actions` and `purchase_roas` for the last 30 days — sufficient for Performance Analysis (Skill 5). The EMQ check (Skill 1) requires you to look in Events Manager directly; I'll flag it as a manual step."*

---

## Routing — Which Skill to Use

The six skills live in `references/`. Read the file(s) for the matched request **in full** before applying their rules — they hold the step-by-step logic, thresholds, and output formats.

| User asks about | Use Skill | Read |
|---|---|---|
| "Audit my account" / full optimization request | Run **Initial Health Check** → **Conversion Metric Focus** → **Performance Analysis** → **Creative Analysis** in that order | `references/health-check.md`, `references/conversion-metric.md`, `references/performance-analysis.md`, `references/creative-analysis.md` |
| Pixel / tracking setup, audience segments setup | **Initial Health Check** (Skill 1) | `references/health-check.md` |
| "What's my account type?" / which KPI to use | **Conversion Metric Focus** (Skill 2) | `references/conversion-metric.md` |
| Campaign structure, primary vs testing, bid splits, audience splits | **Campaign Structure Analysis** (Skill 3) | `references/campaign-structure.md` |
| Ad set targeting, budget utilization, audience comparison | **Ad Set Analysis** (Skill 4) — run after Skill 3 | `references/campaign-structure.md`, `references/ad-set-analysis.md` |
| Top performers, Pareto analysis, which ads to keep/pause | **Performance Analysis** (Skill 5) | `references/performance-analysis.md` |
| Hook rate, hold rate, video diagnostics, why creative isn't working | **Creative Analysis** (Skill 6) — uses the Pareto set from Skill 5 | `references/performance-analysis.md`, `references/creative-analysis.md` |
| Change requests (pause campaign, increase budget, change CTA, etc.) | Apply the relevant analysis skill first, then **recommend** the change in plain language with rationale. Claude does not execute changes on the user's ad account — the user applies recommendations manually in Ads Manager. | The relevant skill's file + `references/edge-cases.md` |

If the user's intent is ambiguous, ask which to focus on first.

**Shared references — read when the situation applies:**

| File | Read when |
|---|---|
| `references/metrics.md` | Computing or benchmarking any metric: definitions, Hook/Hold formulas, account type → PCM, performance benchmarks, significance floors, fatigue signals. Needed for Skills 2, 4, 5, and 6. |
| `references/data-sources.md` | Step 0 when the source is a CSV, screenshot, or pasted values (column translation), or when planning which fields to pull over MCP. |
| `references/depth-of-analysis.md` | Audits, performance reviews, optimization requests, strategy questions. Skip for simple fetches and single-metric lookups. |
| `references/edge-cases.md` | Data is missing or stale, the account mixes conversion types, account type is ambiguous, a needed metric isn't exposed, or the user asks for a change. |

The guardrails and critical checks below stay in this file because they apply to every recommendation.

---

## Universal Guardrails — Apply Before Every Recommendation

**Read these before generating any recommendation.**

### Budget Reallocation Prohibition

You **cannot** allocate, shift, increase, reduce, or scale budget for: individual ads (only campaigns and ad sets have budgets), placements (Meta controls distribution), demographics (age, gender, location breakdowns), user segments (new, existing, engaged).

**Before writing any recommendation, ask:** Does it imply moving money between ads, placements, demographics, or segments? If yes → rewrite using the valid controls below.

**Valid budget controls (only three):**

1. Campaign budget (CBO) or ad set budget (ABO)
2. Bid caps / cost caps
3. Turning ads / ad sets on or off

If a recommendation does not map to one of these three controls, it is not actionable.

**Mandatory rewrites:**

- ❌ "Reallocate $X from [ad A] to [ad B]"
- ✅ "Pause [ad A]. Increase the campaign/ad set budget by 15–20% to give [ad B] more spend opportunity."

- ❌ "Allocate more to [placement / demographic / segment]"
- ✅ "Create a new ad set targeting [dimension] with its own budget, OR exclude underperforming [dimension] via ad set placement settings."

**Rule:** Breakdowns (age, gender, placement, device, region, user segment) show how Meta distributed YOUR budget. They are not levers the user controls. The only way to influence them is creating new ad sets with specific targeting or placement selections.

### Metric Selection by Conversion Type

- **Ecommerce** (purchases / revenue): Use ROAS, revenue, AOV, cost per purchase. Never use ROAS for leadgen.
- **Lead gen** (form submits, leads): Use CPL, cost per qualified lead. Never use ROAS unless offline revenue is mapped.
- **App** (installs, in-app events): Use CPI, cost per activation. Never use ROAS unless in-app revenue tracking is confirmed.
- **Custom conversion**: Use cost per result for that specific event. Do not mix in other conversion types.
- **Unclear**: Ask the user. Do not assume.

### User Segment Targeting Notes

Segments (New Audience, Existing Customers, Engaged Audience) are Meta internal classifications. **They cannot be targeted without custom audiences.**

- Before recommending segmentation, ask: *"Do you have a customer custom audience already built?"*
- If yes → suggest exclusions or separate campaigns using custom audience targeting
- If no → suggest building custom audiences first

### Top Performer Protection (CRITICAL)

**Never recommend pausing the top-converting ad in an ad set.** If Meta's algorithm allocates 60–80% of an ad set's budget to one ad and that ad produces the majority of conversions, that's Meta's optimization working correctly — not a problem.

**Pause decision matrix:**

| Condition | Action |
|---|---|
| Ad has highest conversion volume in ad set | **KEEP** — regardless of budget share |
| Ad has 0 conversions AND spend > 2× ad set CPA target | PAUSE |
| Ad has conversions but CPA > 3× ad set average AND ≥ 3 conversions (statistically significant) | PAUSE |
| Ad has 1–2 conversions with high CPA | WATCH — insufficient data, do not pause yet |
| Ad is < 7 days old | WATCH — let it exit learning phase |

**Self-check before any pause recommendation:** *"Am I about to recommend pausing the ad that drives the most conversions in this ad set?"* If yes → DO NOT recommend pausing. Instead recommend testing new creatives alongside it.

### Methodology Consistency

Once you establish a methodology for evaluating performance in a conversation, do NOT change it unless the user explicitly asks. Changing criteria mid-analysis destroys trust. If you realize your methodology was wrong, say so clearly, explain what you're changing and why, and apply the new methodology consistently from that point.

### STOP Rules

**Pre-check before any recommendation:** Can the user point to the exact Ads Manager UI field that this change maps to? If no → do not recommend.

- No ad-level budget moves
- No demographic or placement budget allocation
- No frequency caps for conversion objectives (Sales, Leads, App install)
- No scaling individual ads (only campaign / ad set level)
- No scaling > 20% at once
- Do not pause ads or ad sets younger than 7 days without enough signals
- Do not increase budget on entities below ROAS/CPL/CPA targets — diagnose first
- Do not call something "scalable" with < 10% revenue share of total account or statistically weak conversion volume
- Minimum signal: 3–5 conversions per ad set per week before performance judgments
- Avoid suggestions that restart the learning phase unless absolutely required
- Do not rely on the first 24–48 hours of data as reliable

### Required Diagnostics Before Action

Before any scale / pause / duplicate / structural recommendation:

1. **User segments**: New vs Existing vs Engaged distribution
2. **Delivery metrics**: CPM, CTR, Reach, Frequency (with spend context)
   - High frequency alone ≠ fatigue
   - Frequency rising + CTR falling over 14+ days = creative fatigue
3. **Engagement relevance**: offer-aligned comments vs spam / backlash
4. **Attribution windows**: 1-day click vs 7-day click vs incremental, if platform / external data mismatch
5. **Confirm results not dominated by warm / small pools** before scaling

### Scaling Guardrails

When recommending a budget increase:

- Only campaign or ad set budget fields (never ad-level)
- Max increase: **20% at once**
- Require before scaling: performance target hit, ad set revenue share ≥ 10% of account, not dominated by 80%+ warm/customer pocket
- If data is noisy or contradictory → say **insufficient data** and shift to a structured testing recommendation instead
- All scaling recommendations must include: deterioration-risk warning + review window + spend cap

### Change-Recommendation Safety Language

When recommending changes the user will apply manually, always include these warnings where relevant:

- **Budget increase > 100%**: warn this is a major increase and ask the user to confirm intent
- **Budget decrease > 50%**: warn this significantly reduces reach and performance
- **Daily vs lifetime budget**: always distinguish which one you're talking about
- **Pausing**: traffic and spending stop immediately
- **Deletion**: permanent, cannot be undone — require explicit confirmation
- **Archiving**: reversible — can be unarchived back to PAUSED
- **Bid strategy change**: resets the learning phase — always warn
- **Targeting change**: if non-trivial, may reset learning phase

---

## Critical Checks — Apply Whenever They Trigger

These two rules from the metric glossary can silently corrupt an analysis or kill a working campaign, so they are always loaded.

### Purchase De-Duplication (CRITICAL — API/MCP only)

**This rule applies only when the source is an MCP / API that returns the raw `actions` array.** If the source is a CSV export, the "Purchases" column has already been deduplicated by Meta — **skip this rule entirely and use the column directly.**

When working with raw API data: Meta returns overlapping purchase action types in the `actions` array: `omni_purchase`, `purchase`, `offsite_conversion.fb_pixel_purchase`, `onsite_web_purchase`, `web_in_store_purchase`, `app_custom_event.fb_mobile_purchase`.

**Rule:** Use ONLY ONE. Check `omni_purchase` first; if absent, fall back to `purchase`. **Never sum multiple types** — this double-counts revenue and inflates ROAS.

**Source check before applying:**
- MCP returning an `actions` array → apply the rule.
- CSV with a "Purchases" column → skip the rule; the column is already deduplicated.
- Screenshot showing a "Purchases" number → skip the rule; trust the figure but flag the source.

### Special Case: COMPLETE_REGISTRATION on PURCHASE Objective (Cross-Source Safety Check)

If an ad set has campaign objective `OUTCOME_SALES` (or legacy `CONVERSIONS` / `PRODUCT_CATALOG_SALES`) AND the optimization event is `COMPLETE_REGISTRATION`, this is **almost always a 3rd-party purchase tracker** (Profitmetrics, Cosmise, Triple Whale, Northbeam) posting purchase events through Meta's CompleteRegistration endpoint — **not a misconfiguration**.

Especially common on:
- Nordic-currency accounts (DKK / SEK / NOK / EUR)
- Shopify + Profitmetrics stacks

**This is the highest-stakes safety check in the skill — getting it wrong can kill a working campaign.**

#### Source-aware detection

| Source | How to detect |
|---|---|
| MCP / API | Read `campaign.objective` + `ad_set.promoted_object.custom_event_type` directly. If the pair matches the trigger, apply the check below. |
| CSV with "Campaign Objective" + "Performance Goal" / "Optimization Goal" columns | Match by column values. If columns are missing, fall through to the manual check. |
| CSV without those columns, screenshot, or copy-paste | **Cannot detect automatically.** Use the proactive question below before any pause / scale / budget-cut recommendation on Nordic-currency or Shopify accounts. |

#### Proactive question (use whenever auto-detection isn't possible OR the account profile fits)

> *"Before I make recommendations on this account: do you use a 3rd-party purchase tracker like Profitmetrics, Triple Whale, Northbeam, or Cosmise? If yes, the conversion event reported as 'Registrations' or `COMPLETE_REGISTRATION` is real purchase volume and the campaign is correctly configured — I should treat it as purchase data."*

Ask this **once per account / conversation**, store the answer, and apply it to all subsequent recommendations.

#### Action rules (apply after detection or confirmation)

Before any optimization recommendation on such ad sets:

1. State the ambiguity in your response, naming the 3rd-party tracker explicitly.
2. **Do NOT** recommend any of the following without explicit user confirmation first:
   - "Change the optimization event to PURCHASE"
   - "Verify and switch the optimization goal"
   - Pause / archive / delete the ad set or campaign
   - Reduce budget by more than 20%

Only after confirmation may you treat the events as registrations (and recommend an optimization-event change) OR as real purchases (apply ROAS / CPA against revenue).
