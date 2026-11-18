# ATR Security Scan

Scan AI agent skills and MCP tool descriptions for security threats.

Runs the latest [agent-threat-rules](https://www.npmjs.com/package/agent-threat-rules) release from npm, so the rule set is always the current one. ATR rules also ship inside Cisco AI Defense skill-scanner.

## Quick Start

```yaml
name: ATR Security Scan
on: [pull_request]
jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: panguard-ai/atr-action@v1
```

Results appear in GitHub's **Security** tab as code scanning alerts.

## Inputs

| Input | Default | Description |
|-------|---------|-------------|
| `path` | `.` | Path to scan |
| `severity` | `medium` | Minimum severity (critical, high, medium, low) |
| `fail-on-findings` | `false` | Fail the action if findings detected |
| `sarif` | `true` | Upload SARIF to GitHub Security tab |

## What It Scans

- `SKILL.md` files (AI agent skill definitions)
- `mcp.json` / `mcp-config.json` (MCP server configurations)
- Any `.skill.md` file

## What It Detects

Every rule in the latest ATR release (current count in [stats.json](https://raw.githubusercontent.com/Agent-Threat-Rule/agent-threat-rules/main/data/stats.json)), including:

- Prompt injection (identity override, system prompt manipulation)
- Tool poisoning (malicious tool descriptions, response injection)
- Credential theft (SSH key exfiltration, API token harvesting)
- Data exfiltration (DNS tunneling, wallet theft, browser data)
- Privilege escalation (sudo abuse, SUID manipulation)
- Supply chain attacks (typosquatting, rug pull, version spoofing)

Full rule list: [agentthreatrule.org/rules](https://agentthreatrule.org/en/rules)

## Example: Block Critical Findings

```yaml
- uses: panguard-ai/atr-action@v1
  with:
    fail-on-findings: 'true'
    severity: 'critical'
```

## Example: Scan Specific Directory

```yaml
- uses: panguard-ai/atr-action@v1
  with:
    path: './skills'
```

## Links

- [ATR Website](https://agentthreatrule.org)
- [ATR Rules](https://github.com/Agent-Threat-Rule/agent-threat-rules)
- [Threat Feed](https://agentthreatrule.org/en/threats)
- [RFC-001 Quality Standard](https://agentthreatrule.org/en/quality-standard)

## License

MIT
