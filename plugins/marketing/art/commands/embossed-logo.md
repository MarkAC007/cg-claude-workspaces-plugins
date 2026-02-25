# /art:embossed-logo -- Embossed Logo Wallpaper Generation

## Purpose

Generate sophisticated wallpapers where the logo is physically embossed as a texture within the visual content -- not overlaid, not floating in empty space. The logo appears as a subtle raised/pressed element integrated into the design, positioned small in the bottom left and surrounded by visual content.

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Create an embossed logo wallpaper"
- "Make a wallpaper with the logo built into the design"
- "I want a subtle logo wallpaper"
- "Generate a wallpaper with embossed branding"
- When the user wants a wallpaper where the logo feels manufactured into the surface

---

## Specifications

| Parameter | Value |
|-----------|-------|
| Resolution | 4K |
| Aspect Ratio | 16:9 |
| Model | nano-banana-pro |
| Logo Size | 3-5% of image width (SMALL) |
| Logo Position | Bottom left, WITHIN visual content |
| Logo Treatment | Embossed texture (raised/pressed), same color range as surroundings |

### Color Palette (STRICT)

**Allowed Colors:**

| Color | Bright | Muted |
|-------|--------|-------|
| Blue | #4a90d9 | #3a6a9a |
| Purple | #8b5cf6 | #6b4c96 |
| Cyan | #06b6d4 | #4a9a9a |
| Black base | #0a0a0f | -- |

