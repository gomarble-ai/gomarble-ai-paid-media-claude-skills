![GoMarble](assets/logo.png)

# GoMarble for Claude

Senior-media-buyer audits for Meta Ads and Google Ads, run by Claude on your live ad account data.

This plugin gives Claude two things:

1. **Two paid media skills.** These are deep audit workflows for Meta Ads and Google Ads. They teach Claude what data to pull, how to read it, which guardrails to check, and how to lay out recommendations.
2. **The GoMarble connector.** This lets Claude read your Meta Ads, Google Ads, Shopify, GA4 and other marketing data directly, so you don't have to export anything.

Ask Claude to audit an account, find wasted spend, or diagnose creative fatigue. It will pull the data, run the checks a senior media buyer would, and tell you what to change next.

---

## What's inside

| Part | What it does |
|---|---|
| `meta-ads` skill | Meta Ads (Facebook + Instagram) audits. Covers the account health check, conversion metric mapping, campaign structure, ad set rules, the Pareto set of ads driving spend, creative fatigue, and Hook Rate / Hold Rate video diagnostics. |
| `google-ads` skill | Google Ads audits. Covers Q1–Q5 search term classification, rank vs budget auction pressure, Shopping SKU classification, PMax maturity gates and asset labels, PMax vs Search ROAS, and keyword research checks. |
| GoMarble connector | A remote MCP server at `https://apps.gomarble.ai/mcp-api/mcp`. You sign in with your GoMarble account (OAuth). It gives Claude read access to the ad accounts and data sources you've connected in GoMarble. |

The skills also work without the connector. You can share CSV or Excel exports, screenshots, or pasted tables instead. Each skill tells Claude which checks still hold on each kind of data and asks for anything missing.

---

## Install

### Claude Code

```text
/plugin marketplace add gomarble-ai/gomarble-ai-paid-media-claude-skills
/plugin install gomarble@gomarble-ai
```

### Claude and Claude Cowork

Install **GoMarble** from the plugin directory once it's listed. You can also upload the plugin from your organization's plugin settings.

---

## Connect your ad accounts

1. The first time Claude uses GoMarble, you'll be asked to sign in. In Claude Code, run `/mcp`, pick `plugin:gomarble:gomarble`, and choose **Authenticate**.
2. Log in at [apps.gomarble.ai](https://apps.gomarble.ai) with your work email.
3. Add your ad accounts and data sources at [apps.gomarble.ai/settings/integrations](https://apps.gomarble.ai/settings/integrations).
4. Come back to Claude and ask for an audit.

**Already added GoMarble as a custom connector?** If you set it up by hand earlier (for example at `https://apps.gomarble.ai/mcp-api/sse`), you'll see two GoMarble connectors after installing the plugin. Remove the old custom one in Claude's connector settings and keep the plugin's.

Depending on what you connect, Claude can read data from Meta Ads, Google Ads, Shopify, GA4, TikTok Ads, LinkedIn Ads, Klaviyo, Bing Ads, Google Search Console and more.

---

## Usage

Invoke a skill by name (`/gomarble:meta-ads`, `/gomarble:google-ads`) or just describe what you want.

### Meta Ads

```text
Run a Meta Ads audit for the last 30 days. Identify what changed, what is wasting spend, which creatives are fatiguing, and what I should do next.
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

### Google Ads

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

## Read and recommend only

The skills never change your ad accounts. Claude analyzes the data and recommends actions, and you apply them in Meta Ads Manager or Google Ads.

The GoMarble connector also offers approval-based tools for making changes. The skills don't use them. For approval-based execution with a full team workflow, use [GoMarble AI](https://www.gomarble.ai?utm_source=github&utm_medium=repo&utm_campaign=claude_plugin).

---

## Data and privacy

- **What the plugin runs locally:** nothing. It has no hooks, scripts, or local servers. It contains markdown skill files and one connector setting.
- **What it connects to:** one remote MCP server, `https://apps.gomarble.ai/mcp-api/mcp`, over HTTPS. You sign in with OAuth. The plugin stores no credentials.
- **What data moves:** when Claude calls a GoMarble tool, GoMarble reads from the ad platforms and data sources you connected in your GoMarble account and returns the results to Claude. Tool requests and their results pass through GoMarble's servers.
- **Access control:** Claude can only reach accounts that your GoMarble login can reach. You can disconnect data sources in GoMarble, or disconnect the connector in Claude, at any time.

GoMarble's privacy policy: [gomarble.ai/privacy](https://www.gomarble.ai/privacy).

---

## Use the skills without the plugin

To install only the skills:

```bash
git clone https://github.com/gomarble-ai/gomarble-ai-paid-media-claude-skills.git
cp -r gomarble-ai-paid-media-claude-skills/skills/meta-ads ~/.claude/skills/
cp -r gomarble-ai-paid-media-claude-skills/skills/google-ads ~/.claude/skills/
```

Or zip each skill folder, including its `references/` folder, and upload it in Claude's skill settings. Uploading `SKILL.md` alone leaves out the step-by-step detail the skill reads from `references/`. To add the connector by hand, follow [docs/gomarble-mcp-setup.md](docs/gomarble-mcp-setup.md).

---

## Repo layout

```text
gomarble-ai-paid-media-claude-skills/
├── .claude-plugin/
│   ├── plugin.json        # plugin manifest
│   └── marketplace.json   # lets Claude Code install from this repo
├── .mcp.json              # GoMarble connector
├── assets/                # plugin icon and logo
├── skills/
│   ├── meta-ads/
│   │   ├── SKILL.md       # routing, guardrails, critical checks
│   │   └── references/    # one file per workflow + metrics, data sources
│   └── google-ads/
│       ├── SKILL.md
│       └── references/
├── docs/
│   └── gomarble-mcp-setup.md
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE.md
└── README.md
```

---

## Who this is for

Media buyers, performance and growth marketers, creative strategists, agency teams, and founders who run their own paid media. These are deep operating workflows for paid media accounts, not generic marketing prompts.

---

## Contributing

PRs are welcome: better audit frameworks, stronger guardrails, clearer output formats, better missing-data handling, and real-world edge cases for Meta, Google, PMax, Shopping, or creative analysis. See [CONTRIBUTING.md](CONTRIBUTING.md).

---

## License

Free to use with attribution. See [LICENSE.md](LICENSE.md).

---

## About GoMarble

GoMarble is the AI agent for paid media teams. It connects your ads, analytics, and creatives, recommends what to do next, and can do it for you.

[gomarble.ai](https://www.gomarble.ai?utm_source=github&utm_medium=repo&utm_campaign=claude_plugin)
