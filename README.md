# ATR Security Scan

Scan AI agent skills and MCP tool descriptions for security threats.

113 rules. 96K skills scanned. 751 malware discovered. Shipped in Cisco AI Defense.

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

113 detection rules across 9 threat categories:

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
