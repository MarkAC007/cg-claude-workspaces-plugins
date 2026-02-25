# /art:thumbnail -- YouTube Thumbnail Generation

## Purpose

Generate complete YouTube thumbnails (1280x720) with AI-generated face-only headshots, dramatic futuristic tech backgrounds, and billboard-style text. Each thumbnail is unique with varied headshot expressions, positions, and background styles.

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Make me a YouTube thumbnail"
- "Create a thumbnail for this video"
- "I need a thumbnail about [topic]"
- Any request involving YouTube thumbnail creation

---

## Output Specifications

| Element | Value |
|---------|-------|
| Canvas | 1280x720 px exactly |
| Border | 16px #bb9af7 (Tokyo Night purple) |
| Headshot | FACE ONLY (forehead to chin), transparent background |
| Title | 100pt Helvetica-Bold, 4px black stroke outline |
| Subtitle | 50pt Helvetica-Bold, 3px black stroke outline |
| Title color | CYAN (#7dcfff) by default -- NEVER plain white |
| Subtitle color | White (#FFFFFF) |
| Text position | FILLS safe zone opposite headshot (NEVER overlaps) |
| Background | Dramatic futuristic tech art |

### Text Color Presets (--title-color flag)

| Name | Hex | Use |
|------|-----|-----|
| cyan | #7dcfff | DEFAULT -- Tech, futuristic |
| white | #FFFFFF | High contrast |
| purple | #bb9af7 | Matches border |
| blue | #7aa2f7 | Professional |
| magenta | #ff007c | Bold, attention |
| yellow | #e0af68 | Warning, highlight |
| green | #9ece6a | Success, growth |
| orange | #ff9e64 | Energy, urgency |
| red | #f7768e | Alert, danger |

---

## Workflow Steps (ALL MANDATORY)

### Step 1: Content Analysis

Extract title and subtitle from user input (script, URL, topic, outline).

- TITLE: Max 6 words. Use power words: "SECRET", "HIDDEN", "REAL", "TRUTH", "WHY", "HOW"
- SUBTITLE: Max 12 words. The value promise or context.
- Create curiosity gaps. Be specific over generic. Make a bold claim or promise.

### Step 2: Generate Background

Dark futuristic tech background -- NO faces, NO text in the background.

```bash
TIMESTAMP=$(date +%Y%m%d-%H%M%S)

bun run ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art/tools/Generate.ts \
  --model nano-banana \
  --prompt "Dramatic futuristic technology background. Dark hexagonal circuit board pattern with glowing cyan/blue neon edge lighting. 3D depth perspective. Metallic dark grey hexagons with embedded circuit patterns. Glowing cyan (#7dcfff) and purple (#bb9af7) edge highlights. Deep shadows, high contrast. Sci-fi aesthetic like Blade Runner or Tron. Abstract technology, NO TEXT, NO PEOPLE. Dark moody atmosphere with electric blue glow accents. Topic context: [EXTRACTED_TOPIC]" \
  --size 16:9 \
  --output ~/Downloads/yt-bg-${TIMESTAMP}.png
```

### Step 3: Generate Headshot (FACE ONLY)

CRITICAL RULES:
- FACE ONLY: Forehead to chin, ear to ear
- NO shoulders, NO neck, NO body visible
- Face fills 95% of image area
- If shoulders/body visible, REGENERATE IMMEDIATELY
- Must use reference images for likeness
- Must use --remove-bg for transparency

For EACH thumbnail, randomly select one from each variation category:

**Angle:** Straight-on | Slight 3/4 turn (15 degrees right) | Head tilted slightly right
**Expression:** Confident/authoritative | Contemplative/thoughtful intensity | Focused/direct engagement
**Lighting:** Soft diffused key light | Dramatic side lighting with shadow | Rembrandt lighting pattern

Example prompts:

- Variation A: "Extreme close-up FACE ONLY. Forehead to chin, ear to ear. NO shoulders, NO neck, NO body. Confident, authoritative expression, NOT smiling. Looking directly at camera. Pure black background. Full beard along jawline, clean-shaven upper lip. Soft diffused key lighting. Ultra-tight crop on face only."
- Variation B: "Extreme close-up FACE ONLY. Forehead to chin, ear to ear. NO shoulders, NO neck, NO body. Contemplative, thoughtful expression. Face turned 15 degrees right, slight 3/4 angle. Pure black background. Full beard along jawline, clean-shaven upper lip. Dramatic side lighting. Ultra-tight crop on face only."
- Variation C: "Extreme close-up FACE ONLY. Forehead to chin, ear to ear. NO shoulders, NO neck, NO body. Focused, direct engagement expression. Head tilted slightly. Pure black background. Full beard along jawline, clean-shaven upper lip. Rembrandt lighting. Ultra-tight crop on face only."

```bash
bun run ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[FACE-ONLY HEADSHOT PROMPT]" \
  --reference-image [REFERENCE_IMAGE] \
  --size 2K \
  --aspect-ratio 1:1 \
  --remove-bg \
  --output ~/Downloads/yt-headshot-${TIMESTAMP}.png
```

### Step 4: Compose Thumbnail

Combine background, headshot, and text using ComposeThumbnail.

```bash
bun run ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art/tools/ComposeThumbnail.ts \
  --background ~/Downloads/yt-bg-${TIMESTAMP}.png \
  --headshot ~/Downloads/yt-headshot-${TIMESTAMP}.png \
  --title "[TITLE - MAX 6 WORDS]" \
  --subtitle "[SUBTITLE - MAX 12 WORDS]" \
  --headshot-position [left|center|right] \
  --title-color cyan \
  --output ~/Downloads/yt-thumbnail-${TIMESTAMP}.png
```

**ComposeThumbnail flags:**

| Flag | Description |
|------|-------------|
| --background | Background image path |
| --headshot | Transparent headshot PNG path |
| --title | Up to 6 words (will be CAPITALIZED) |
| --subtitle | Up to 12 words |
| --headshot-position | left, center, or right (default: left) |
| --title-color | white, cyan, purple, blue, magenta, yellow, green, orange, red, or #hex |
| --subtitle-color | Default white |
| --border-color | Default #bb9af7 (Tokyo Night purple) |
| --output | Output path (produces 1280x720) |

**Position logic:**
- left: Headshot on left, text centered on right half
- center: Headshot centered, title at top, subtitle at bottom
- right: Headshot on right, text centered on left half

### Step 5: Quality Validation

ALL checks must pass before presenting to user.

```bash
# Verify dimensions (must be 1280x720)
magick identify -format "%wx%h" ~/Downloads/yt-thumbnail-${TIMESTAMP}.png

# Open for visual inspection
open ~/Downloads/yt-thumbnail-${TIMESTAMP}.png

# MANDATORY: Test at YouTube thumbnail size (320x180)
magick ~/Downloads/yt-thumbnail-${TIMESTAMP}.png -resize 320x180 /tmp/yt-preview.png
open /tmp/yt-preview.png
```

---

## Validation Checklist

- [ ] Dimensions exactly 1280x720
- [ ] FACE-ONLY headshot (NO shoulders, NO neck, NO body)
- [ ] Face fills 90%+ of headshot area
- [ ] Text fills the text zone (large, bold, billboard-style)
- [ ] Title color is CYAN or vibrant (NOT plain white)
- [ ] Stroke visible (4px title / 3px subtitle)
- [ ] No overlap between text and headshot
- [ ] Visibly different from previous generation (varied expression, position, background)
- [ ] Text READABLE at 320x180 (YouTube grid size)
- [ ] Professional, billboard-quality appearance

**If ANY check fails:** Do NOT present to user. Fix the issue, recompose, revalidate.

---

## Outputs

| File | Description |
|------|-------------|
| ~/Downloads/yt-bg-{timestamp}.png | Generated background |
| ~/Downloads/yt-headshot-{timestamp}.png | Transparent face-only headshot |
| ~/Downloads/yt-thumbnail-{timestamp}.png | Final composed thumbnail (1280x720) |

---

## Quick Reference

```
Tokyo Night Colors:
  Purple (border):  #bb9af7
  Cyan (title):     #7dcfff
  Blue (accent):    #7aa2f7
  Dark base:        #1a1b26

Workflow Summary:
  1. ANALYZE content -> Extract TITLE + SUBTITLE
  2. GENERATE background -> Dramatic tech art (nano-banana, NO faces/text)
  3. GENERATE headshot -> FACE-ONLY (nano-banana-pro, 1:1, --remove-bg), WITH VARIATION
  4. COMPOSE -> ComposeThumbnail.ts (auto-crops, cyan text, 100pt title)
  5. VALIDATE -> ALL gates including 320x180 readability test

Philosophy: The thumbnail is a BILLBOARD, not a document.
  - FACE dominates one side
  - TEXT FILLS the other side
  - Must be readable at 320x180
  - Every generation is visibly different
```
