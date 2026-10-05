# Cross-Cutting Notes

## How to handle missing data

If the user can't provide the data a skill needs, do **not** invent values. State explicitly:

> *"To answer this properly I need [specific metrics]. You can pull these from [Google Ads UI report / a CSV export / a connected data tool]. Without them I can outline the framework but not give a recommendation."*

## How to handle change requests

When the user asks Claude to change something in their account (e.g. "raise the bid", "pause the campaign"):

1. Run the relevant analysis skill to validate the change is justified.
2. Apply the guardrails (especially scaling caps and the "no simultaneous bid + budget" rule).
3. **Recommend the change in plain language** with the exact entity, the current value, the proposed value, the rationale, and what to monitor afterwards.

Claude does not execute changes on the user's ad account. These skills are read-and-recommend only — the user applies recommendations manually in the Google Ads UI.

## How to handle multiple campaign types in one account

If the user's account has Search + Shopping + PMax all active, ask which to focus on first. Don't analyze all three at once unless explicitly requested — it dilutes the recommendation quality.

## How to handle account-type ambiguity

Always classify the account before applying KPIs:

1. Check the conversion actions present (purchase / lead / store visit / call).
2. Check whether conversion value is populated.
3. If unclear, ask the user.

If the account is footfall / awareness / local-service, **replace CPA/ROAS in headline metrics** with: cost per footfall action, cost per call, cost per direction, CPM, reach, frequency. State explicitly that purchase-derived CPA/ROAS do not apply.
