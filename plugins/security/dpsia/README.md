# DPSIA Plugin

Data Protection Security Impact Assessment for vendor security evaluation. Combines GDPR DPIA requirements with CIA triad security analysis, integrating with ClickUp or Jira for ticket-driven workflows and saving reports to your GRC vault.

## Commands

| Command | Description |
|---------|-------------|
| `/dpsia:assess` | Full DPSIA for a single vendor — research, CIA triad, risk scoring, report |
| `/dpsia:batch-process` | Process multiple pending DPSIA tickets for a client |

## Assessment Framework

- **Risk scoring:** 5×5 matrix (Likelihood × Impact), thresholds: LOW / MEDIUM / HIGH / CRITICAL
- **Certification bar:** ISO 27001 (required), SOC 2 Type II (required), SOC 2 Type I (conditional)
- **Research sources:** HIBP, GDPR Enforcement Tracker, ICO, FTC, CVE Details, CISA KEV
- **Output:** RAG status (RED/AMBER/GREEN), risk score, Obsidian report, optional Word export to task manager

## Prerequisites

- `GRC_VAULT_PATH` environment variable configured
- Client `Client Overview.md` with `task-system` and `dpsia-workbench-path` fields
- ClickUp or Jira MCP tools configured (per client)
- DocConverter plugin (for Word export)

## Install

```bash
claude plugin add ~/dev/cg-claude-workspaces-plugins/plugins/security/dpsia
```

See [SETUP.md](./SETUP.md) for full configuration instructions.
