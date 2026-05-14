# GoMarble Paid Media Claude Skills

Deep Claude Skills for paid media operators — Meta Ads audits, Google Ads audits, creative analysis, search term diagnosis, PMax reviews, Shopping audits, and performance recommendations.

These skills help Claude reason like a senior media buyer.

They work with:
- connected MCP servers like GoMarble MCP
- uploaded CSV / Excel exports
- screenshots
- pasted tables

Use them when you want Claude to audit ad accounts, diagnose performance issues, find wasted spend, analyze creatives, and recommend what to do next.

---

## What is a skill?

A skill is a markdown file (`SKILL.md`) that teaches Claude how to run a specific workflow.

Each skill includes:
- what data to look for
- how to interpret performance
- decision rules and guardrails
- required checks before recommending action
- structured output formats
- examples of what to ask for when data is missing

The skill teaches Claude how to think through paid media problems with more depth and consistency.

---

## Skills included

### Meta Ads

A senior-media-buyer workflow for auditing and optimizing Meta Ads accounts.

Covers:
- account health checks
- conversion metric mapping
- campaign structure analysis
- ad set analysis
- performance analysis
- creative analysis
- video hook / hold diagnostics
- tracking and attribution caveats

Folder:

```bash
skills/meta-ads/SKILL.md
```

Use it for prompts like:

> Run a Meta Ads audit for the last 30 days. Identify what changed, what is wasting spend, which creatives are fatiguing, and what I should do next.

---

### Google Ads

A senior-media-buyer workflow for auditing and optimizing Google Ads accounts.

Covers:
- Search campaign optimization
- Q1–Q5 search term classification
- auction pressure diagnosis
- Shopping SKU classification
- Performance Max maturity checks
- PMax asset performance labels
- PMax vs Search comparison
- keyword research validation

Folder:

```bash
skills/google-ads/SKILL.md
```

Use it for prompts like:

> Run a Google Ads audit across Search, Shopping, and PMax. Find wasted spend, classify search terms, review PMax maturity, and recommend what to do next.

---

## Best with GoMarble MCP

These skills can work with exported files, screenshots, or pasted data.

They become more powerful when Claude is connected to GoMarble MCP, because Claude can access marketing data more directly instead of relying only on manual exports.

GoMarble MCP helps Claude work with data from platforms like:
- Meta Ads
- Google Ads
- Shopify
- GA4
- TikTok Ads
- LinkedIn Ads
- Klaviyo
- Google Sheets
- Bing Ads
- Google Search Console

Set up GoMarble MCP by following the instructions here:

```text
https://www.gomarble.ai/mcp-thankyou
```

---

## Want the full paid media operator?

Claude Skills are a useful starting point. GoMarble is the full paid media operator.

Use these free skills when you want to run one-off audits inside Claude.

Use GoMarble AI when your team needs:
- shared paid media context
- account diagnostics & RCA
- creative analysis
- competitor research
- recurring reports
- multi-channel diagnosis
- approval-based campaign actions
- Agent Mode for launching and updating ads

Try GoMarble AI:

```text
https://www.gomarble.ai?utm_source=github&utm_medium=repo&utm_campaign=paid_media_claude_skills
```

---

## Install

### Clone this repo

```bash
git clone https://github.com/gomarble-ai/paid-media-claude-skills.git
```

Then copy the skills you want into your Claude skills directory.

Example:

```bash
cp -r paid-media-claude-skills/skills/meta-ads ~/.claude/skills/
cp -r paid-media-claude-skills/skills/google-ads ~/.claude/skills/
```

Or upload each `SKILL.md` file manually inside Claude.

---

## Usage

Once installed, ask Claude to run the relevant workflow.

### Meta Ads examples

```text
Run a Meta Ads audit for the last 30 days and give me performance and creative recommendations.
```

```text
Analyze my active Meta ads for creative fatigue. Check frequency, CTR trend, Hook Rate, Hold Rate, and top-spend creatives.
```

```text
Find the Pareto set of ads driving 90% of spend. Classify each ad as keep, pause, watch, or create variations.
```

```text
Analyze my Meta ad sets from the last 7 days. Tell me which are worth keeping, watching, or changing.
```

---

### Google Ads examples

```text
Run a Google Ads audit across Search, Shopping, and PMax. Start with data inventory, then identify the biggest optimization opportunities.
```

```text
Classify my Search terms into Q1–Q5 tiers and recommend negatives, exact-match isolation, or bid changes.
```

```text
Audit my PMax campaigns. Check maturity, asset labels, search term insights, device/location performance, and PMax vs Search ROAS.
```

```text
Classify my Shopping products into KILL, DOWNGRADE, PROMOTE, or MONITOR based on SKU-level spend, AOV, conversions, and ROAS.
```


---

## Important note

These skills are read-and-recommend workflows.

They do not directly change your ad accounts.

Claude will analyze the data and recommend actions. You apply those recommendations manually in Meta Ads Manager or Google Ads.

For approval-based execution, use GoMarble AI.

---

## Repo layout

```bash
paid-media-claude-skills/
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── docs/
│   └── gomarble-mcp-setup.md
├── examples/
│   ├── meta-ads-example-prompts.md
│   └── google-ads-example-prompts.md
└── skills/
    ├── meta-ads/
    │   └── SKILL.md
    └── google-ads/
        └── SKILL.md
```

---

## Who this is for

These skills are built for:
- media buyers
- performance marketers
- growth marketers
- creative strategists
- agency teams
- founders who manage paid media
- operators using Claude for marketing analysis

They are not generic marketing prompts.

They are deep operating workflows for paid media accounts.

---

## Contributing

PRs are welcome.

Good contributions include:
- new audit frameworks
- better guardrails
- clearer output formats
- missing-data handling
- examples from real paid media workflows
- improvements to Meta, Google, PMax, Shopping, or creative analysis logic

Please keep contributions practical, specific, and grounded in how paid media operators actually work.

---

## License

See `LICENSE`.

---

## About GoMarble

GoMarble is the AI agent for paid media teams.

It connects your ads, analytics, and creatives to recommend what to do next — and does it for you.

Learn more:

```text
https://www.gomarble.ai?utm_source=github&utm_medium=repo&utm_campaign=paid_media_claude_skills
```
