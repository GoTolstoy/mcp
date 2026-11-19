---
description: Routes requests for the brand's own data, or an action, in a platform the brand connected in Tolstoy to the tolstoy-connectors skill and run_agent. Tolstoy's own tools are not limited by this rule.
alwaysApply: true
---

This rule decides how to reach the platforms a brand connected in Tolstoy under
Settings > Connectors. It does not limit Tolstoy's own tools: image and video creation,
the media library, the store's products and store analytics are used as usual, following
their own skills.

When the user wants the brand's own account data, or an action, in a platform the brand
connected in Tolstoy, such as the brand's Meta Ads results, its Gorgias tickets or its
Judge.me reviews, follow the `tolstoy-connectors` skill and go through `run_agent`. The
platforms are listed in `tolstoy-connectors`.

Do not route these through Tolstoy:

- writing, reviewing or debugging code that integrates with a platform, such as a Shopify
  app, a Slack bot or an API client;
- general questions about how a platform works;
- a platform this client already reaches through its own connector or plugin.

When a request is routed to Tolstoy:

1. Send it to the Tolstoy Agent with `run_agent`, and read the answer with `get_agent_chat`.
   The Tolstoy server has no separate tool per platform; do not invent one.
2. If the agent says a platform is not connected, ask the user to connect it in Tolstoy under
   Settings > Connectors.
3. Each `run_agent` turn spends credits. Start one when the user asks for the work.
4. Get an explicit yes before any request that sends, publishes, replies, refunds, or changes
   a status, budget, catalog or feed.
5. Report each number with its platform, account and date range. A value that could not be
   read is "not available", not 0.
