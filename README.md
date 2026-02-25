# CG Claude Workspaces Plugins

[![CI](https://github.com/MarkAC007/cg-claude-workspaces-plugins/actions/workflows/ci.yml/badge.svg)](https://github.com/MarkAC007/cg-claude-workspaces-plugins/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub issues](https://img.shields.io/github/issues/MarkAC007/cg-claude-workspaces-plugins)](https://github.com/MarkAC007/cg-claude-workspaces-plugins/issues)
[![GitHub stars](https://img.shields.io/github/stars/MarkAC007/cg-claude-workspaces-plugins?style=social)](https://github.com/MarkAC007/cg-claude-workspaces-plugins/stargazers)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/MarkAC007/cg-claude-workspaces-plugins/pulls)
[![Last commit](https://img.shields.io/github/last-commit/MarkAC007/cg-claude-workspaces-plugins)](https://github.com/MarkAC007/cg-claude-workspaces-plugins/commits/master)
[![Built for Claude Code](https://img.shields.io/badge/Built%20for-Claude%20Code-blue?logo=anthropic)](https://claude.ai/code)

Private monorepo marketplace of Claude Code plugins for ComplianceGenie workflows.

## Structure

```
cg-claude-workspaces-plugins/
├── .claude-plugin/
│   └── marketplace.json          ← Marketplace catalog
├── plugins/
│   └── marketing/
│       └── art/                  ← Visual content plugin
│           ├── commands/         ← 22 slash commands (/art:*)
│           ├── skills/           ← Ambient skills
│           ├── tools/            ← TypeScript generation tools
│           └── lib/              ← Discord/Midjourney libraries
└── README.md
```

## Installing the Marketplace

### Local (Mark's machine)

```bash
claude plugin marketplace add ~/GitHub/cg-claude-workspaces-plugins
claude plugin install art@cg-plugins
```

### Another machine / team member

```bash
claude plugin marketplace add MarkAC007/cg-claude-workspaces-plugins
claude plugin install art@cg-plugins
```

Requires `gh auth login` to be configured — GitHub CLI handles authentication transparently for private repos.

## Development / Testing (no install needed)

```bash
claude --plugin-dir ~/GitHub/cg-claude-workspaces-plugins/plugins/marketing/art
```

Loads the plugin directly without install or restart.

## Available Plugins

| Plugin | Category | Commands | Description |
|--------|----------|----------|-------------|
| `art` | marketing | 22 `/art:*` | Visual content — illustrations, diagrams, thumbnails, infographics |

## Adding New Plugins

1. Create `plugins/<category>/<name>/` with plugin structure
2. Add entry to `.claude-plugin/marketplace.json`
3. PR → merge → users update with `claude plugin update`
