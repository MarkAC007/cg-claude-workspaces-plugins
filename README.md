# CG Claude Workspaces Plugins

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
claude plugin marketplace add ~/dev/cg-claude-workspaces-plugins
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
claude --plugin-dir ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art
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
