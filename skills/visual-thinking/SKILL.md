---
name: art-visual-thinking
description: Visual thinking expertise. USE WHEN determining the best visual format for content, choosing between code-rendered vs AI-generated visuals, or needing guidance on concept-to-visual routing.
---

# Art Visual Thinking Skill

Concept-to-visual routing expertise. Analyzes content and selects the optimal visualization approach.

## When to Generate vs When to Code

### Use AI-Generated Images (Generate.ts)
- Editorial illustrations with artistic style
- Blog headers and conceptual visuals
- Infographics with visual metaphors
- Content requiring artistic interpretation
- Anything needing the charcoal sketch aesthetic

### Use Code-Rendered Visuals
- Data with precise numbers requiring accurate charts
- Interactive visualizations (use `/art:d3`)
- Flowcharts with exact logic (use `/art:flowchart` for AI-rendered OR code for interactive)
- Diagrams that need to be editable programmatically

## Visual Format Selection

| Content Type | Best Format | Command |
|---|---|---|
| Process or workflow | Flowchart/sequence | `/art:flowchart` |
| Data comparison | Stat card or comparison | `/art:stat` or `/art:comparison` |
| Conceptual relationships | Framework or map | `/art:framework` or `/art:map` |
| Time-based progression | Timeline | `/art:timeline` |
| Classification system | Taxonomy | `/art:taxonomy` |
| Step-by-step guide | Recipe card | `/art:recipe` |
| Architecture diagram | Technical diagram | `/art:diagram` |
| Interactive data | D3 dashboard | `/art:d3` |
| Blog header / editorial | Essay illustration | `/art:generate` |
| Multi-dimensional content | Adaptive visualization | `/art:visualize` |
| Quote or aphorism | Quote card | `/art:aphorism` |
| Comic/narrative | Comic panels | `/art:comic` |
| Real screenshot + notes | Annotated screenshot | `/art:annotate` |
| YouTube thumbnail | Thumbnail | `/art:thumbnail` |

## Routing Decision Protocol

1. **Analyze content type** — What information needs to be conveyed?
2. **Identify primary dimension** — Is it primarily data, narrative, conceptual, or process?
3. **Check if single-mode** — Does it clearly fit one format? → Use that command
4. **Check for hybrid** — Multiple dimensions? → Use `/art:visualize` to orchestrate
5. **Route to command** — Execute the appropriate `/art:` command

## When Unsure

If the content type is ambiguous or multi-dimensional, always default to `/art:visualize` — the adaptive orchestrator that analyzes content and selects the optimal approach automatically.
