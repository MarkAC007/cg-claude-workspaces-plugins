# /art:pack-icon -- PAI Pack Icon Generation

## Purpose

Generate 256x256 transparent PNG icons for PAI packs. Icons use electric blue (#4a90d9) as the dominant color with minimal purple accent, simple flat geometry readable at 64x64 pixels, and NO text.

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running the Pack Icon workflow", "voice_id": "25"}' \
  > /dev/null 2>&1 &
```

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Create an icon for this pack"
- "Generate a pack icon"
- "I need an icon for [pack-name]"
- New pack creation requiring an icon
- Icon refresh or regeneration

---

## Visual Specifications

| Spec | Value |
|------|-------|
| Dimensions | 256x256 pixels EXACTLY |
| Format | PNG with actual transparency (NOT checkerboard background) |
| Primary Color | Electric Blue #4a90d9 (dominant, 85-90%) |
| Accent Color | Purple #8b5cf6 (10-15% max) |
| Optional Dark | #0a0a0f (contrast elements if needed) |
| Style | Simple, flat, modern |
| Readability | Must be clear at 64x64 pixels |
| Text | NONE -- icons must work without labels |
| Centering | Icon centered in 256x256 canvas |

---

## Workflow Steps (ALL MANDATORY)

### Step 1: Understand Pack Purpose

Before generating, determine:
- What does this pack do?
- What visual metaphor represents its core function?
- How should it relate to other pack icons?

**Good icon concepts (examples):**
- Hook system -> Hook shape, event trigger
- Core install -> Download/install arrow
- Skill system -> Brain, routing, capability
- Agent system -> Robot/assistant figure
- Voice system -> Sound wave, speaker
- Memory system -> Brain with data flow
- Art system -> Paintbrush, palette, canvas

### Step 2: Construct Prompt

Build a prompt specifying the visual concept, style, colors, and constraints.

**Prompt template:**
```
[VISUAL CONCEPT representing PACK_FUNCTION]. Minimalist icon design.
Electric blue #4a90d9 as dominant color, tiny purple #8b5cf6 accent (10-15% max).
Simple flat geometry, modern icon style, readable at 64x64 pixels.
NO TEXT in the icon. Centered composition. Transparent background.
```

### Step 3: Generate at 1K with Background Removal

Generate at 1K resolution (produces ~2048px) with transparent background, then resize to 256x256.

```bash
bun run ~/dev/cg-claude-workspaces-plugins/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "Minimalist icon for [PACK_CONCEPT]. Electric blue #4a90d9 dominant, tiny purple #8b5cf6 accent. Simple flat geometry, readable at 64x64px. Transparent background. NO TEXT." \
  --size 1K \
  --aspect-ratio 1:1 \
  --remove-bg \
  --output ~/Downloads/[pack-name]-icon-2048.png
```

### Step 4: Resize to 256x256

Use ImageMagick to resize from the high-resolution source to the target dimensions.

```bash
magick ~/Downloads/[pack-name]-icon-2048.png \
  -resize 256x256 \
  ~/Downloads/[pack-name]-icon.png
```

### Step 5: Verify Output

```bash
# Check dimensions (must be 256x256)
magick identify -format "%wx%h" ~/Downloads/[pack-name]-icon.png

# Verify transparency
magick identify -verbose ~/Downloads/[pack-name]-icon.png | grep -A 5 "Alpha"

# Open for visual inspection
open ~/Downloads/[pack-name]-icon.png
```

### Step 6: Test at 64x64

The icon MUST be readable at 64x64 pixels (the size it appears in file explorers and small UIs).

```bash
magick ~/Downloads/[pack-name]-icon.png -resize 64x64 /tmp/icon-preview-64.png
open /tmp/icon-preview-64.png
```

If the icon is not clearly recognizable at 64x64, the design is too complex. Simplify and regenerate.

---

## Tool Invocation

```bash
# Step 1: Generate at high resolution with transparency
bun run ~/dev/cg-claude-workspaces-plugins/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[ICON PROMPT]" \
  --size 1K \
  --aspect-ratio 1:1 \
  --remove-bg \
  --output ~/Downloads/[pack-name]-icon-2048.png

# Step 2: Resize to target dimensions
magick ~/Downloads/[pack-name]-icon-2048.png \
  -resize 256x256 \
  ~/Downloads/[pack-name]-icon.png
```

---

## Validation Checklist

- [ ] File exists at ~/Downloads/[pack-name]-icon.png
- [ ] Format is PNG with actual transparency (alpha channel present)
- [ ] Dimensions are exactly 256x256 pixels
- [ ] Electric blue (#4a90d9) is the dominant color
- [ ] Purple accent (#8b5cf6) is 10-15% max (not competing with blue)
- [ ] NO text appears in the icon
- [ ] Icon is centered in the canvas
- [ ] Icon is clearly recognizable at 64x64 pixels
- [ ] Design represents the pack's core function
- [ ] Style is consistent with other PAI pack icons (simple, flat, modern)
- [ ] No background artifacts (clean transparency)

---

## Examples

### Hook System Pack
```bash
bun run ~/dev/cg-claude-workspaces-plugins/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "Stylized hook shape representing event hooks in software. Electric blue #4a90d9 dominant, tiny purple #8b5cf6 accent. Simple flat geometry, readable at 64x64px. Transparent background. NO TEXT." \
  --size 1K \
  --aspect-ratio 1:1 \
  --remove-bg \
  --output ~/Downloads/pai-hook-system-icon-2048.png

magick ~/Downloads/pai-hook-system-icon-2048.png -resize 256x256 ~/Downloads/pai-hook-system-icon.png
```

### Memory System Pack
```bash
bun run ~/dev/cg-claude-workspaces-plugins/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "Brain with data flowing in and out representing an AI memory system. Electric blue #4a90d9 dominant, tiny purple #8b5cf6 accent. Simple flat geometry, readable at 64x64px. Transparent background. NO TEXT." \
  --size 1K \
  --aspect-ratio 1:1 \
  --remove-bg \
  --output ~/Downloads/pai-memory-system-icon-2048.png

magick ~/Downloads/pai-memory-system-icon-2048.png -resize 256x256 ~/Downloads/pai-memory-system-icon.png
```

---

## Outputs

| File | Description |
|------|-------------|
| ~/Downloads/[pack-name]-icon-2048.png | High-resolution source (transparent) |
| ~/Downloads/[pack-name]-icon.png | Final 256x256 icon (transparent PNG) |
| /tmp/icon-preview-64.png | 64x64 readability test preview |
