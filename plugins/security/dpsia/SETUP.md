# DPSIA Plugin — Setup

## Prerequisites

- Claude Code with MCP tools for ClickUp and/or Jira (configured per client)
- Access to a GRC vault directory (Obsidian or any structured folder)
- DocConverter plugin (for Word export step)

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `GRC_VAULT_PATH` | Yes | Root path of your GRC vault (e.g. `/path/to/GRC/`) |

## Installation

```bash
claude plugin add ~/dev/cg-claude-workspaces-plugins/plugins/security/dpsia
```

Copy `.env.example` to `.env` in your project and fill in `GRC_VAULT_PATH`.

## Client Configuration

Each client requires a `Client Overview.md` at:
```
$GRC_VAULT_PATH/1-clients/[client-name]/Client Overview.md
```

Required frontmatter fields:
```yaml
task-system: clickup   # or jira
dpsia-workbench-path: /path/to/supplier/evaluation/forms
lightrag-endpoint: http://...   # optional — for policy alignment queries
```

## Vault Structure

The plugin expects and creates this structure:
```
$GRC_VAULT_PATH/
└── 1-clients/
    └── [client-name]/
        ├── Client Overview.md
        └── DPSIA/
            ├── [Vendor]-DPSIA-[YYYY-MM-DD].md
            └── Batch-Summary-[YYYY-MM-DD].md
```
