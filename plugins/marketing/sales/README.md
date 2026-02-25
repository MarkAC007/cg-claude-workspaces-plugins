# Sales Plugin

Transform product documentation into compelling sales narratives with talking points, elevator pitches, and visual concepts. Focuses on value-driven storytelling that sales teams can use immediately.

## Commands

| Command | Description |
|---------|-------------|
| `/sales:create-narrative` | Transform product docs into a sales narrative with talking points and elevator pitch |
| `/sales:create-package` | Full pipeline: narrative + emotional register + visual concept brief |

## Notes

- `/sales:create-package` produces a visual brief (scene, subjects, emotion) but does not generate images. Use the Art plugin for image generation.
- Both commands strip technical jargon and focus on customer value.

## Prerequisites

No external dependencies.

## Install

```bash
claude plugin add ~/GitHub/cg-claude-workspaces-plugins/plugins/marketing/sales
```
