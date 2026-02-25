# Evals Plugin

AI agent evaluation framework based on Anthropic's best practices. Create evaluation use cases, design LLM-as-Judge scorers, run A/B prompt tests, and compare models. Supports three grader types: code-based (deterministic), model-based (nuanced), and human (calibration).

## Commands

| Command | Description |
|---------|-------------|
| `/evals:create-use-case` | Create a new evaluation use case with test cases and scoring criteria |
| `/evals:create-judge` | Design a custom LLM-as-Judge for evaluating AI outputs |
| `/evals:run-eval` | Execute an evaluation suite against test cases |
| `/evals:compare-prompts` | A/B test two prompt versions using the Science Protocol |
| `/evals:compare-models` | Compare multiple models on the same prompt |
| `/evals:view-results` | Query and display evaluation results and trends |

## Notes

- Commands guide the evaluation process conceptually and produce YAML config files
- Results are stored as JSON in `Results/<use-case>/` directories
- TypeScript evaluation tooling requires local PAI setup

## Prerequisites

No external API keys required for the command guidance workflows.

## Install

```bash
claude plugin add ~/GitHub/cg-claude-workspaces-plugins/plugins/dev-tools/evals
```
