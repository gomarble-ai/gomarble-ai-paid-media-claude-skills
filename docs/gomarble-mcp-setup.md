# GoMarble MCP Setup

Use GoMarble MCP to connect Claude with your marketing data.

These paid media skills can work with uploaded files, screenshots, or pasted data. They work best when Claude is connected to GoMarble MCP, so Claude can query your marketing data directly.

The easiest way to connect is to install the GoMarble plugin (see the [README](../README.md#install)). It adds the connector for you. Use the steps below only if you want to add the connector by hand.

More about GoMarble MCP: https://www.gomarble.ai/mcp

## Setup steps

1. Open Claude Integrations:

   https://claude.ai/settings/integrations

2. Add a new custom integration.

3. Use this integration name:

   GoMarble AI

4. Use this integration URL:

   https://apps.gomarble.ai/mcp-api/mcp

   If you added GoMarble earlier with the older `https://apps.gomarble.ai/mcp-api/sse` address, it still works. Don't add a second connector if you already have one.

5. Click Add.

6. Click Connect.

7. Go to GoMarble:

   https://apps.gomarble.ai

8. Log in with your work email ID.

9. Add your ad accounts and integrations here:

   https://apps.gomarble.ai/settings/integrations

10. Return to Claude and start using GoMarble MCP.

## Test your MCP setup

Once connected, try asking Claude:

- Give me the ROAS of my Facebook ad accounts in the past week.
- Analyze which audience segments have the highest ROAS across Facebook Ads and Google Ads.
- Generate a weekly performance report comparing my Google Ads and Facebook Ads campaigns.
- Run a Meta Ads audit for the last 30 days using the GoMarble MCP data.
- Run a Google Ads audit across Search, Shopping, and PMax using GoMarble MCP.

## Using GoMarble MCP with these skills

After MCP is connected, install the GoMarble plugin, or upload the skill folders from this repo. Each folder holds a `SKILL.md` plus a `references/` folder with the detailed steps, so upload the whole folder, not just `SKILL.md`:

- `skills/meta-ads/`
- `skills/google-ads/`

Then ask Claude to run the relevant skill.

Example:

Run a Meta Ads audit using GoMarble MCP. Start with data inventory, identify the primary conversion metric, analyze campaign structure, then give me performance and creative recommendations.

Example:

Run a Google Ads audit using GoMarble MCP. Start with data inventory, then review Search, Shopping, PMax, wasted spend, and keyword opportunities.

## What data does GoMarble MCP help Claude access?

Depending on the integrations you connect, GoMarble MCP can help Claude work with marketing data from platforms such as:

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

## Join the AI in Ads Slack community

Want to discuss AI workflows for paid media, Claude Skills, MCP, creative analysis, and ad account automation with other operators?

Join the AI in Ads Slack community:

https://join.slack.com/t/ai-in-ads/shared_invite/zt-3t2twdhw7-UsRpEoqPgScNklp8ydsCgw
