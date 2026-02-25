# Art Plugin for Claude Code

Complete visual content system for Claude Code Desktop. A knowledge-work plugin that replicates the PAI Art skill — same workflows, same models, same behaviour.

## What It Does

Generates editorial illustrations, technical diagrams, infographics, YouTube thumbnails, and visual assets using four AI models:

| Model | Flag | Best For |
|---|---|---|
| **Nano Banana Pro** (Gemini 3 Pro) | `--model nano-banana-pro` | Default — best quality + text rendering |
| **Nano Banana** (Gemini Flash) | `--model nano-banana` | Fast iteration and drafts |
| **Flux 1.1 Pro** | `--model flux` | Stylistic variety |
| **GPT-image-1** | `--model gpt-image-1` | Alternative interpretation |
| **Midjourney** | `/art:midjourney` | Photorealistic / maximally stylized |

All images output to `~/Downloads/` first for review — never directly to project dirs.

## Prerequisites

- **Bun** — `brew install oven-sh/bun/bun`
- **ImageMagick** — `brew install imagemagick`
- **WebP tools** — `brew install webp`
- **API Keys** — See [SETUP.md](SETUP.md)

## Installation

```bash
# 1. Clone or place this repo at ~/dev/cg-claude-workspaces-plugins/
git clone <repo-url> ~/dev/cg-claude-workspaces-plugins/

# 2. Install tool dependencies
cd ~/dev/cg-claude-workspaces-plugins/tools && bun install

# 3. Configure API keys (see SETUP.md)
cp .env.example ~/.claude/.env
# Edit ~/.claude/.env with your actual keys

# 4. Install the plugin
claude plugin install ~/dev/cg-claude-workspaces-plugins/
```

## Available Commands

| Command | Description |
|---|---|
| `/art:generate` | Blog headers and editorial illustrations (charcoal sketch style) |
| `/art:visualize` | Adaptive multi-modal visualization |
| `/art:diagram` | Clean Excalidraw-style architecture diagrams |
| `/art:flowchart` | Mermaid-style flowcharts and sequence diagrams |
| `/art:comparison` | X vs Y split compositions |
| `/art:timeline` | Chronological progressions with illustrated milestones |
| `/art:framework` | 2x2 matrices, Venn diagrams, mental models |
| `/art:taxonomy` | Classification grids and periodic tables |
| `/art:comic` | 3-4 panel editorial comic strips |
| `/art:aphorism` | Quote cards with typography-hero design |
| `/art:stat` | Single-stat illustrated cards |
| `/art:map` | Conceptual territory maps |
| `/art:recipe` | Step-by-step process recipe cards |
| `/art:annotate` | Annotated screenshots with hand-drawn overlays |
| `/art:d3` | Interactive D3.js data dashboards |
| `/art:thumbnail` | YouTube thumbnails (1280x720) |
| `/art:thumbnail-checklist` | YouTube thumbnail validation |
| `/art:remove-bg` | Background removal from images |
| `/art:wallpaper` | Branded 4K wallpapers |
| `/art:pack-icon` | PAI pack icons (256x256 transparent) |
| `/art:embossed-logo` | Embossed logo wallpapers |
| `/art:midjourney` | Midjourney via Discord |

## Ambient Skills

The plugin includes two ambient skills that activate automatically:

- **art-generation** — Routes visual content requests to the appropriate `/art:` command
- **art-visual-thinking** — Provides concept-to-visual format selection guidance

This means you can just say "create a header image for my blog post" without needing to know the specific command — the generation skill will route it to `/art:generate` automatically.

## Directory Structure

```
cg-claude-workspaces-plugins/
├── .claude-plugin/plugin.json    # Plugin manifest
├── .mcp.json                     # MCP configuration (empty)
├── .env.example                  # API key template
├── commands/                     # 22 slash commands
├── skills/
│   ├── generation/SKILL.md       # Ambient: routes visual requests
│   └── visual-thinking/SKILL.md  # Ambient: concept-to-visual routing
├── tools/                        # Bundled TypeScript tools
│   ├── Generate.ts               # Multi-model image generation CLI
│   ├── ComposeThumbnail.ts       # YouTube thumbnail compositor
│   ├── GenerateMidjourneyImage.ts # Midjourney via Discord
│   └── ...
└── lib/                          # Library dependencies (Discord, Midjourney)
```

## If Plugin Is Installed Elsewhere

The command files reference `~/dev/cg-claude-workspaces-plugins/tools/`. If you install at a different path, update the tool paths in all `commands/*.md` files:

```bash
# Find and replace the path (adjust NEW_PATH):
find ~/your-install-path/commands -name "*.md" -exec \
  sed -i '' 's|~/dev/cg-claude-workspaces-plugins/tools/|~/your-install-path/tools/|g' {} \;
```

## API Keys

See [SETUP.md](SETUP.md) for API key configuration.
