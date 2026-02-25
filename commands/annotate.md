# /art:annotate -- Annotated Screenshots

## Purpose

Creates annotated screenshots -- real UI or code screenshots with hand-drawn purple/teal commentary overlays. Arrows, circles, callouts, and editorial voice annotations layered on top of an actual screenshot. The screenshot is the foundation; the annotations add insight. Purple (#4A148C) for critical callouts, teal (#00796B) for helpful context.

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running the Annotate workflow", "voice_id": "25"}' \
  > /dev/null 2>&1 &
```

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Annotate this screenshot..."
- "Add callouts to this image..."
- "Mark up this UI with notes"
- "Create an annotated version of..."
- Product reviews with annotated screenshots
- Technical tutorials pointing out UI elements
- UX critiques with visual commentary
- Code reviews with illustrated notes
- "THIS IS THE PROBLEM" arrows and callouts

## Workflow Steps (ALL MANDATORY)

### Step 1: Prepare the Screenshot

1. **Get the base image** -- capture an actual screenshot of UI, code, website, or any visual artifact.
2. **Crop to relevant area** -- ensure the key content is visible and text is readable.
3. **Note the file path** -- you will pass this as `--reference-image`.

Output:
```
SCREENSHOT SOURCE: [Path to screenshot file]
SUBJECT: [What the screenshot shows]
ASPECT RATIO: [What ratio the screenshot is, e.g., 16:9, 4:3]
```

### Step 2: Plan Annotations

Identify what to mark and what commentary to add.

1. **What are you calling attention to?** Problem areas, good examples, workflow steps, hidden features.
2. **What type of annotation for each?**
   - Arrow pointing to element
   - Circle/box highlighting region
   - Underline or bracket
   - Callout box with note
3. **What is the commentary?** Write in editorial voice -- casual, direct, insightful. Use phrases like: "*this is the problem*", "*should be here instead*", "*genius design*", "*notice this pattern*", "*where users drop off*".
4. **Assign colors:**
   - Purple (#4A148C) -- critical annotations ("this is wrong", "key insight")
   - Teal (#00796B) -- helpful context ("here is why", "notice this")
   - Black (#000000) -- structural marks (arrows, circles, underlines)

Output:
```
ANNOTATIONS:

1. [Area/Element]:
   - Type: [Arrow / Circle / Box / Underline]
   - Color: [Purple / Teal / Black]
   - Text: "[Editorial commentary]"
   - Position: [Where on screenshot]

2. [Area/Element]:
   - Type: [Annotation type]
   - Color: [Color choice]
   - Text: "[Commentary]"
   - Position: [Location]

EMPHASIS:
- Purple (critical): [Which annotations]
- Teal (helpful): [Which annotations]
```

Limit to 3-5 key annotations. More than that becomes cluttered.

### Step 3: Construct Prompt

Build the annotation overlay prompt. This workflow uses `--reference-image` to pass the screenshot as the base.

```
Real UI screenshot with hand-drawn editorial annotations overlay.

STYLE: Actual screenshot with imperfect hand-drawn arrows, circles, and notes on top. Variable stroke weight, wobbly imperfect lines. Gestural quality (not polished vectors). Hand-lettered annotation text.

SCREENSHOT BASE: Slightly desaturated (80% opacity) to let annotations stand out. All original text and UI elements clearly visible.

ANNOTATIONS:

1. PURPLE ARROW pointing to [UI element]:
   - Hand-drawn wobbly arrow in Purple (#4A148C)
   - Text: "*[EDITORIAL COMMENTARY]*"
   - Thick stroke, clear pointing direction
   - Position: [Location]

2. TEAL CIRCLE around [UI area]:
   - Hand-drawn imperfect circle in Teal (#00796B)
   - Text: "*[helpful context]*"
   - Slightly wobbly outline
   - Position: [Area to highlight]

3. BLACK UNDERLINE beneath [text]:
   - Hand-drawn wavy underline in Black (#000000)
   - Emphasizes existing screenshot text

4. PURPLE CALLOUT box near [element]:
   - Hand-drawn box with arrow
   - Text: "*[critical insight]*"
   - Purple outline and text

COLOR: Screenshot original colors (slightly faded). Purple for critical callouts. Teal for helpful context. Black for structural marks. Charcoal (#2D2D2D) for general text.

CRITICAL: Screenshot remains readable. Annotations clearly overlay (not integrated into UI). Hand-drawn quality (wobbly, imperfect). Editorial voice. Strategic color (not every annotation colored). No gradients on annotations.
```

### Step 4: Determine Aspect Ratio

**Match the screenshot aspect ratio.** Do not change proportions.

- Screenshot is 16:9 -- use 16:9
- Screenshot is vertical phone -- use 9:16
- Screenshot is square -- use 1:1
- Screenshot is wide desktop -- use 21:9

### Step 5: Generate

```bash
bun run ~/dev/cg-claude-workspaces-plugins/tools/Generate.ts \
  --model nano-banana-pro \
  --reference-image [SCREENSHOT_PATH] \
  --prompt "[YOUR ANNOTATION PROMPT]" \
  --size 2K \
  --output ~/Downloads/annotated.png
```

Immediately open for review:
```bash
open ~/Downloads/annotated.png
```

**Alternative composite approach:** If generating combined image is difficult, generate the annotation layer separately (transparent background, only arrows/circles/text) and composite manually on top of the screenshot.

### Step 6: Validate

**Must Have:**
- [ ] Screenshot readable -- original content clearly visible
- [ ] Annotations clear -- arrows/circles/text obviously hand-drawn overlays
- [ ] Editorial voice -- annotations sound like smart commentary
- [ ] Strategic pointing -- annotations highlight key insights, not decoration
- [ ] Color emphasis -- purple on critical, teal on helpful
- [ ] Hand-drawn quality -- wobbly arrows, imperfect circles
- [ ] Functional value -- annotations enhance understanding

**Must NOT Have:**
- [ ] Unreadable screenshot
- [ ] Polished digital annotation look
- [ ] Generic corporate callouts
- [ ] Too many annotations (cluttered)
- [ ] Formal voice
- [ ] Perfect straight arrows or circles

**Fix Table:**

| Problem | Fix |
|---------|-----|
| Screenshot too dark | Lighten/desaturate screenshot, increase annotation contrast |
| Annotations too polished | "Hand-drawn wobbly arrows, imperfect circles, gestural sketch" |
| Voice too formal | Rewrite in casual voice: "*this right here*", "*the real issue*" |
| Can't tell what is pointed out | Larger/bolder arrows, clearer pointing direction |
| Too cluttered | Reduce to 3-5 key insights only |
| Looks corporate | "Editorial annotation style, smart person's markup, hand-drawn notes" |

## Outputs

- `~/Downloads/annotated.png` -- the annotated screenshot image
- Move to project directory only after validation passes
