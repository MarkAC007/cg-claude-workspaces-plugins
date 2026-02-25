# /art:comic -- Editorial Comic Strips

## Purpose

Creates editorial comic strips -- 3-4 panel sequential storytelling with a sophisticated New Yorker-style aesthetic. Black linework, flat colors, hand-drawn imperfection. These are NOT cartoonish or cutesy. They are thoughtful illustrated narratives with editorial intelligence.

Use this for explaining complex concepts through narrative, before/during/after sequences, illustrated thought experiments, multi-step processes shown visually, or any scenario that benefits from sequential panels.

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running the Comic workflow", "voice_id": "25"}' \
  > /dev/null 2>&1 &
```

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Make a comic about..."
- "Create a comic strip showing..."
- "Illustrate this scenario as panels"
- "Draw a 3-panel comic for..."
- Explaining concepts through sequential narrative
- Before/during/after sequences
- Illustrated thought experiments

## Workflow Steps (ALL MANDATORY)

### Step 1: Define Comic Narrative

Plan the story before generating anything.

1. **Identify the concept or scenario** -- what are you explaining or illustrating?
2. **Decide panel count** -- 3 panels (setup, action, result) or 4 panels (setup, complication, action, result).
3. **Map each panel** -- what happens in each panel? What is the scene, action, and dialogue?
4. **Identify the punchline or insight** -- the final panel must deliver the point. What makes this memorable?
5. **Define characters** -- main character gets purple (#4A148C) accent, secondary gets teal (#00796B).

Output a narrative plan:
```
COMIC CONCEPT: [What you are illustrating]
PANELS: [3 or 4]

NARRATIVE ARC:
Panel 1: [Setup - initial state]
Panel 2: [Action/Complication - what changes]
Panel 3: [Escalation or Result]
Panel 4: [Punchline/Insight] (if 4 panels)

DIALOGUE (Minimal):
Panel 1: "[Brief text or none]"
Panel 2: "[Brief text or none]"
Panel 3: "[Brief text or none]"
Panel 4: "[Punchline or insight]"

KEY CHARACTERS:
- [Character 1]: [Description, purple accent]
- [Character 2]: [Description, teal accent if needed]
```

### Step 2: Design Panel Layout

Choose the panel arrangement and structure.

- **Horizontal strip** (3-4 panels left to right) -- most common, classic comic strip
- **Vertical strip** (3-4 panels top to bottom)
- **Grid** (2x2 for 4 panels)

Panel sizes can be equal (classic) or varied (final panel larger for punchline emphasis). Keep backgrounds minimal and simple. Characters should be consistent across all panels -- same angular vocabulary, same color accents.

### Step 3: Construct Prompt

Build a detailed prompt using this structure:

```
Hand-drawn editorial comic strip in New Yorker style.

STYLE: New Yorker cartoon, editorial illustration, sophisticated sequential art. Hand-drawn editorial style (NOT cartoonish or cute). Flat color, black linework. Simplified but sophisticated character design. Variable stroke weight. Gestural imperfect linework. Minimal backgrounds. Smart humor or insight, not silly.

COMIC STRUCTURE: [3-panel / 4-panel] [horizontal strip / vertical / grid]

PANEL LAYOUT: [Number] panels arranged [direction]. Each panel has hand-drawn black border (slightly wobbly). Panel sizes: [Equal / Varied].

PANEL 1 - [SETUP]: Scene: [description]. Characters: [positions and actions]. Main character with Purple (#4A148C) accent on [element]. Background: Light cream (#F5E6D3), minimal. Dialogue: "[text]" or no text.

PANEL 2 - [ACTION]: Scene: [what changes]. Characters: [actions]. Optional secondary character with Teal (#00796B) accent. Background: [minimal elements]. Dialogue: "[text]" or no text.

PANEL 3 - [RESULT]: Scene: [situation develops]. Characters: [new states]. Background: [minimal]. Dialogue: "[text]" or no text.

PANEL 4 - [PUNCHLINE]: (if 4 panels) Scene: [final state]. Often larger panel. Background: simple for focus. Dialogue: "[punchline text]".

CHARACTER DESIGN - PLANEFORM AESTHETIC:
- All figures from ANGULAR PLANES (architectural paper models)
- NO round forms, NO smooth curves, NO circles on bodies
- Adult proportions (1:7 head-to-body), elongated and dignified
- NO cute proportions (big heads, stubby limbs)
- Faces are MINIMAL geometric blocks, NOT detailed, NOT cute
- Emotion through GESTURE and SILHOUETTE only
- Constructivist influence: El Lissitzky, Oskar Schlemmer, Saul Bass

COLOR: Black (#000000) for all linework. Purple (#4A148C) on main character. Teal (#00796B) on secondary. Charcoal (#2D2D2D) for dialogue. Light cream (#F5E6D3) or white backgrounds. Minimal flat color fills.
```

### Step 4: Determine Aspect Ratio

| Layout | Aspect Ratio | Notes |
|--------|-------------|-------|
| 3-panel horizontal | 16:9 or 21:9 | Wide strip format |
| 4-panel horizontal | 21:9 | Extra wide for 4 panels |
| 3-panel vertical | 9:16 | Tall strip |
| 4-panel grid (2x2) | 1:1 | Square balanced |
| Flexible | 4:3 | Default safe choice |

**Default: 16:9** -- classic comic strip format.

### Step 5: Generate

```bash
bun run ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[YOUR CONSTRUCTED PROMPT]" \
  --size 2K \
  --aspect-ratio 16:9 \
  --output ~/Downloads/comic.png
```

Immediately open for review:
```bash
open ~/Downloads/comic.png
```

### Step 6: Validate

**Must Have:**
- [ ] Clear panel structure -- panels obviously sequential
- [ ] Editorial aesthetic -- sophisticated, not cartoonish
- [ ] Narrative flow -- story/concept clear across panels
- [ ] Character consistency -- same character recognizable in all panels
- [ ] Hand-drawn quality -- imperfect linework, gestural
- [ ] Angular planeform figures -- NOT round, NOT cute
- [ ] Adult proportions (1:7) -- NOT stubby/big-headed
- [ ] Minimal faces -- geometric blocks, emotion through gesture
- [ ] Smart insight -- punchline or point lands

**Must NOT Have:**
- [ ] Cartoonish or cutesy style
- [ ] Round forms or smooth curves on figures
- [ ] Big heads, stubby proportions, big eyes
- [ ] Busy complex backgrounds
- [ ] Too much dialogue
- [ ] Gradients or shadows
- [ ] Generic AI illustration style

**Fix Table:**

| Problem | Fix |
|---------|-----|
| Too cartoonish | Add "sophisticated editorial, New Yorker aesthetic, NOT cartoonish" |
| Characters too round/cute | Add "ANGULAR PLANES ONLY. Constructivist. El Lissitzky, Schlemmer." |
| Cartoon proportions | Add "Adult 1:7 head-to-body. Elongated dignified figures." |
| Can't follow story | Clarify "Panel 1 setup, Panel 2 complication, Panel 3 result" |
| Too complex | Add "Minimal backgrounds, simple scenes, focus on key action" |

## Outputs

- `~/Downloads/comic.png` -- the generated comic strip image
- Move to project directory only after validation passes
