# Reporting and connection recovery

First confirm the workspace and the tool your task needs. A successful Tolstoy sign-in does not connect a separate service such as Meta Ads.

## Choose the connection for the task

| Task | Connection | What to check |
| --- | --- | --- |
| Find existing media, inspect product tags, or inspect a storefront video widget | Library or full workspace | Confirm the store with `get_setup_state`. |
| Read Meta ad performance | Full workspace | Meta Ads must be connected to the same Tolstoy workspace. |
| Read an AI Widget Builder widget's saved analytics | Full workspace | Get its `widgetId` from `list_ai_widgets`. |
| Generate content in Studio | Full workspace | Confirm the intended task and any generation cost before starting. |

- Library: `https://apilb.gotolstoy.com/mcp/v1/library/mcp`
- Full workspace: `https://apilb.gotolstoy.com/mcp/v1/mcp`

The Library connection declares 20 tools: 17 model-facing tools and three upload-panel callbacks. It does not expose Studio generation, Meta ad tools, or AI widget analytics. Refresh tool discovery after changing a connection. If the expected tools remain absent, inspect the endpoint and workspace before retrying the task.

If your organization uses an MCP gateway, its administrator must configure the remote Streamable HTTP connection and supported OAuth flow. Then verify tool discovery and the intended Tolstoy workspace from the person's own client. A gateway installation alone does not prove that the person's connection works.

## Read the right report

### Meta advertising

`get_ads_performance` reads live Meta Insights data. It supports campaign, ad-set, or ad level and date presets such as `last_7d`. An optional `adAccountId` selects the account.

Ask:

> Read campaign-level Meta performance for the last seven days on my confirmed ad account. Show spend, clicks, CTR, currency, and the reporting window. Preserve the conversion action types. Do not change campaigns or budgets. If a read fails, show the error and stop instead of treating it as zero activity.

The tool does not calculate ROAS. Confirm which conversion event represents the business result before calculating it from `actions` and `action_values`. Different action types can describe the same conversion. If the result is truncated, report that the totals may be incomplete. Dates use the ad account's timezone and Meta's default attribution window.

### AI widgets and product-page video widgets

`get_ai_widget_analytics` reads saved metrics for widgets built with the AI Widget Builder. Use `list_ai_widgets` to get the `widgetId`. Supply `from` and `to` together as calendar dates; both UTC days are included, with a maximum span of 90 days. Without dates, the tool uses the last 30 days. It runs saved metric definitions and does not create new calculations.

`list_widgets` returns storefront video experiences such as Spotlight and Stories. Their `publishId` values are not accepted by `get_ai_widget_analytics`. `get_widget` can inspect a product's content selection, but that read is not a product-performance report.

For product-level performance or static-image reporting, first agree on the required fields, dates, and attribution definition with support. Do not infer those metrics from a media list or substitute an AI widget's report for a storefront video widget's report.

### Exporting a report

Tolstoy's Analytics interface supports CSV download for charts that have an export configured. Open the relevant saved chart, set the store and date filters, and use **Download CSV** if the chart exposes it. Check the exported columns and row count before importing the file into another system.

These MCP tools do not configure a Fivetran or BigQuery sync. A CSV download is a manual export. Ask support to confirm the supported export and data coverage before planning a scheduled warehouse feed.

## Recover a missing Meta Ads connection

1. Confirm that Tolstoy is open in the intended workspace.
2. Open **Settings → Integrations** and connect Meta Ads with an account that has access to the intended ad account. Follow the permissions shown in that flow. Connecting Shopify or Instagram alone does not connect Meta Ads.
3. Return to the full-workspace MCP connection and make one read-only `list_ad_campaigns` request. If more than one ad account is available, use the verified `adAccountId` in the next request.
4. Run one `get_ads_performance` read for that same account. Check the response and any error text.

If Meta reports missing permissions, ask the integration owner to complete the required reconnect. Changing the date preset or repeating Tolstoy OAuth does not repair a separate Meta integration. Share the client, store domain, tool, failure time, and error text with support. Keep tokens and signed upload URLs out of the report.

## Use the browser when a file transfer fails

The full-workspace connection can give a command-capable client a signed upload plan. It also offers a browser upload path. If a command is refused or a transfer keeps failing:

1. Check the Library first. A file that completed after a retry does not need another upload.
2. Ask the assistant to open `upload_library_assets_from_panel`, then choose the files yourself. The panel transfers each file separately and reports what arrived and what failed.
3. If your client does not show the panel, upload the files directly in Tolstoy.
4. Find each uploaded item with `list_assets` or `search_assets`, then use its returned ID and type with `get_asset` to verify the result. Keep failed files separate and do not mark them complete.

Changing the upload path can help you continue work, but it does not diagnose a connection reset. If it recurs, retain the file size, client and execution environment, failure time, error code, and whether the upload used a single transfer or multiple parts. Do not publish private files on the open web or send signed upload URLs to support. Stop on an authorization refusal instead of repeatedly retrying it.
