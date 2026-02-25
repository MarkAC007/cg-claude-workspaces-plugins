---
name: art-generation
description: Complete visual content system. USE WHEN user wants to create visual content, illustrations, diagrams, OR mentions art, header images, visualizations, mermaid, flowchart, technical diagram, infographic, icon, thumbnail, wallpaper, or any visual creation.
---

# Art Generation Skill

Complete visual content system for creating illustrations, diagrams, and visual content.

## Customization

**Before executing, check for user customizations at:**
`~/.claude/skills/PAI/USER/SKILLCUSTOMIZATIONS/Art/`

If this directory exists, load and apply:
- `PREFERENCES.md` - Aesthetic preferences, default model, output location
- `CharacterSpecs.md` - Character design specifications
- `SceneConstruction.md` - Scene composition guidelines

These override default behavior. If the directory does not exist, proceed with skill defaults.

## 🚨 MANDATORY: Voice Notification (REQUIRED BEFORE ANY ACTION)

**You MUST send this notification BEFORE doing anything else when this skill is invoked.**

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running the WORKFLOWNAME workflow in the Art skill to ACTION"}' \
  > /dev/null 2>&1 &
```

**This is not optional. Execute this curl command immediately upon skill invocation.**

## 🚨🚨🚨 MANDATORY: Output to Downloads First 🚨🚨🚨

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️  ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST                   ⚠️
⚠️  NEVER output directly to project directories                    ⚠️
⚠️  User MUST preview in Finder/Preview before use                  ⚠️
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**This applies to ALL workflows in this skill.**

## Workflow Routing

Route to the appropriate `/art:` command based on the request:

| Request Type | Command |
|---|---|
| Remove background from image | `/art:remove-bg` |
| Branded wallpaper with logo integration | `/art:wallpaper` |
| Blog header or editorial illustration | `/art:generate` |
| D3.js interactive chart or dashboard | `/art:d3` |
| Visualization or unsure which format | `/art:visualize` |
| Mermaid flowchart or sequence diagram | `/art:flowchart` |
| Technical or architecture diagram | `/art:diagram` |
| Taxonomy or classification grid | `/art:taxonomy` |
| Timeline or chronological progression | `/art:timeline` |
| Framework or 2x2 matrix | `/art:framework` |
| Comparison or X vs Y | `/art:comparison` |
| Annotated screenshot | `/art:annotate` |
| Recipe card or step-by-step | `/art:recipe` |
| Aphorism or quote card | `/art:aphorism` |
| Conceptual map or territory | `/art:map` |
| Stat card or big number visual | `/art:stat` |
| Comic or sequential panels | `/art:comic` |
| YouTube thumbnail (generate from content) | `/art:thumbnail` |
| YouTube thumbnail validation | `/art:thumbnail-checklist` |
| PAI pack icon | `/art:pack-icon` |
| Embossed logo wallpaper | `/art:embossed-logo` |
| Midjourney image generation | `/art:midjourney` |

## Default Model

**Default:** `nano-banana-pro` (Gemini 3 Pro) — best quality + text rendering.

Check `~/.claude/skills/PAI/USER/SKILLCUSTOMIZATIONS/Art/PREFERENCES.md` for user-configured default.

## Core Tools

All image generation uses:
```bash
bun run ~/dev/cg-claude-workspaces-plugins/tools/Generate.ts [FLAGS]
```

YouTube thumbnails use:
```bash
bun run ~/dev/cg-claude-workspaces-plugins/tools/ComposeThumbnail.ts [FLAGS]
```

Midjourney uses:
```bash
bun run ~/dev/cg-claude-workspaces-plugins/tools/GenerateMidjourneyImage.ts [FLAGS]
```

**API keys loaded from:** `~/.claude/.env` (fallback) or `~/dev/cg-claude-workspaces-plugins/.env`
