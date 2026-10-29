# Fin Codes API MCP server

Connect your AI assistant to banking reference data, payee-name verification, and sanctions screening.

**Hosted endpoint:** `https://mcp.fincodesapi.com/mcp`  
**Transport:** Streamable HTTP  
**Homepage and setup:** https://fincodesapi.com/mcp-server  
**Official registry:** `com.fincodesapi/fincodesapi`

This repository contains public connector configuration and documentation for the hosted service. It does not contain the proprietary backend, run a local server, or publish an npm, PyPI, or Docker package.

## Connect

Add the endpoint as a remote HTTP MCP server in your client, then sign in to your Fin Codes API account through OAuth. Sign up at https://fincodesapi.com/sign-up if needed. OAuth-aware clients do not need a manually created API key.

### Claude Code

```sh
claude mcp add --transport http fincodesapi https://mcp.fincodesapi.com/mcp
```

Run `/mcp` to sign in. In Claude Desktop or claude.ai, add the endpoint as a custom connector.

### VS Code

Add to `.vscode/mcp.json`, then start the server and sign in:

```json
{"servers":{"fincodesapi":{"type":"http","url":"https://mcp.fincodesapi.com/mcp"}}}
```

### Cursor and other MCP clients

Add the remote endpoint in the client's MCP settings. The included `mcp.json` defines the connection; `plugin.json` is a portable Agent Plugins manifest. Client support and OAuth setup vary.

### Gemini CLI

```sh
gemini extensions install https://github.com/swiftcodesapi/fincodesapi-mcp
```

Run `/mcp auth fincodesapi` if prompted to sign in. The extension uses HTTP transport and OAuth discovery.

### API-key clients

Clients without OAuth can use an API key created at https://fincodesapi.com/api-keys. Send `Authorization: Bearer YOUR_API_KEY` to the same endpoint. Store your real key in the client's secret store; never commit it to this repository.

## Eleven tools

| Tool | Purpose |
| --- | --- |
| `lookup_iban` | Validate an IBAN and return bank, country, and BIC/SWIFT details |
| `verify_iban_payee` | Compare a supplied payee name with the holder of a supported European IBAN |
| `lookup_bic` | Resolve BIC/SWIFT bank and branch details |
| `lookup_us_routing_number` | Look up a US ABA routing number |
| `lookup_canada_routing_number` | Look up a Canadian routing number |
| `lookup_australia_bsb` | Look up an Australian BSB |
| `lookup_new_zealand_bank_code` | Look up a New Zealand bank and branch code |
| `lookup_india_ifsc` | Look up an Indian IFSC |
| `lookup_mexico_clabe` | Validate a Mexican CLABE and identify its bank |
| `lookup_argentina_cbu` | Validate an Argentine CBU and identify its bank |
| `screen_sanctions` | Screen a name against EU, UK, UN, OFAC, Swiss, Australian and Canadian sanctions lists |

Live MCP tool schemas are authoritative.

## Examples

- “Validate DE57 1001 0010 0593 9081 19 and tell me its bank and BIC.”
- “Which bank and branch does Australian BSB 082-024 identify?”
- “Run the documented free payee verification fixture: does DE75512108001245126199 match John Doe?”
- “Screen the name Sadam Husein with a minimum match score of 95.”

The John Doe/IBAN pair is a documented test fixture. Its response does not establish real account ownership. Bank-code validity alone does not establish account existence or ownership. Sanctions name similarity requires review and does not establish identity or sanctioned status. The tools do not transfer money, execute trades, reverse-search private accounts by name, or determine creditworthiness.

## Account and pricing

A Fin Codes API account is required. Lookups consume the account's plan quota; payee checks consume prepaid Verification of Payee credits. Plans and credits are purchased on https://fincodesapi.com/pricing. The connector does not process purchases or payments. A trial is available; current terms and limits are shown on the website.

## Privacy and support

Inputs are sent to the hosted Fin Codes API service. Review https://fincodesapi.com/privacy-policy, https://fincodesapi.com/gdpr, and https://fincodesapi.com/terms-of-service before use. Support: andrej@fincodesapi.com or Contact us at https://fincodesapi.com/mcp-server.

## License

The connector configuration and documentation in this repository are MIT licensed. The hosted service remains governed by its Terms of Service.
