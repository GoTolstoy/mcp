# MCP Audits

This repo runs the Tolstoy MCP capability audit on README and registry copy.

The audit is provided by the private JavaScript package in `GoTolstoy/tolstoy-audit-kit`. Configure the `TOLSTOY_AUDIT_KIT_TOKEN` GitHub Actions secret with read-only access to that private repo before enabling the workflow.

It compares documented MCP claims against the currently supported Tolstoy MCP tools:

- `generate_studio_content`
- `iterate_studio_content`
- `list_assets`
- `search_assets`
- `get_asset`
- `update_asset`

The CI job fails only on clear unsupported claims, such as promising widget creation, widget publishing, or analytics through MCP when no matching tool exists. Softer status wording is reported in the artifact so the docs owner can decide whether to tighten it.

## Run Locally

After installing `tolstoy-audit-kit` with Node.js 20 or newer:

```bash
tolstoy-audit run mcp-capability \
  --source readme=README.md \
  --source mcp-config=mcp.json \
  --source registry-studio=registry/studio.server.json \
  --source registry-library=registry/library.server.json \
  --tools-json audit/tolstoy-mcp-tools.json \
  --out reports/mcp-capability.md \
  --fail-on fail
```

Live Settings -> MCP setup-page checks remain manual/on-demand until that copy is mirrored or exported into a repo.
