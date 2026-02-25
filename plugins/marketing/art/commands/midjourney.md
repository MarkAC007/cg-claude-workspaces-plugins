# /art:midjourney -- Midjourney Image Generation

## Purpose

Generate images via Midjourney using Discord bot integration. Best for photorealistic renders, maximally stylized artwork, or aesthetics where Midjourney excels over other models. Uses GenerateMidjourneyImage.ts to send prompts to Midjourney through Discord and download the completed result.

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Generate this with Midjourney"
- "I want a photorealistic image of..."
- "Use Midjourney for this"
- "Create something really stylized"
- When photorealism is critical
- When Midjourney-specific aesthetics are desired
- When maximum visual polish is needed
- For images where nano-banana-pro results are not sufficient

---

## Prerequisites

Two environment variables MUST be set in ~/.claude/.env before using this command:

| Variable | Description |
|----------|-------------|
| DISCORD_BOT_TOKEN | Discord bot token with access to the Midjourney channel |
| MIDJOURNEY_CHANNEL_ID | The Discord channel ID where the Midjourney bot is active |

```bash
# Verify env vars are set
source ~/.claude/.env
echo "Bot token set: $([ -n "$DISCORD_BOT_TOKEN" ] && echo YES || echo NO)"
echo "Channel ID set: $([ -n "$MIDJOURNEY_CHANNEL_ID" ] && echo YES || echo NO)"
```

If either variable is missing, the generation will fail. Set them in ~/.claude/.env before proceeding.

---

## Midjourney Prompt Guide

### Prompt Structure

Midjourney prompts are plain text descriptions with optional parameter flags appended at the end.

```
[DESCRIPTION OF DESIRED IMAGE] --ar [RATIO] --v 6.1 [OTHER FLAGS]
```

### Key Parameters

| Parameter | Values | Description |
|-----------|--------|-------------|
| --ar | 16:9, 1:1, 9:16, 4:3, 3:4 | Aspect ratio |
| --v | 6.1 | Model version (use 6.1 for latest) |
| --style | raw | More literal interpretation (less Midjourney "style") |
| --stylize | 0-1000 | Aesthetic level (0 = literal, 1000 = maximum artistic) |
| --chaos | 0-100 | Variation level (higher = more unexpected) |
| --no | [item] | Negative prompt (exclude elements) |
| --q | 0.25, 0.5, 1, 2 | Quality (higher = slower, more detailed) |

### Prompt Tips

- Be descriptive and specific about the scene, lighting, and mood
- Include camera/lens references for photorealistic shots: "shot on Canon EOS R5, 85mm f/1.4"
- Include art style references: "in the style of [artist]", "oil painting", "watercolor"
- Specify lighting: "golden hour lighting", "dramatic chiaroscuro", "soft diffused light"
- Use --style raw when you want more control and less Midjourney interpretation
- Use --stylize 750+ for maximum artistic quality
- Use --no to exclude unwanted elements: "--no text --no watermark"

### Example Prompts

**Photorealistic portrait:**
```
Professional headshot of a tech executive, dramatic side lighting, dark moody background, shot on Canon EOS R5 85mm f/1.4, shallow depth of field --ar 1:1 --v 6.1 --stylize 500
```

**Futuristic scene:**
```
Cyberpunk cityscape at night, neon signs reflected in rain-slicked streets, volumetric fog, cinematic composition, Blade Runner aesthetic --ar 16:9 --v 6.1 --stylize 750
```

**Abstract art:**
```
Abstract flowing liquid metal in electric blue and deep purple, dark void background, reflective surfaces, macro photography --ar 16:9 --v 6.1 --stylize 900 --chaos 30
```

---

## Workflow Steps (ALL MANDATORY)

### Step 1: Verify Discord Environment

```bash
source ~/.claude/.env

# Check both variables exist
if [ -z "$DISCORD_BOT_TOKEN" ] || [ -z "$MIDJOURNEY_CHANNEL_ID" ]; then
  echo "ERROR: Missing Discord env vars in ~/.claude/.env"
  echo "Required: DISCORD_BOT_TOKEN, MIDJOURNEY_CHANNEL_ID"
  exit 1
fi
echo "Discord environment ready"
```

If variables are missing, STOP and ask the user to configure them.

### Step 2: Craft the Prompt

Build the Midjourney prompt with:
1. Detailed scene description
2. Style/mood/lighting keywords
3. Camera/lens references (if photorealistic)
4. Aspect ratio flag (--ar)
5. Model version (--v 6.1)
6. Style/stylize flags as needed
7. Negative prompts (--no) for unwanted elements

### Step 3: Generate Image

```bash
bun run ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art/tools/GenerateMidjourneyImage.ts \
  --prompt "[FULL MIDJOURNEY PROMPT INCLUDING --ar AND --v FLAGS]" \
  --output ~/Downloads/midjourney-[descriptive-name].png
```

NOTE: Generation may take 1-3 minutes. The tool sends the prompt to Discord, waits for Midjourney to process it, and downloads the result.

### Step 4: Wait for Completion

Midjourney generation is not instant. The tool handles the waiting, but expect:
- Fast: 30-60 seconds (simple prompts, lower quality)
- Standard: 1-2 minutes (normal prompts)
- Slow: 2-3 minutes (complex prompts, --q 2, high detail)

### Step 5: Validate Output

```bash
# Verify file was created
ls -lh ~/Downloads/midjourney-[descriptive-name].png

# Check dimensions
magick identify -format "%wx%h" ~/Downloads/midjourney-[descriptive-name].png

# Open for visual inspection
open ~/Downloads/midjourney-[descriptive-name].png
```

### Step 6: Iterate if Needed

If the result is not satisfactory:
- Adjust the prompt for more specificity
- Try different --stylize values
- Add --style raw for more literal interpretation
- Add --no flags to exclude unwanted elements
- Try different --chaos values for variety
- Regenerate with the refined prompt

---

## Tool Invocation

```bash
bun run ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art/tools/GenerateMidjourneyImage.ts \
  --prompt "[PROMPT] --ar 16:9 --v 6.1" \
  --output ~/Downloads/midjourney-[name].png
```

NOTE: This uses GenerateMidjourneyImage.ts (NOT Generate.ts). The Midjourney tool handles Discord integration, waiting, and downloading internally.

---

## Validation Checklist

- [ ] Discord env vars are set (DISCORD_BOT_TOKEN, MIDJOURNEY_CHANNEL_ID)
- [ ] Output file created in ~/Downloads/
- [ ] Image matches the described prompt intent
- [ ] Aspect ratio matches the --ar flag used
- [ ] No unwanted artifacts, text, or watermarks
- [ ] Quality level is satisfactory
- [ ] Image opened and visually inspected

---

## Comparison: Midjourney vs nano-banana-pro

| Use Case | Recommended Tool |
|----------|-----------------|
| YouTube thumbnails | nano-banana-pro (via /art:thumbnail) |
| Pack icons | nano-banana-pro (via /art:pack-icon) |
| Branded wallpapers | nano-banana-pro (via /art:wallpaper) |
| Photorealistic portraits | Midjourney |
| Maximum artistic stylization | Midjourney |
| Images needing --reference-image | nano-banana-pro (Midjourney has no reference flag) |
| Images needing --remove-bg | nano-banana-pro (Midjourney has no bg removal) |
| Speed-critical generation | nano-banana-pro (faster) |
| Highest possible visual quality | Midjourney |

---

## Outputs

| File | Description |
|------|-------------|
| ~/Downloads/midjourney-[name].png | Midjourney-generated image |
