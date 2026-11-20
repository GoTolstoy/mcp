# Changelog

## 1.3.1 (Cursor) and 1.2.4 (Claude) - 2026-11-20

- The Cursor rule is now `rules/use-tolstoy.md`, the `.md` form Cursor also reads, so the repository has no `.mdc` file. Its text is unchanged.
- README: which files each client reads.

## 1.3.0 - 2026-11-19

Cursor plugin:

- The description says what Tolstoy does (images and videos from the store's products, the media library, store analytics) and names the platforms the Tolstoy Agent reaches once a brand connects them in Tolstoy. The keywords name those platforms, what brands ask for, and Tolstoy's own product.
- New skill `cursor/skills/tolstoy-connectors`, which reaches connected platforms through `run_agent` and lists what each connector covers. The Cursor plugin ships it with the existing `ecommerce-analytics` and `tolstoy-product-media` skills.
- New always-on rule `rules/use-tolstoy.md` (first shipped as `.mdc`) and agent `cursor/agents/tolstoy-commerce-agent.md`. The rule routes requests for the brand's own data or actions in a connected platform to `tolstoy-connectors` and `run_agent`, leaves Tolstoy's own tools as they are, and excludes code that integrates with a platform, general questions about a platform, and platforms the client has its own connector for.
- The manifest points at its skills (`skills/` and `cursor/skills/`), rules, agent and the root `mcp.json` (`type: http`). `.cursor-plugin/mcp.json` is removed.
- Listing icon `assets/icon.png` (512×512).
- Added `SECURITY.md` and this changelog.

The Claude plugin (`.claude-plugin/plugin.json`, `.mcp.json`, `skills/`) is unchanged.

## 1.2.3

- `ecommerce-analytics` skill, and analytics in the plugin listings.

## 1.0.0

- Initial Cursor Marketplace plugin: the Tolstoy workspace MCP server over OAuth.
