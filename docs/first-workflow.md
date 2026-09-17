# Your first useful Tolstoy workflow

Use Tolstoy to find existing videos for one product and check where they appear. You will finish with a media shortlist you can use to make a product-page decision.

## 1. Connect your workspace

| Client and scope | Remote MCP endpoint |
| --- | --- |
| Cursor: full Tolstoy workspace | `https://apilb.gotolstoy.com/mcp/v1/mcp` |
| Claude: Tolstoy Library | `https://apilb.gotolstoy.com/mcp/v1/library/mcp` |

In the client's connector or MCP settings, add the endpoint and complete the Tolstoy sign-in for your workspace. Your team may need to approve the connector first. Each person must also finish their own connection. A team approval or another person's successful sign-in does not establish yours.

The Library endpoint covers existing media, product tags, catalogs, and shoppable widgets. It does not expose Studio generation or paid-ad tools. A custom connection does not require or prove a directory listing.

For client-specific installation steps, use **Settings → MCP** in Tolstoy. The [Cursor plugin](../.cursor-plugin/plugin.json) includes the workspace connection and the `tolstoy-product-media` skill.

## 2. Check the store

Ask:

> Check my Tolstoy setup for brand, catalog, integrations, and stores. Tell me which brand and store domain this connection uses, whether the catalog is ready, and whether any integration needs attention. Do not change anything.

Confirm that the answer names your intended store. If it names another workspace, disconnect and sign in to the correct one. If a section cannot be read, its state is unknown; it is not proof that your account has no data.

## 3. Make a product-page decision

Replace the product name in this prompt:

> For [product name], find up to five existing Tolstoy library videos that could help a shopper understand it. Inspect the available details and product tags. Give me exact asset IDs, available preview links, why each fits, and anything you could not verify. Check the current shoppable widget for this product if one exists. Recommend a shortlist; do not change tags or publish anything.

Review the actual videos and choose the assets you want to use. If you want Tolstoy to change product tags or a widget, name that change in a follow-up request. The assistant should read back the result and distinguish a draft from a published widget.

## 4. Repeat with a real next task

On another day, choose the next product or a changed collection. Run the same check and compare the returned assets and placement. Keep the product, selected asset IDs, and the decision you made. A connection check or empty result is useful diagnosis, but it does not establish a completed media workflow.

## If something blocks you

| What you see | Next step |
| --- | --- |
| An administrator approved Tolstoy, but you cannot use it | Add or enable the connector in your own client account and complete Tolstoy sign-in. Ask your administrator if the connector is not available to your account. |
| A different brand or store | Reconnect to the correct Tolstoy workspace before reading or changing its assets. |
| Missing or old tools | Refresh tool discovery. If the client still caches an old tool list, create a new named connection and inspect it again. |
| Catalog import in progress | Wait for the import to finish, then check the named product again. |
| An integration needs attention | Reconnect the named service in Tolstoy and retry the relevant read. |
| No suitable video | Pick another existing asset or import your own approved media. The assistant should explain the gap without inventing content. |
| No inline preview | Use the preview links or open the asset in Tolstoy. A text response does not prove the client rendered the media. |

For support, share the client name, store domain, tool name, time of the failure, and the error text with [support@gotolstoy.com](mailto:support@gotolstoy.com). Do not include access tokens or customer secrets.

See [reporting and connection recovery](reporting-and-recovery.md) for reporting scope, Meta Ads setup, and browser uploads.
