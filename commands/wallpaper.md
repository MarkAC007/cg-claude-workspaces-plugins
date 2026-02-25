# /art:wallpaper -- Branded 4K Wallpaper Generation

## Purpose

Generate branded 4K wallpapers (16:9) that integrate logos as organic design elements -- emblazoned, embossed, woven, or negative space. Designed for terminal backgrounds and macOS desktop with the UL blue/purple/teal color palette.

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running the Wallpaper workflow", "voice_id": "25"}' \
  > /dev/null 2>&1 &
```

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Create a wallpaper"
- "Generate a desktop background"
- "Make a terminal background with my logo"
- "I need a 4K wallpaper"
- Any request for branded wallpapers with logo integration

---

## Specifications

| Parameter | Value |
|-----------|-------|
| Resolution | 4K |
| Aspect Ratio | 16:9 |
| Model | nano-banana-pro |
| Background | Dark (#0a0a0f to #1a1a2e) |
| Primary Color | Electric Blue (#4a90d9) |
| Secondary Color | Deep Purple (#8b5cf6) |
| Tertiary Color | Cyan/Teal (#06b6d4) |
| Style | Dark tech (circuits, geometric, abstract, flowing) |

---

## Workflow Steps (ALL MANDATORY)

### Step 1: Gather Input

Collect from the user:

1. **Logo selection** -- Which logo file to embed (path to PNG/SVG)
2. **Style direction** -- One of:
   - **Circuit** -- Dense PCB traces, solder points, layer depth
   - **Geometric** -- Hexagonal grids, triangular tessellation, isometric depth
   - **Flowing** -- Organic curved lines, data streams, particle flows
   - **Abstract** -- Non-representational color fields, gradient washes, minimal
3. **Integration style** -- How the logo appears:
   - **Emblazoned** -- Logo as glowing focal point, patterns radiate outward
   - **Embossed** -- Logo as subtle raised/pressed texture, discoverable not obvious
   - **Woven** -- Logo dissolved into pattern, circuits flow through it
   - **Negative space** -- Logo revealed by absence of pattern
4. **Output name** -- Filename in kebab-case (no extension)

**Defaults if not specified:**
- Integration: woven (most subtle)
- Style: circuit (matches existing wallpapers)
- Use primary logo if available

### Step 2: Analyze Logo

Read the selected logo to understand its shapes, forms, and proportions.

```bash
ls [LOGO_PATH]
open [LOGO_PATH]
```

### Step 3: Construct Prompt

Build the generation prompt with all required sections:

```
Dark tech wallpaper for terminal/desktop, 16:9 4K resolution.

BACKGROUND: Deep dark blue-black gradient (#0a0a0f to #1a1a2e)

INTEGRATION: [LOGO_NAME] logo shape [INTEGRATION_STYLE]:
- [Describe how logo integrates with the pattern]
- Logo should feel organic to the design, not overlaid
- Shape emerges from or defines the pattern flow

PATTERN STYLE: [STYLE_DIRECTION]
- [Specific pattern elements matching style]
- [How pattern interacts with logo shape]

COLOR PALETTE:
- Primary: Electric blue (#4a90d9) -- main circuit lines/elements
- Secondary: Deep purple (#8b5cf6) -- accent glows, key nodes
- Tertiary: Cyan/teal (#06b6d4) -- highlights, energy points
- Background: Near-black with subtle blue undertone

EFFECTS:
- Subtle depth of field (sharper center, soft edges)
- Glow effects on key nodes and accent points
- Fine detail in circuit traces/patterns
- Atmospheric haze in corners

CRITICAL:
- Logo shape is INTEGRAL to design, not overlaid
- Must work as terminal background with 85% dark tint overlay
- No text, no watermarks
- High contrast details for visibility through tint
- Professional, sophisticated tech aesthetic
```

### Step 4: Generate Wallpaper

```bash
bun run ~/dev/cg-claude-workspaces-plugins/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[CONSTRUCTED_PROMPT]" \
  --reference-image [LOGO_PATH] \
  --size 4K \
  --aspect-ratio 16:9 \
  --output ~/Downloads/wallpaper-[output-name].png
```

### Step 5: Preview and Validate

```bash
open ~/Downloads/wallpaper-[output-name].png
```

Run through the validation checklist below. If any check fails, adjust the prompt and regenerate.

### Step 6: Iterate if Needed

Common fixes:
- Logo not integrated: Strengthen integration language in prompt
- Wrong colors: List exact hex codes, explicitly exclude unwanted colors
- Too bright: Add "MUTED, SUBDUED, desaturated"
- Too simple: Describe sophistication level, add complexity keywords
- Logo not visible: Try a different integration style

---

## Integration Styles Reference

### Emblazoned
Logo as the glowing focal point -- circuits/patterns radiate outward from it.
```
Logo shape as central glowing element, circuit traces emanating outward from its edges,
energy nodes at key logo vertices, pattern density increases near logo
```

### Embossed
Logo as subtle texture -- raised or pressed into the pattern layer.
```
Logo shape visible as subtle raised/depressed region in the pattern,
same color palette but slightly different luminosity, discoverable not obvious
```

### Woven
Logo shape defines pattern flow -- elements flow through/around it.
```
Circuit traces and geometric elements flow through and around logo shape,
logo boundary influences pattern direction, shape emerges from negative space
```

### Negative Space
Logo revealed by absence -- pattern stops at logo boundaries.
```
Dense pattern everywhere except logo shape, logo appears as void/window,
subtle glow at logo edges where pattern meets empty space
```

---

## Tool Invocation

```bash
bun run ~/dev/cg-claude-workspaces-plugins/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[4K WALLPAPER PROMPT WITH LOGO INTEGRATION]" \
  --reference-image [LOGO_PATH] \
  --size 4K \
  --aspect-ratio 16:9 \
  --output ~/Downloads/wallpaper-[name].png
```

---

## Validation Checklist

- [ ] Logo shape is recognizable but integrated (not pasted on)
- [ ] Color palette matches UL aesthetic (blue/purple/teal on dark)
- [ ] Pattern has enough contrast to show through terminal tint (85% dark)
- [ ] No artifacts, text, or watermarks
- [ ] Professional quality suitable for desktop/terminal
- [ ] Image dimensions are 4K+ (5504x3072 or similar)
- [ ] Dark background dominates (#0a0a0f to #1a1a2e range)
- [ ] No unwanted colors (no bright green, pink, orange, etc.)

---

## Outputs

| File | Description |
|------|-------------|
| ~/Downloads/wallpaper-[name].png | 4K 16:9 branded wallpaper |

User copies to wallpaper directory after approval.
