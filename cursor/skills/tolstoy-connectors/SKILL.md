---
name: tolstoy-connectors
description: Reads the brand's own data and acts in platforms the brand connected in Tolstoy under Settings > Connectors, through the Tolstoy Agent and the run_agent tool - ad performance and campaigns, social posts and comments, support tickets, reviews and review replies, SMS and email subscribers, campaigns and messages, loyalty points and rewards, returns, shipment tracking, product feeds and PIM, attribution and profit, brand assets. Platforms include Instagram, Meta Ads, Pinterest, YouTube, OpenAI Ads (ChatGPT Ads), Gorgias, Triple Whale, Attentive, Yotpo, Judge.me, Okendo, Postscript, Rebuy, Nosto, Klevu, Bazaarvoice, Smile.io, Loop Returns, AfterShip, Feedonomics, Channable, Akeneo and Brandfolder. Use only when the user wants the brand's own account data or an action in one of these platforms. Not for writing or debugging code that integrates with a platform, and not for a platform this client already has its own connector for.
---

# Platforms the brand connected in Tolstoy

A brand connects a platform once in the Tolstoy platform under **Settings > Connectors**
(`/settings/connectors`). The Tolstoy Agent then works with that platform for the brand,
and you reach the Tolstoy Agent with `run_agent`. The Tolstoy MCP server has no separate
tool for each platform.

## When to use this

Use it when the user wants the brand's own data from a platform in the table below, or
an action in it: "how did our Meta ads do last week", "reply to yesterday's Judge.me
reviews", "which Gorgias tickets are about shipping".

Do not use it:

- for code that integrates with a platform: building a Shopify app, a Slack bot, a
  Klaviyo API client or a storefront theme. That is ordinary coding work.
- for general questions about how a platform works.
- for a platform this client already reaches through its own connector or plugin.
  Use that one.

## Before the first turn

1. Check that `run_agent` and `get_agent_chat` are in the current tool list. If they are
   missing, say so and stop. Do not guess another tool name.
2. Each `run_agent` turn spends the workspace's credits. Start a turn only when the user
   asks for work on the platform. `get_usage` reads the balance.
3. You cannot see from here which platforms are connected. If the Tolstoy Agent answers
   that a platform is not connected or needs a reconnect, ask the user to connect it under
   Settings > Connectors and continue after they confirm. The brand completes the
   platform's own sign-in; never ask for a password, API key or code in chat.

## Ask the Tolstoy Agent

1. Call `run_agent` with `message` set to the user's request in their own words. Name the
   platform, the account or store when there are several, and the date range. Ask about
   one platform per turn.
2. `run_agent` returns once the turn has started. Read the answer with `get_agent_chat`
   and its `chatId`, and read again while the turn is still running.
3. For a follow-up on the same work, call `run_agent` again with the same `chatId`.
4. `stop_agent` stops a turn the user no longer wants.

## Writes need a fresh yes

Sending a message or campaign, publishing a post, changing an ad's status or budget,
issuing points, rewards or returns, replying to a review, comment or ticket, and editing a
catalog or feed all change something outside Tolstoy. Before you ask the Tolstoy Agent to
do one, show the user exactly what will change and get an explicit yes. Afterwards, ask
the agent to read the result back, and report complete, partial and failed outcomes
separately.

## Report what came back

- Give each number with its platform, account and date range.
- A value the agent could not read is "not available", never 0.
- Say when an answer is partial, and do not fill gaps with guesses.

## What each connector covers

| Platform | What the Tolstoy connector covers |
| --- | --- |
| Instagram | Media and media insights, account insights, comments (read, reply, hide, delete), publishing, hashtag and tagged media, catalog product search |
| Meta Ads | Campaigns, ad sets, ads, creatives, catalogs and product sets, custom audiences, ad rules, studies, Instant Form leads |
| Pinterest | Account analytics, boards and sections, pins and top pins, pin search, image and video pins, followers |
| YouTube | Channel info and analytics, videos and video details, comments (read, reply, moderate), captions, playlists, video metadata and thumbnails |
| OpenAI Ads (ChatGPT Ads) | Account status and spending limits; campaigns, ad groups and ads; insights; conversion pixels and events; audiences; product feeds |
| Gorgias | Tickets and messages, customers, search, CSAT, tags, rules and macros, team performance, voice calls |
| Triple Whale | Channel attribution, customer journeys, marketing efficiency (MER, CPA, POAS), customer economics (CAC, LTV), profitability, product performance, orders, traffic and conversion |
| Attentive | Subscribers, custom attributes, events, catalog upload status, privacy request status |
| Yotpo | Reviews, Q&A, catalog, customers, purchases, review-request emails, UGC, loyalty |
| Judge.me | Reviews and moderation, review replies, review metrics, settings, webhooks |
| Okendo | Reviews, moderation and replies, review groups, customers, loyalty, quizzes, surveys |
| Postscript | SMS subscribers, SMS and MMS messages and delivery status, compliance, custom events |
| Rebuy | Recommendations, customer product history, data sources, Smart Search, Smart Collections |
| Nosto | Products, categories, sessions, orders, recommendations, statistics |
| Klevu | Search, product discovery, category merchandising, recommendations |
| Bazaarvoice | Reviews, ratings, Q&A, brand answers and comments |
| Smile.io | Loyalty customers, points, rewards, earning rules, VIP tiers |
| Loop Returns | Returns and return actions, labels, draft returns, exchange carts, Happy Returns shipments, destinations |
| AfterShip | Shipment tracking, courier detection, delivery estimates, tracking notifications |
| Feedonomics | Feed health, feed data quality, channel exports |
| Channable | Marketplace offers (price and stock), orders, returns, carriers |
| Akeneo | Products, catalogs and catalog structure, Asset Manager media, reference entities, workflows |
| Brandfolder | Assets, attachments, collections, metadata, uploads |
| Klaviyo | Campaigns and email drafts, flows, forms, lists and segments, consent, catalogs, coupons, reviews, reports |
| Shopify | Catalog, orders, customers, analytics, themes and content, through the Admin API |
| TikTok | Organic profile publishing, account content and performance |
| TikTok Ads | Campaigns, ad groups and ads, budgets, targeting, creatives, performance |
| TikTok Shop | Seller catalog, shoppable posts, product anchors, shop performance, order counts |
| X | Organic posts where the brand's X API plan allows reads, and X Ads when the connection granted ads access |
| Google Analytics | GA4 traffic, acquisition, key events, ecommerce, promotions, audiences, realtime |
| Slack | Channel messages, reactions and pins, files, users |
| Gmail | The connected mailbox: messages, threads, drafts, sending, labels, attachments |
| Outlook | The connected mailbox: search, read, draft, send, reply, forward, organize |
| Google Drive | Files, sharing, comments and revisions; Docs, Sheets and Slides |
| Airtable | Bases, records, fields, views, forms, automations |
| Asana | Tasks, projects, comments, attachments, portfolios, goals, custom fields, time tracking |
| Canva | Designs and folders, exports, asset uploads, imports |
| Drip | Email campaign drafts, test emails, audiences, campaign results |
