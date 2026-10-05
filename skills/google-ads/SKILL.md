---
name: google-ads
description: Audits and optimizes Google Ads accounts at senior-media-buyer depth. Use when the user asks about Google Ads performance, campaign optimization, search terms, keywords, Shopping campaigns, Performance Max (PMax), keyword research, wasted spend, or wants a Google Ads audit. Covers Q1-Q5 search term classification, auction pressure diagnosis (rank vs budget), Shopping SKU classification (KILL/DOWNGRADE/PROMOTE), PMax maturity gates and asset performance labels, PMax-vs-Search ROAS comparison, brand cannibalization detection, and buyer-intent keyword validation. Read-and-recommend only — produces analysis the user applies manually in the Google Ads UI.
---

# Google Ads Optimization Skills

A consolidated set of skills for analyzing and optimizing Google Ads accounts. These skills are **framework-agnostic** — the analytical logic (Q1–Q5 query tiers, auction-pressure diagnosis, PMax maturity gates, item classification) applies regardless of where the data comes from.

The skills define **what to know, what data to look for, how to interpret it, and how to recommend action**. They do not depend on any specific tool integration.

> **Read-and-recommend only.** These skills never make changes to the user's Google Ads account. Claude reads data and produces recommendations in plain language; the user applies the recommended changes themselves in the Google Ads UI.

---

## Data Sources Are Not All Equal

Data can come from four kinds of sources, but they have **very different completeness**. Some skill rules silently break on weaker sources — most notably, PMax asset performance labels and PMax search term insights are NOT in default Google Ads CSV exports. Always identify the source first and consult the **Data Source Compatibility Matrix** in `references/data-sources.md` before applying any rule.

| Priority | Source | Notes |
|---|---|---|
| 1 (preferred) | A connected MCP server exposing Google Ads data (e.g. GoMarble) with GAQL access | All rules work. Query each Google Ads resource via GAQL. |
| 2 | CSV / Excel exports from Google Ads UI | Most basic rules work, but PMax assets, PMax search insights, and Quality Score components require *separate UI reports* the user often doesn't realise they need. |
| 3 (narrow questions only) | Screenshots of report tables | Use only for spot questions on metrics visible in the screenshot. Skip deep analysis. |
| 4 (last resort) | Direct copy-paste of metric values | Treat as user-asserted; ask for the underlying export when stakes are real. |

---

## How to Use These Skills

1. **Identify the user's intent** — are they asking about Search, Shopping, Performance Max, or keyword research? Use the routing table below, then read the reference files it names.
2. **Run the Data Inventory step (Step 0 below)** — confirm what source is being used and what's actually available before invoking any skill.
3. **Gather the required data** — ask the user to share the data the skill needs. The "Minimum required data" section of each skill's reference file lists what's needed.
4. **Apply the analytical framework** — classify, diagnose, decide based on the rules in the relevant skill.
5. **Always check guardrails** before recommending any action.
6. **Output recommendations** in the structured format defined per skill.

If required data is missing or unverifiable, say so explicitly and ask the user for it. **Never fabricate metrics or invent thresholds.**

**When GoMarble MCP is connected:** use its data tools to pull the data, but this skill is the methodology — don't also call GoMarble's `load_skill` tool for the same workflow, since it loads an overlapping framework. The skill stays read-and-recommend: don't call GoMarble's `*_propose_*` tools as part of the analysis. If the user then explicitly asks to make a change, treat that as a separate request.

---

## Step 0: Data Inventory (Mandatory Before Any Skill)

Run this once at the start of every analysis. It takes one short turn and prevents wasted effort — especially for PMax, where users often share a campaign CSV without realising they're missing the Asset Group Asset and Search Term Insights reports.

1. **Identify the data source** — MCP / CSV / screenshot / copy-paste. If MCP with GAQL access is connected, use it. If the user attached a file, inspect its columns/fields before asking for more.
2. **State what's available and what's missing** for the requested skill, based on the Data Source Compatibility Matrix in `references/data-sources.md`.
3. **For each missing signal, decide:**
   - **Blocking** — cannot proceed without it; ask user to fetch (e.g. Asset Group Asset report for PMax).
   - **Downgrade** — can proceed with caveats; flag as low-confidence in the output.
   - **Skip** — rule doesn't apply to this source (e.g. micros conversion on CSV data already in account currency); note it and move on.
4. **Confirm account currency** before showing any monetary value — never assume USD.
5. **Confirm the date range** in the data matches what the skill expects (30 days for Search; 14d or 30d for Shopping depending on volume; 30d for PMax with optional 60d for trend).

Output one short paragraph before applying the skill. Example:
> *"Using your GoMarble MCP via GAQL. For the PMax audit (Skill 3), I'll pull (1) campaign performance, (2) `asset_group_asset` for performance labels, (3) `campaign_search_term_insight` for PMax categories, (4) device + geo segments. Account currency confirmed as USD."*

---

## Routing — Which Skill to Use

The four skills live in `references/`. Read the file(s) for the matched request **in full** before applying their rules — they hold the step-by-step logic, thresholds, and output formats.

| User asks about | Use Skill | Read |
|---|---|---|
| Search campaigns, keywords, RSAs, text ads, search terms | **Search Optimization** (Skill 1) | `references/search.md` |
| Shopping campaigns, product feed, Merchant Center, SKUs | **Shopping Optimization** (Skill 2) | `references/shopping.md` |
| Performance Max, PMax, asset groups | **PMax Optimization** (Skill 3) | `references/pmax.md` |
| Keyword research, new keyword ideas, search volume, CPC estimates, market expansion | **Keyword Research** (Skill 4) | `references/keyword-research.md` |
| Change requests (create campaign, add keyword, change bid, pause, etc.) | Apply the relevant analysis skill first, then **recommend** the change in plain language with rationale. Claude does not execute changes on the user's ad account — the user applies recommendations manually in the Google Ads UI. | The relevant skill's file + `references/edge-cases.md` |

