# Instructions for agents working in this repository

This public repository holds the Tolstoy MCP server listing for several clients at once. Claude, Cursor, the MCP Registry and other public stores read the default branch (`main`), so a merge goes live for all of them. Check every change against each client below before merging.

## Which files each client reads

| Client | Reads | Notes |
| --- | --- | --- |
| Claude plugin directory | `.claude-plugin/plugin.json`, `.mcp.json`, `skills/`, plus every other file in the repository | The plugin folder is the repository root. That was set at submission and can't be changed without a new submission. |
| Cursor Marketplace | `.cursor-plugin/plugin.json`, `mcp.json`, `skills/`, `cursor/skills/`, `cursor/agents/`, `rules/`, `assets/icon.png` | Reviews the default branch. Paths are set in the manifest. |
| MCP Registry | `registry/tolstoy.server.json`, `registry/closet.server.json` | Published manually by `.github/workflows/publish-mcp-registry.yml`. |
| Glama | `glama.json` | |
| Cline and other MCP directories | `README.md`, `llms-install.md`, `mcp.json` | |

The MCP server itself is `https://apilb.gotolstoy.com/mcp/v1/mcp`. Nothing in this repository deploys it.

## Why the tree looks like this

- **The Claude plugin is the repository root, so Anthropic's directory checks every file.** For organizations that aren't Verified, the directory's policy refuses any file outside its allowed list:
  - Allowed: Markdown, plain text, JSON, YAML, and PNG, JPEG, GIF, WebP or ICO images.
  - Not allowed: files that start with `#!`, package-manager config files, `.claude/skills` folders, and any file in `.claude-plugin/` other than `plugin.json`.
  - From the policy: "An `.svg` other than the plugin's icon isn't accepted: use a PNG." "A license, a readme, .gitignore, and the plugin's icon can stay." "If your repository needs other files, or holds other plugins, put the plugin in a subfolder and submit that folder."
  - 1.2.3 was refused for `rules/use-tolstoy.mdc` and `assets/logo.svg`. 1.2.4 renamed the rule to `.md`, and 1.2.5 deleted the SVG. `assets/logo.png` is the same image as a PNG.
  - Also keep each file under 256 KiB, and never use `export-ignore` or `export-subst` in `.gitattributes`.
  - The directory also shows warnings that don't block a version. These include a download-and-run command in `.github/workflows/publish-mcp-registry.yml`, which it says "can be held or refused". Don't add more files like that.
- **Cursor-only skills and agents live under `cursor/`.** Claude Code loads `skills/` and `agents/` at the root, so anything there ships in the Claude plugin too. `skills/` holds only the skills both clients share.
- **Cursor rules are `.md` files with frontmatter (`description`, `alwaysApply`), not `.mdc`.** Cursor reads `.md`, `.mdc` and `.markdown` rules. Only `.md` is safe for the Claude check.
- **One repository serves both plugins.** The Cursor submission and the Claude submission both point at `GoTolstoy/mcp` at the root. Moving either one means a new store submission.

## Before merging

1. Raise `version` in `.claude-plugin/plugin.json` when a change to skills, `.mcp.json` or the manifest should reach Claude users. The directory's refusal notice asks for a new version before it rechecks. Raise `version` in `.cursor-plugin/plugin.json` when Cursor files change. Add a `CHANGELOG.md` entry.
2. Claude: `claude plugin validate ./`. Warnings for `icon`, `documentationUrl`, `supportUrl`, `privacyPolicyUrl` and `termsOfServiceUrl` are expected on older CLI versions; the directory reads these fields, so keep them.
3. Cursor: validate against the schema, then check that every manifest path exists:
   ```sh
   curl -fsSLo /tmp/cursor-plugin.schema.json https://raw.githubusercontent.com/cursor/plugins/main/schemas/plugin.schema.json
   npx --yes --package ajv-cli@5 --package ajv-formats@3 ajv validate --spec=draft7 -s /tmp/cursor-plugin.schema.json -d .cursor-plugin/plugin.json -c ajv-formats
   for p in $(jq -r '[.logo,.skills,.agents,.rules,.mcpServers]|flatten|.[]' .cursor-plugin/plugin.json); do test -e "$p" || echo "missing $p"; done
   ```
4. File types: every tracked file must be an allowed type, must not start with `#!`, and must be UTF-8 text or an image:
   ```sh
   git ls-files | while read -r f; do
     case "$f" in LICENSE|.gitignore|*.md|*.txt|*.json|*.yml|*.yaml|*.png|*.jpg|*.jpeg|*.gif|*.webp|*.ico) ;; *) echo "not allowed: $f";; esac
     [ "$(head -c2 "$f")" = '#!' ] && echo "shebang: $f"
   done
   ```
5. JSON: `jq empty .mcp.json mcp.json glama.json registry/*.json .claude-plugin/plugin.json .cursor-plugin/plugin.json`.
6. Keep `registry/*.server.json` names and paths unchanged unless the workflow changes too.

## Wording

- Describe `run_agent` truthfully. It reaches the platforms a brand connected in Tolstoy (Settings > Connectors). It isn't one direct tool per platform.
- No test-status lines in public files.
- The Cursor description lists the connected platforms first.
