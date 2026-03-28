# ATR Security Scan — GitHub Action

Scan MCP servers for prompt injection, credential theft, and supply chain threats in CI. 71 detection rules. OWASP Agentic Top 10 full coverage. One file. No source code changes.

## Quick Start

```yaml
# .github/workflows/atr-security-scan.yml
name: Security Scan
on: [push, pull_request]
jobs:
  atr-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: panguard-ai/atr-action@v1
```

## What It Checks

- Prompt injection patterns in tool descriptions and responses
- Credential exposure (API keys, tokens, secrets in tool output)
- Supply chain risk indicators (postinstall scripts, typosquatting signals)
- Tool poisoning (hidden instructions, consent bypass, trust escalation)
- 71 ATR rules covering all 10 OWASP Agentic Top 10 categories

## Options

| Input | Default | Description |
|-------|---------|-------------|
| path | . | Path to scan |
| fail-on-critical | false | Fail the workflow if CRITICAL threats are found |
| report-to-cloud | false | Share anonymous scan results with Threat Cloud (no source code sent) |

## Outputs

| Output | Description |
|--------|-------------|
| findings-critical | Number of CRITICAL findings |
| findings-high | Number of HIGH findings |
| findings-medium | Number of MEDIUM findings |
| findings-total | Total findings count |
| risk-score | Overall risk score (0-100) |

## Threat Cloud (Collective Defense)

Set `report-to-cloud: true` to anonymously share scan results with Threat Cloud. Every scan makes the detection network stronger for everyone.

What gets sent: severity counts + content hash. What never gets sent: source code, file paths, repo name.

```yaml
- uses: panguard-ai/atr-action@v1
  with:
    report-to-cloud: 'true'
```

## Examples

Fail CI on critical findings:

```yaml
- uses: panguard-ai/atr-action@v1
  with:
    fail-on-critical: 'true'
```

Scan a specific directory:

```yaml
- uses: panguard-ai/atr-action@v1
  with:
    path: './src/mcp-server'
```

Use outputs in subsequent steps:

```yaml
- uses: panguard-ai/atr-action@v1
  id: security
- run: echo "Found ${{ steps.security.outputs.findings-critical }} critical issues"
```

## Badge

Add to your README:

```markdown
[![ATR Security Scan](https://img.shields.io/badge/ATR-scanned-brightgreen?style=flat-square)](https://github.com/Agent-Threat-Rule/agent-threat-rules)
```

## About ATR

ATR (Agent Threat Rules) is an open-source detection ruleset for AI agent security threats. 71 YAML-based rules. Engine-agnostic. MIT licensed.

- 62.7% recall, 99.7% precision on PINT benchmark (850 adversarial samples)
- Scanned 36,394 MCP skills from ClawHub ecosystem
- OWASP Agentic Top 10: 10/10 categories covered
- SAFE-MCP: 78/85 techniques covered (91.8%)
- Paper: https://doi.org/10.5281/zenodo.19178002

Repository: https://github.com/Agent-Threat-Rule/agent-threat-rules
Website: https://panguard.ai

## License

MIT