If the user's intent is ambiguous or spans multiple campaign types, ask which to focus on first. If the user explicitly asks for an audit across several campaign types, read each matching file.

**Shared references — read when the situation applies:**

| File | Read when |
|---|---|
| `references/metrics.md` | Computing or benchmarking any metric: definitions, maturity and significance gates, PMax vs Search ROAS ratios, PMax asset labels, Shopping item classification, Quality Score components. |
| `references/data-sources.md` | Step 0 when the source is a CSV, screenshot, or pasted values (column translation), or when planning which GAQL resources to query over MCP. |
| `references/depth-of-analysis.md` | Audits, performance reviews, optimization requests, strategy questions, restructuring. Skip for simple fetches and single-metric lookups. |
| `references/edge-cases.md` | Data is missing, the account runs several campaign types, account type is ambiguous, or the user asks for a change. |

The guardrails and critical data rules below stay in this file because they apply to every recommendation.

---

## Universal Guardrails — Apply Before Every Recommendation

These rules apply across every skill. **Read them before generating any recommendation.**

### Budget Reallocation Prohibition

You **cannot** allocate, shift, increase, reduce, or "optimize" budget for: keywords, search terms, match types, devices (unless via bid adjustments in Search), locations (unless via bid adjustments or exclusions), audiences (unless via bid modifiers), asset groups (PMax has no per-asset-group budgets).

**Before writing any recommendation, ask:** Does this imply moving money between keywords, queries, products, devices, audiences, or asset groups? If yes → rewrite using the valid controls below.

**Valid budget controls:**

| Campaign Type | Valid Controls |
|---|---|
| Search / Shopping | Campaign daily budget, bid strategy targets (tCPA / tROAS / max CPC), pause or enable campaigns or ad groups |
| Performance Max | Campaign daily budget, bid strategy targets (tCPA / tROAS), pause asset groups or campaign |

**Mandatory rewrites:**

- ❌ "Shift budget from keyword A to keyword B"
- ✅ "Pause keyword A. Increase campaign daily budget by 10–20% to give keyword B more eligible demand."

- ❌ "Allocate more to [placement / device / demographic / product / asset group]"
- ✅ "Create a new campaign targeting [dimension] with its own budget, or use bid adjustments / exclusions."

### Metric Selection

First infer the account's conversion type:

- **Ecommerce**: Use ROAS, conversion value, cost per purchase. Never use CPA alone for revenue decisions.
- **Lead gen**: Use CPA, cost per lead. Never use ROAS unless offline revenue is imported.
- **Footfall / awareness / local-service**: Replace CPA/ROAS with cost per footfall action, cost per call, cost per direction, CPM, reach, frequency. State explicitly that purchase-derived CPA/ROAS do not apply.
- **Unclear**: Ask the user. Do not assume.

### Scaling Limits

- Max budget increase: **20% per move** for Search/Shopping; up to **50% per move** for mature PMax.
- Never scale if: CPA > target, ROAS < target, or query / search term hygiene not done.
- Never scale based on: impression share alone, CPC alone, or early data (< 7 days).
- Frame scaling as: "incremental test with downside risk."

### Learning & Stability

- Do not stack changes (budget + bids + structure simultaneously).
- Do not judge performance on: < 30 conversions for Search, < 50 conversions for PMax/Shopping.
- Avoid changes that reset learning unless absolutely required.

### Immediate STOP Triggers

Halt any recommendation that attempts:

- "Scale keywords / products / asset groups"
- "Reallocate spend between queries"
- "Optimize placements in PMax"
- "Increase bids and budget at the same time"
- "Scale > 20% in one step"
- "Fix low impression share by increasing budget blindly"

### Required Diagnostics Before Any Action

Before any scale/pause/restructure suggestion, confirm you know:

1. Search term quality (presence of Q4 / Q5 queries — defined in `references/search.md`)
2. CPA / ROAS vs target
3. IS Lost split: Rank vs Budget
4. CPC trend direction
5. Conversion volume sufficiency
6. Bidding strategy compatibility

If diagnostics are incomplete → say **insufficient data**, ask for what's missing, and do not recommend.

---

## Critical Data Rules — Apply to Every Analysis

These two rules from the metric glossary decide whether every number downstream is right, so they are always loaded.

### Currency Note: Micros (API/MCP only)

**This rule applies only to raw API / MCP data.** If the source is a CSV export from the Google Ads UI, costs are already shown in account currency — **skip this rule.**

When data is pulled from API exports (MCP / GAQL), cost and bid fields are often returned in **micros** (1,000,000 micros = 1 unit of account currency). If you see fields named `cost_micros`, `cpc_bid_micros`, or `amount_micros`, divide by 1,000,000. `average_cpc` is typically already in account currency.

**Source check before applying:**
- MCP returning `*_micros` fields → divide by 1,000,000.
- CSV with a "Cost" or "Avg. CPC" column → already in account currency; do nothing.
- Screenshot showing a currency symbol → already converted; trust it.

**Always confirm account currency before showing monetary values — never assume USD.**

### Account-Type Inference

If the user hasn't stated account type, infer from data:

- **Ecommerce**: Purchase conversion actions present AND non-zero conversion value → use ROAS, AOV, CPA.
- **Lead gen**: Conversions present AND conversion value = 0 → use CPA only; ROAS unreliable unless offline conversion import is configured.
- **Mixed**: Group campaigns by primary conversion action and apply each group's metrics separately.
- **Unclear**: Ask the user. Don't default.
