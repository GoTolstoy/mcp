# Security policy

Please report suspected vulnerabilities privately to [rnd@gotolstoy.com](mailto:rnd@gotolstoy.com) with the subject **Security report**. Do not open a public issue for a security report.

Include the affected file, endpoint or behavior, steps to reproduce, and any relevant logs with secrets and customer data removed. We will acknowledge the report and coordinate a fix and disclosure with you.

The Tolstoy MCP servers use OAuth 2.1 with PKCE, so this repository needs no API key. Never commit access tokens, platform credentials or customer data to it. Platforms reached through Tolstoy are connected in the Tolstoy platform under Settings > Connectors, and their credentials stay there.

For Tolstoy's wider security practices, see [gotolstoy.com/security](https://www.gotolstoy.com/security).
