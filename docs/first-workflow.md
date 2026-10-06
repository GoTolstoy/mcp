# Your first useful Tolstoy workflow

Use Tolstoy to find the existing media for one product, then create new content for it. You will finish with a media shortlist and a Studio draft you can review.

## 1. Connect your workspace

| Client and scope | Remote MCP endpoint |
| --- | --- |
| Cursor: full Tolstoy workspace | `https://apilb.gotolstoy.com/mcp/v1/mcp` |
| Claude: Tolstoy Library | `https://apilb.gotolstoy.com/mcp/v1/library/mcp` |

In the client's connector or MCP settings, add the endpoint and complete the Tolstoy sign-in for your workspace. Your team may need to approve the connector first. Each person must also finish their own connection. A team approval or another person's successful sign-in does not establish yours.

The Library endpoint covers existing media and the product catalog. It does not expose Studio generation.

For client-specific installation steps, use **Settings → MCP** in Tolstoy. The [Cursor plugin](../.cursor-plugin/plugin.json) includes the workspace connection and the `tolstoy-product-media` skill.

## 2. Find the product and its media

Replace the product name in this prompt:

> Find [product name] in my Tolstoy store. Then find up to five existing Tolstoy library videos or images for it. Inspect their details and product tags. Give me the exact media IDs, available preview links, why each fits, and anything you could not verify. Do not change anything.

Confirm that the product comes from your intended store. If it does not, disconnect and sign in to the correct workspace. Review the actual media and choose the items you want to use.

## 3. Create new content

With the full workspace connection, ask:

> Create a product video for [product name] with Tolstoy Studio. Use the product from my store and the library media I chose. Show me the result and the chat ID.

Studio returns a draft. Continue the same chat to revise it. A draft stays in Studio until you publish it in Tolstoy.

## If something blocks you

| What you see | Next step |
| --- | --- |
| An administrator approved Tolstoy, but you cannot use it | Add or enable the connector in your own client account and complete Tolstoy sign-in. Ask your administrator if the connector is not available to your account. |
| A different brand or store | Reconnect to the correct Tolstoy workspace before reading or changing its media. |
| Missing or old tools | Refresh tool discovery. If the client still caches an old tool list, create a new named connection and inspect it again. |
| No Studio tools | You are on the Library connection. Connect the full workspace endpoint to create content. |
| No suitable media | Upload your own approved media with the Tolstoy upload panel, or create new content in Studio. The assistant should explain the gap without inventing content. |
| No inline preview | Use the preview links or open the media in Tolstoy. A text response does not prove the client rendered the media. |

For support, share the client name, store domain, tool name, time of the failure, and the error text with [support@gotolstoy.com](mailto:support@gotolstoy.com). Do not include access tokens or customer secrets.
