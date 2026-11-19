---
name: tolstoy-connectors
description: Reach a platform the brand connected in Tolstoy - Instagram, Meta Ads, Pinterest, YouTube, OpenAI Ads (ChatGPT Ads), Gorgias, Triple Whale, Attentive, Yotpo, Judge.me, Okendo, Postscript, Rebuy, Nosto, Klevu, Bazaarvoice, Smile.io, Loop Returns, AfterShip, Feedonomics, Channable, Akeneo, Brandfolder, Klaviyo, Shopify, TikTok, TikTok Ads, TikTok Shop, X, Google Analytics, Slack, Gmail, Outlook, Google Drive, Airtable, Asana, Canva or Drip - through the Tolstoy Agent and the run_agent tool. Use for any request about one of these platforms, and load it before the platform-group skills.
---

# Reach connected platforms through Tolstoy

The Tolstoy MCP server has no separate tool for each platform. A brand connects a
platform once in the Tolstoy platform under **Settings > Connectors**
(`https://platform.gotolstoy.com/settings/connectors`). After that, the Tolstoy Agent
can work with that platform, and you reach the Tolstoy Agent with `run_agent`.

## Before the first turn

1. Check that `run_agent` and `get_agent_chat` are in the current tool list. If they
   are missing, say so and stop. Do not guess another tool name.
2. Each `run_agent` turn spends the workspace's credits. Start a turn only when the
   user asks for work on the platform. `get_usage` reads the balance.
3. You cannot see from here which platforms are connected. If the Tolstoy Agent answers
   that a platform is not connected or needs a reconnect, ask the user to connect it
   under Settings > Connectors and try again after they confirm. The brand completes
   the platform's own sign-in; never ask for a password, API key or code in chat.

## Ask the Tolstoy Agent

1. Call `run_agent` with `message` set to the user's request in their own words. Name
   the platform, the account or store when there are several, and the date range.
2. `run_agent` returns once the turn has started. Read the answer with
   `get_agent_chat` and its `chatId`, and read again while the turn is still running.
3. For a follow-up on the same work, call `run_agent` again with the same `chatId`.
4. `stop_agent` stops a turn the user no longer wants.

## Writes need a fresh yes

Sending a message or campaign, publishing a post, changing an ad's status or budget,
issuing a refund, reward or return, replying to a review or ticket, and editing a
catalog or feed all change something outside Tolstoy. Before you ask the Tolstoy Agent
to do one, show the user exactly what will change and get an explicit yes. Afterwards,
ask the agent to read the result back, and report complete, partial and failed
outcomes separately.

## Report what came back

- Give each number with its platform, account and date range.
- A value the agent could not read is "not available", never 0.
- Say when the agent's answer is thin or partial, and do not fill gaps with guesses.

## What has been tested

Reaching platforms through `run_agent` is new. In Tolstoy's own tests, Klaviyo returned
real data and X returned thin data. The Attentive connector has no campaign reporting.
The other platforms have not been tested through `run_agent` yet, so treat their first
answers as unverified and check them in the platform itself when the result matters.
