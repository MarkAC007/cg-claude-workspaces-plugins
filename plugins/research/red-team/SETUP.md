# Red Team Plugin — Setup

## Prerequisites

- Claude Code with Task tool access (required for parallel agent deployment)

## No Additional Setup Required

This plugin uses Claude Code's built-in Task tool to spawn parallel agents. No API keys, no additional dependencies, no installation steps beyond adding the plugin.

## Install

```bash
claude plugin add ~/GitHub/cg-claude-workspaces-plugins/plugins/research/red-team
```

## Usage

```
/red-team:parallel-analysis [paste your argument/idea here]
/red-team:adversarial-validation [describe the decision or design problem]
```
