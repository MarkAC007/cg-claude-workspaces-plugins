# Council Plugin — Setup

## Prerequisites

- Claude Code with Task tool access (required for parallel agent deployment)

## No Additional Setup Required

This plugin uses Claude Code's built-in Task tool to spawn parallel agents for council members. No API keys, no additional dependencies, no installation steps beyond adding the plugin.

## Install

```bash
claude plugin add ~/GitHub/cg-claude-workspaces-plugins/plugins/research/council
```

## Usage

```
/council:debate Should we use WebSockets or SSE for real-time updates?
/council:quick Is this API design reasonable?
```
