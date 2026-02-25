# /art:recipe -- Process Recipe Cards

## Purpose

Creates process recipe cards -- numbered steps with small illustrations for each action. Scannable format with 3-tier typography (title, steps, details). These are visual how-to guides that make complex processes memorable and easy to reference. Purple (#4A148C) for critical steps and outcomes. Professional deliverable quality.

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Make a recipe card for this process..."
- "Create a step-by-step visual for..."
- "Turn this workflow into a recipe card"
- "Illustrate these steps as a visual guide"
- Process documentation and methodology playbooks
- Consulting deliverable how-to guides
- Best practice checklists
- Strategic frameworks with steps
- "The 5-Step Analysis Recipe" style visuals

## Workflow Steps (ALL MANDATORY)

### Step 1: Define the Process

1. **Name the process** -- give it a recipe-style title (e.g., "The 5-Step TELOS Analysis Recipe").
2. **Define the outcome** -- what does completing this process achieve?
3. **List 3-7 steps** -- each step needs a name, action description, and icon metaphor. Too many steps means break into multiple recipes.
4. **Mark critical steps** -- which step(s) are most important? These get purple emphasis.

Output:
```
PROCESS NAME: [The X Recipe / X-Step Y Method]
OUTCOME: [What this process achieves]

STEPS:
1. [Step name] -- [Action description] -- [Icon metaphor]
2. [Step name] -- [Action description] -- [Icon metaphor]
3. [Step name] -- [Action description] -- [Icon metaphor]
4. [Step name] -- [Action description] -- [Icon metaphor]
5. [Step name] -- [Action description] -- [Icon metaphor]

CRITICAL STEPS (Purple): [Which step numbers are most important]
OUTCOME STEP (Purple): [Final step gets purple emphasis]
```

### Step 2: Design Recipe Card Layout

Plan the visual structure:

1. **Layout style:**
   - Vertical list (top to bottom) -- most common, classic recipe card
   - Grid (2x3 for 6 steps)
   - Horizontal flow (left to right)
   - Circular flow (process loops)

2. **Each step contains:**
   - Numbered badge (circled number, e.g., "1" in circle)
   - Small hand-drawn icon/illustration for the action
   - Step name (Tier 2 typography)
   - Brief description (Tier 3 typography)
   - Arrow connecting to next step

3. **Color coding:**
   - Most steps: Black badges and icon outlines
   - Critical step(s): Purple (#4A148C) badge and icon accents
   - Final outcome: Purple emphasis
   - Text: Charcoal (#2D2D2D)

### Step 3: Construct Prompt

Build the generation prompt:

```
Hand-drawn process recipe card in editorial style.

STYLE: Recipe card, visual playbook, illustrated step-by-step guide. Hand-drawn step icons (simple, imperfect, editorial). Numbered steps with clear progression. Variable stroke weight. Professional but human quality.

BACKGROUND: Light Cream #F5E6D3 -- clean, card-like.

LAYOUT: [Vertical list / Grid / Horizontal flow]

TYPOGRAPHY (3-TIER):
TIER 1 - TITLE (Advocate Block Display): "[PROCESS NAME]" -- large at top, extra bold, hand-lettered, all-caps. Black #000000.
TIER 2 - STEP NAMES (Concourse Sans): "Step 1: [Name]" -- medium readable. Charcoal #2D2D2D.
TIER 3 - DESCRIPTIONS (Advocate Condensed): Brief action text -- 60% of Tier 2. Charcoal #2D2D2D.

STEPS:
STEP 1: [Name]
- Number badge: "1" in black circle
- Icon: [Simple hand-drawn icon, e.g., "magnifying glass"]
- Description: "[Brief action]"
- Arrow: Black arrow to Step 2

STEP 2: [Name]
- Number badge: "2" in black circle
- Icon: [Simple hand-drawn icon]
- Description: "[Brief action]"
- Arrow: Black arrow to Step 3

STEP 3: [Critical Step Name]
- Number badge: "3" in Purple (#4A148C) circle -- CRITICAL STEP
- Icon: [Hand-drawn icon with purple accents]
- Description: "[Brief action]"
- Arrow: Purple arrow to Step 4

[Continue for all steps...]

FINAL STEP [X]: [Outcome]
- Number badge: "[X]" in Purple (#4A148C) circle -- OUTCOME
- Icon: [Success icon, e.g., "checkmark", "trophy"]
- Description: "[Outcome achieved]"
- Purple emphasis

CONNECTING: Hand-drawn wobbly arrows between steps. Black for normal, purple for critical path.

CRITICAL: Hand-drawn recipe card aesthetic. Simple scannable icons. Clear 1-2-3 progression. 3-tier typography. Purple on critical/outcome steps. No gradients. Professional deliverable quality.
```

### Step 4: Determine Aspect Ratio

| Layout | Aspect Ratio | Notes |
|--------|-------------|-------|
| Vertical list (3-7 steps) | 9:16 or 4:3 | Tall card format |
| Grid (6-9 steps) | 1:1 | Square balanced grid |
| Horizontal flow | 16:9 | Wide linear progression |
| Circular process | 1:1 | Square for symmetry |

**Default: 9:16 (portrait)** -- classic recipe card orientation. Use 4:3 if the vertical crop is too extreme.

### Step 5: Generate

```bash
bun run ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[YOUR CONSTRUCTED PROMPT]" \
  --size 2K \
  --aspect-ratio 9:16 \
  --output ~/Downloads/recipe-card.png
```

Immediately open for review:
```bash
open ~/Downloads/recipe-card.png
```

### Step 6: Validate

**Must Have:**
- [ ] Clear progression -- steps obviously flow 1, 2, 3
- [ ] Scannable layout -- easy to reference quickly
- [ ] Simple icons -- each step has recognizable illustration
- [ ] Readable text -- all step names and descriptions legible
- [ ] Strategic color -- purple on critical/outcome steps
- [ ] Hand-drawn quality -- recipe card has editorial aesthetic
- [ ] Professional deliverable -- client-ready quality

**Must NOT Have:**
- [ ] Complex detailed illustrations
- [ ] Cluttered layout
- [ ] Illegible small text
- [ ] Missing step numbers
- [ ] Unclear flow
- [ ] Corporate process diagram look

**Fix Table:**

| Problem | Fix |
|---------|-----|
| Icons too complex | "Simple hand-drawn icons, minimal detail, recognizable at glance" |
| Can't follow flow | "Clear numbered badges 1-2-3, black arrows connecting steps" |
| Too cluttered | Reduce description text, simplify layout |
| Looks corporate | "Recipe card aesthetic, hand-drawn playbook, editorial style" |
| Text unreadable | Increase Tier 2/3 text sizes, more spacing |
| Missing emphasis | "Purple (#4A148C) on Step [X] and final outcome step" |

## Outputs

- `~/Downloads/recipe-card.png` -- the generated recipe card image
- Move to project directory only after validation passes
