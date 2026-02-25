# Council Plugin

Multi-agent debate system where specialized agents (Architect, Designer, Engineer, Researcher) discuss topics in rounds, respond to each other's points, and surface insights through intellectual friction. Best decisions emerge from diverse perspectives genuinely challenging each other.

**Key differentiator from Red Team:** Council is collaborative-adversarial (debate to find best path). Red Team is purely adversarial (attack the idea).

## Commands

| Command | Description |
|---------|-------------|
| `/council:debate` | Full 3-round structured debate with visible transcript and synthesis |
| `/council:quick` | Fast single-round perspective check (10-20 seconds) |

## When to Use Which

- **debate**: Important decisions with real trade-offs — architectural choices, feature design, strategy
- **quick**: Sanity checks before committing — "Is this API design reasonable?"

## Install

```bash
claude plugin add ~/GitHub/cg-claude-workspaces-plugins/plugins/research/council
```
