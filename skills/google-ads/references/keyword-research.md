# Skill 4: Keyword Research

**Contents:** When to use this skill · When NOT to use this skill · Data to gather · Step 1: Generate Candidate Keywords · Step 2: Evaluate Each Keyword · Step 3: Final Decision Rule · Step 4: Match Type Assignment · Output Format (per keyword) · Core Principles · Minimum required data (by source) · Tool hints

When a decision depends on search volume, CPC (top-of-page bid), or competition, real keyword data is required. **Without that data, do not estimate volume or CPC — say insufficient data and ask the user to share it.**

## When to use this skill

| Trigger | Action |
|---|---|
| "Do keyword research" / "Suggest keywords" / "Find buyer keywords" | Discover new keyword ideas + validate |
| "Are these keywords good?" / "Which should I keep?" | Validate against volume + CPC |
| "Which keyword is better?" / "Prioritize these" | Compare metrics across candidates |
| "Create a new search campaign" / "Launch Google Search ads" | Research → validate BEFORE proposing structure |
| "Expand to a new country" / "International Google Ads" | Pull metrics with the new geo + language |
| "Can we scale?" / "What CPCs should we expect?" | Pull top-of-page bid forecasts |

## When NOT to use this skill

Keyword Planner data is NOT required for:

- Creative work (RSA headlines, descriptions, ad strength)
- Structure work (match type explanations, campaign naming, account audits)
- Post-performance analysis (CPA / ROAS analysis, search-term-report mining for existing campaigns)

## Data to gather

For each candidate keyword, the user needs to provide (or pull from any keyword-research tool — Keyword Planner, third-party tools, etc.):

- **Search volume** (monthly searches in the target geo + language)
- **Top-of-page bid range** (Low / Medium / High, or explicit min–max CPC)
- **Competition** (Low / Medium / High — used only as a tie-breaker)

If targeting a specific geography or language, confirm the metrics are scoped to that region.

## Step 1: Generate Candidate Keywords

Generate using buyer-intent patterns only.

**Approved patterns:**

- [service] + agency
- [service] + management
- [service] + pricing
- [service] + cost
- [service] + consultant
- [software] + for + [industry]
- [competitor] + alternative

**Disallowed patterns:**

- how to
- what is
- guide
- tips
- tutorial
- free
- examples

## Step 2: Evaluate Each Keyword

| Criterion | Rule |
|---|---|
| **Intent** | Buyer intent must be explicit in the keyword text. Unclear → REJECT. |
| **Search Volume** | Volume < 50 → REJECT. Volume ≥ 50 → PASS. |
| **Top-of-Page Bid** | High → STRONG APPROVE. Medium → APPROVE. Low → APPROVE only if intent is very strong. Zero / Missing → REJECT. |
| **Competition** | Tie-breaker only. Never reject solely due to high competition. |

## Step 3: Final Decision Rule

```
IF
  buyer intent = YES
  AND volume ≥ 50
  AND top-of-page bid ≠ Low / Zero
THEN
  APPROVE
ELSE
  REJECT
```

## Step 4: Match Type Assignment

For approved keywords only:

| Match Type | When to Use |
|---|---|
| Exact | Very strong intent, specific wording |
| Phrase | Core scalable keywords |
| Broad | Do NOT suggest by default |

## Output Format (per keyword)

```
Keyword:
Match Type:
Volume:
Top of Page Bid:
Competition:
Decision: APPROVE / REJECT
Reason:
```

**Example:**

```
Keyword: google ads agency for ecommerce
Match Type: Phrase
Volume: 90
Top of Page Bid: High
Competition: Medium
Decision: APPROVE
Reason: Clear buyer intent + active advertiser bidding
```

## Core Principles

1. Intent > Volume (always)
2. Top-of-page bid = strongest commercial signal
3. Informational keywords = auto-reject
4. Fewer correct keywords > many random ones

## Minimum required data (by source)

| Source | What you need |
|---|---|
| MCP | Per candidate keyword (scoped to target geo + language): monthly search volume, top-of-page bid range (low / high), competition level. Via tools like `google_ads_keyword_discover` (seed → ideas) and `google_ads_keyword_metrics` (validate specific keywords). |
| CSV | A Keyword Planner export covering the target geo + language. Standard Planner CSV columns map directly: "Avg. monthly searches" → volume; "Top of page bid (low range)" / "(high range)" → top-of-page bid; "Competition" → competition. |
| Screenshot / copy-paste | Workable if the user pastes the Planner table directly with all three signals. |

## Tool hints

This skill cannot run on guesses — never estimate volume or CPC from training data. If MCP keyword tools are available, they're the cleanest source. If only a CSV export is available, confirm it's scoped to the target geo and language before applying the decision rule (a US-scoped Planner export gives the wrong CPCs for a UK launch).
