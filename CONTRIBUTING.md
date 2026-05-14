# Contributing to GoMarble Paid Media Claude Skills

Thanks for your interest in improving these skills.

This repo contains Claude Skills for paid media operators. Contributions should make the skills more useful, accurate, and practical for real Meta Ads and Google Ads workflows.

## What we welcome

Good contributions include:

- Better audit frameworks
- Clearer decision rules
- Stronger guardrails
- Better missing-data handling
- Improved output formats
- Example prompts
- Real-world paid media edge cases
- Improvements to Meta Ads, Google Ads, PMax, Shopping, Search, or creative analysis logic

## What we do not want

Please avoid:

- Generic marketing prompts
- Vague AI instructions
- Unsupported benchmark claims
- Platform rules that are not true in Meta Ads Manager or Google Ads
- Recommendations that imply unsafe account changes
- Anything that asks Claude to make account changes without user review
- SaaS-specific repackaging or productization of these skills without GoMarble's permission

These skills are read-and-recommend workflows. Claude should analyze and recommend. The user applies changes manually.

## Service use is allowed

Agencies, consultants, freelancers, and in-house teams may use these skills for internal work and client-service work.

The license restricts turning these materials into, or embedding them inside, a commercial SaaS, software product, marketplace product, AI agent product, API, browser extension, plugin, or hosted workflow product without permission.

## Skill format

Each skill should live in its own folder:

`skills/[skill-name]/SKILL.md`

For this repo, the current folders are:

- `skills/meta-ads/SKILL.md`
- `skills/google-ads/SKILL.md`

Each `SKILL.md` should include:

- Name and description
- When to use the skill
- Required data
- Workflow steps
- Decision rules
- Guardrails
- Output format
- Missing-data handling

## Quality bar

Before opening a pull request, please check:

- Is the recommendation actually actionable in Meta Ads Manager or Google Ads?
- Does it avoid inventing metrics?
- Does it say when data is missing?
- Does it protect top performers?
- Does it avoid over-optimizing on weak data?
- Does it distinguish Meta, Google Search, Shopping, and PMax mechanics correctly?
- Does it avoid claiming that Claude directly changes ad accounts?
- Does it clearly separate analysis from execution?

## Read-and-recommend principle

These skills are designed for analysis and recommendations.

Claude should:

- Inspect the available data
- Explain what is missing
- Diagnose the likely issue
- Recommend the next best action
- Explain the risk and what to monitor

Claude should not:

- Pretend to have data it does not have
- Invent account metrics
- Recommend unsafe budget changes
- Tell the user that changes were made in an ad account
- Bypass user review or approval

## Pull request process

1. Fork the repo.
2. Create a new branch.
3. Make your changes.
4. Open a pull request.
5. Include a short explanation of what changed and why.

Useful PR descriptions include:

- Which skill changed
- What workflow or edge case improved
- What guardrail was added or clarified
- Any example prompt used to test the change

## Example contribution ideas

Good first contributions:

- Add more example prompts
- Improve missing-data instructions
- Add clearer warnings around low-signal recommendations
- Add platform-specific caveats
- Improve output templates
- Add examples for ecommerce, lead gen, or mixed accounts

Larger contributions:

- Add a new paid media skill
- Expand creative research workflows
- Improve PMax audit logic
- Add better Shopping feed diagnostics
- Add more Meta creative analysis patterns
- Add more multi-channel analysis workflows

## Attribution and licensing

By contributing, you agree that your contribution will be licensed under the repo's license.

Please make sure any contribution is your own work or that you have the right to submit it.

If you redistribute, remix, or publish modified versions of these materials, follow the attribution requirements in the license.