**FORBIDDEN Colors:**
- Matrix green (#00ff41 or any green)
- Pink/magenta neon
- Bright saturated neons
- Any color outside the UL palette

---

## Common Failures to Avoid

| Failure | Correct Approach |
|---------|-----------------|
| Literal text "brand name" instead of logo shape | Use --reference-image with the logo file for shape guidance |
| Logo overlaid/floating instead of embossed | Specify "EMBOSSED INTO the surface" with "raised/pressed texture" |
| Logo in empty/blank area | Specify "WITHIN the visual content" and "NO empty corners" |
| Logo too large and prominent | Specify "3-5% of image width" and "SMALL" |
| Logo glowing differently from surroundings | Specify "same materials/colors as surroundings, slight luminosity difference only" |
| Wrong colors (green, pink, etc.) | List exact hex codes and explicitly say "NO GREEN, NO PINK" |
| Simple/cartoony/flat vector style | Describe "sophisticated, photorealistic or stylized with depth, dense detail" |
| Visual content only in center | Specify "visual content fills ENTIRE canvas, NO empty corners or blank areas" |

---

## Workflow Steps (ALL MANDATORY)

### Step 1: Gather Requirements

Ask about:
1. **Style direction** -- Photorealistic circuit, cyberpunk/hacker, abstract, neural network, etc.
2. **Tone** -- Bright and energetic OR muted and subdued (muted is usually better)
3. **Logo path** -- Path to the logo file (PNG)
4. **Output name** -- Filename in kebab-case

### Step 2: Load References

```bash
# Verify logo exists
ls [LOGO_PATH]

# Open logo to study shape
open [LOGO_PATH]
```

Study the logo for:
- Primary shapes and connected elements
- Key geometric features
- How it could be embossed as texture

### Step 3: Construct Prompt

Build the prompt with ALL required sections. This is the most critical step.

```
[STYLE] wallpaper, 16:9 4K resolution. [TONE MODIFIER].

AESTHETIC:
- [Describe visual style: cyberpunk, circuit, neural, abstract, etc.]
- Sophisticated, dense detail, photorealistic depth

VISUAL COMPLEXITY:
- Dense layers of [relevant visual elements]
- Overlapping translucent layers
- Visual content fills THE ENTIRE IMAGE including all corners
- NO empty or blank areas anywhere

TONE:
- [MUTED: desaturated, dark dominant, subtle glows, quiet sophistication]
- [OR BRIGHT: vibrant accents on dark base, electric highlights]

COLOR PALETTE (STRICT UL BRAND):
- Deep black void dominates (#0a0a0f)
- Blue (#4a90d9 or muted #3a6a9a)
- Purple (#8b5cf6 or muted #6b4c96)
- Cyan (#06b6d4 or muted #4a9a9a)
- NO GREEN, NO PINK, NO MAGENTA, NO OTHER COLORS

LOGO INTEGRATION (CRITICAL):
- Logo shape (from reference) EMBOSSED INTO the visual content
- Position: bottom left, WITHIN the design, not in empty space
- Logo is part of the visual architecture -- traces/elements flow through it
- SMALL: 3-5% of image width
- Same visual treatment as surrounding elements
- Embossed texture: slight depth/luminosity difference ONLY
- Should look manufactured into the surface
- NOT floating, NOT overlaid, NOT glowing differently

COMPOSITION:
- Visual content fills ENTIRE canvas
- Bottom left corner has visual detail WITH logo embossed into it
- No blank corners or empty zones
- Uniform density of visual interest

CRITICAL:
- Logo MUST be integrated INTO the design
- Logo MUST be SMALL and SUBTLE
- Entire image has visual content -- no blank areas
- ONLY blue/purple/cyan colors -- nothing else
```

### Step 4: Generate

```bash
bun run ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[CONSTRUCTED_PROMPT]" \
  --reference-image [LOGO_PATH] \
  --size 4K \
  --aspect-ratio 16:9 \
  --output ~/Downloads/embossed-[output-name].png
```

### Step 5: Validate (CRITICAL)

Open the generated image and check EVERY item in the validation checklist.

```bash
open ~/Downloads/embossed-[output-name].png
```

If ANY check fails, adjust the prompt and regenerate. Common prompt adjustments:
- Logo in wrong place: Emphasize "WITHIN the visual content" and "NO empty corners"
- Logo too big: Specify "3-5% of image width" more forcefully
- Wrong colors: Repeat exact hex codes and add "NO GREEN, NO PINK, NO [wrong color]"
- Too bright: Add "MUTED, SUBDUED, desaturated" throughout prompt
- Too simple: Add more complexity keywords and reference sophisticated style

### Step 6: Iterate Until All Checks Pass

Do NOT present the wallpaper until every validation item passes. Regenerate as many times as needed.

---

## Tool Invocation

```bash
bun run ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[SOPHISTICATED DARK TECH WALLPAPER WITH EMBOSSED LOGO IN BOTTOM LEFT]" \
  --reference-image [LOGO_PATH] \
  --size 4K \
  --aspect-ratio 16:9 \
  --output ~/Downloads/embossed-[name].png
```

---

## Validation Checklist

- [ ] Logo is the correct shape (from reference), NOT text
- [ ] Logo is EMBOSSED (texture/raised), NOT overlaid or floating
- [ ] Logo is in the bottom left corner
- [ ] Logo is SMALL (3-5% of image width)
- [ ] Logo is WITHIN visual content, NOT in empty space
- [ ] Logo uses same color palette as surroundings (not glowing differently)
- [ ] Colors are ONLY blue/purple/cyan (NO green, NO pink, NO other colors)
- [ ] Style is sophisticated, NOT cartoony or flat vector
- [ ] Tone matches request (muted if requested)
- [ ] Visual content fills entire canvas (NO blank areas, NO empty corners)
- [ ] Quality matches professional wallpaper standards
- [ ] Image dimensions are 4K+ (5504x3072 or similar)

---

## Example Prompt (Muted Cyberpunk)

```
Cyberpunk hacker wallpaper, 16:9 4K resolution. SUBDUED AND MUTED.

AESTHETIC:
- Dense layers of data streams and neural network architecture
- Sophisticated cyberpunk atmosphere - Ghost in the Shell aesthetic
- Mature, serious, detailed

VISUAL COMPLEXITY:
- Thousands of tiny particles and data points
- Overlapping translucent layers of circuit geometry
- Dense but organized chaos throughout THE ENTIRE IMAGE
- Visual content extends to ALL edges including bottom left
- NO empty or blank areas anywhere

TONE (SUBDUED):
- MUTED colors - desaturated, not neon bright
- DARK overall - near-black dominates
- Subtle glows instead of bright neon
- Quiet sophistication, not loud

COLOR PALETTE (MUTED UL BRAND):
- Deep black void dominates (#0a0a0f)
- Desaturated blue (#3a6a9a)
- Muted purple (#6b4c96)
- Soft cyan (#4a9a9a)
- NO GREEN, NO PINK, NO OTHER COLORS

LOGO INTEGRATION (CRITICAL):
- Logo shape (from reference) EMBOSSED INTO the visual content
- Position: bottom left, WITHIN the circuit/data design
- Part of the circuit architecture - traces flow through it
- SMALL: 3-5% of image width
- Same visual treatment as surrounding elements
- Embossed texture - slight depth/luminosity difference only
- Manufactured into the circuit board surface
- NOT floating, NOT in empty space

COMPOSITION:
- Visual content fills ENTIRE canvas
- Bottom left has circuit detail WITH logo embossed into it
- No blank corners or empty zones

CRITICAL:
- Logo integrated INTO design, not placed in empty space
- Logo SMALL and SUBTLE
- Entire image has visual content
- Subdued, muted, sophisticated
```

---

## Outputs

| File | Description |
|------|-------------|
| ~/Downloads/embossed-[name].png | 4K 16:9 wallpaper with embossed logo |

User copies to wallpaper directory after approval.
