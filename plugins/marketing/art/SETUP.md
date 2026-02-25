# Art Plugin — API Key Setup

## Where to Add Keys

Add API keys to `~/.claude/.env`. The plugin tools automatically load from this file.

```bash
# Open for editing
nano ~/.claude/.env
```

If `~/.claude/.env` doesn't exist, create it:
```bash
cp ~/dev/cg-claude-workspaces-plugins/.env.example ~/.claude/.env
# Then edit with your actual keys
```

## Required Keys

### GOOGLE_API_KEY
**Required for:** `nano-banana-pro` (default model — Gemini 3 Pro)

Get from: [Google AI Studio](https://aistudio.google.com/app/apikey)

```bash
GOOGLE_API_KEY=AIza...
```

### REPLICATE_API_TOKEN
**Required for:** `flux` and `nano-banana` models

Get from: [replicate.com/account/api-tokens](https://replicate.com/account/api-tokens)

```bash
REPLICATE_API_TOKEN=r8_...
```

### OPENAI_API_KEY
**Required for:** `gpt-image-1` model

Get from: [platform.openai.com/api-keys](https://platform.openai.com/api-keys)

```bash
OPENAI_API_KEY=sk-...
```

### REMOVEBG_API_KEY
**Required for:** `--remove-bg` flag and `/art:remove-bg` command

Get from: [remove.bg/api](https://www.remove.bg/api)

```bash
REMOVEBG_API_KEY=...
```

## Optional Keys (Midjourney Only)

These are only required for the `/art:midjourney` command.

### DISCORD_BOT_TOKEN
A Discord bot with access to a channel where the Midjourney bot is active.

```bash
DISCORD_BOT_TOKEN=...
```

### MIDJOURNEY_CHANNEL_ID
The Discord channel ID where Midjourney is configured.

```bash
MIDJOURNEY_CHANNEL_ID=...
```

## Complete ~/.claude/.env Example

```bash
# Core image generation models
GOOGLE_API_KEY=AIza...
REPLICATE_API_TOKEN=r8_...
OPENAI_API_KEY=sk-...

# Background removal
REMOVEBG_API_KEY=...

# Midjourney (optional)
DISCORD_BOT_TOKEN=...
MIDJOURNEY_CHANNEL_ID=...
```

## System Dependencies

```bash
# ImageMagick — required for thumbnail composition and image optimization
brew install imagemagick

# WebP tools — required for WebP conversion in blog header workflow
brew install webp

# Verify
magick --version
cwebp --version
```

## Verify Setup

After adding keys, test the default model:

```bash
cd ~/dev/cg-claude-workspaces-plugins/tools
bun run Generate.ts --model nano-banana-pro --prompt "test" --size 1K --output /tmp/test.png
```

Expected: `/tmp/test.png` created successfully.

## Troubleshooting

**"GOOGLE_API_KEY not found"** — Check that `~/.claude/.env` exists and contains the key without extra spaces or quotes.

**"REPLICATE_API_TOKEN not found"** — Same as above for Replicate token.

**`magick: command not found`** — Run `brew install imagemagick`.

**`cwebp: command not found`** — Run `brew install webp`.

**Midjourney timeout** — Verify the Discord bot has permissions in the Midjourney channel and the channel ID is correct.
