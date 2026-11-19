# Changelog

## 1.3.0 - 2026-11-19

Cursor plugin:

- The description and keywords name the platforms a brand can connect in Tolstoy, and say how they are reached: connect the platform under Settings > Connectors in Tolstoy, then ask the Tolstoy Agent through the `run_agent` tool. The old image and video creation wording is gone.
- New skills in `cursor/skills/`: `tolstoy-connectors`, and one skill per platform group (social and video, paid ads, customer support, reviews and UGC, email and SMS, store and attribution analytics, search and merchandising, loyalty, returns and shipping, catalog and feeds, brand assets and team tools). Each lists which platforms have been tested through `run_agent`.
- New always-on rule `rules/use-tolstoy.mdc` and agent `cursor/agents/tolstoy-commerce-agent.md`.
- The manifest points at its skills, rules, agents and the root `mcp.json` (`type: http`). `.cursor-plugin/mcp.json` is removed.
- Listing icon `assets/icon.png` (512×512).
- Added `SECURITY.md`, `.github/CODEOWNERS` and this changelog.

The Claude plugin (`.claude-plugin/plugin.json`, `.mcp.json`, `skills/`) is unchanged.

## 1.2.3

- `ecommerce-analytics` skill, and analytics in the plugin listings.

## 1.0.0

- Initial Cursor Marketplace plugin: the Tolstoy workspace MCP server over OAuth.
