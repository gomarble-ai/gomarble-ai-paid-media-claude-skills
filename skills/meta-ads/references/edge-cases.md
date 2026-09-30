# Cross-Cutting Notes

## How to handle missing data

If the user can't provide the data a skill needs, do **not** invent values. State explicitly:

> *"To answer this properly I need [specific metrics]. You can pull these from [Ads Manager export / a connected data tool / Events Manager]. Without them I can outline the framework but not give a recommendation."*

## How to handle change requests

When the user asks Claude to change something in their account (e.g. *"pause this ad"*, *"raise the budget 20%"*):

1. Run the relevant analysis skill to validate the change is justified.
2. Apply the guardrails (especially scaling caps, top-performer protection, and the "no ad-level budget moves" rule).
3. **Recommend the change in plain language** — exact entity, current value, proposed value, rationale, what to monitor afterwards, and any safety warnings (learning-phase reset, > 50% decrease, > 100% increase, etc.).

Claude does not execute changes on the user's ad account. These skills are read-and-recommend only — the user applies recommendations manually in Ads Manager.

## How to handle multiple account types in one account

If the account has both purchase-optimized and lead-optimized campaigns:

- Group ad sets by their `custom_event_type`
- Apply each group's PCM separately
- Never aggregate ROAS across purchase + lead campaigns

## How to handle account-type ambiguity

Always classify the account before applying KPIs:

1. Check the actual ad-set-level conversion events (not the campaign / ad set names).
2. Check whether conversion value is populated.
3. If unclear, ask the user.
4. Apply the special-case check for COMPLETE_REGISTRATION on purchase objectives (3rd-party tracker scenario).

## How to handle stale data

Meta campaigns change frequently. If the data the user shared is more than a day or two old:

- Ask for a fresh pull before any recommendation
- Especially before pause / scale / structural changes
- Recommendations based on stale state can be wrong or harmful

## What to do when the API / export doesn't show a needed metric

Some signals aren't directly available via standard insights exports:

- **EMQ Score** → manual check in Events Manager
- **Audience segment configuration** → manual check in Audience Manager (the breakdown shows distribution, but setup state isn't readable)
- **Comments / sentiment** → manual check in Ads Manager or the Page
- **Per-product conversion data in catalog ads** → not provided; use spend + CTR as proxy

When a signal isn't available, state that explicitly, point the user to where they can check it manually, and frame the recommendation around the data that IS available.
