# /art:comparison -- X vs Y Split Compositions

## Purpose

Create hand-drawn side-by-side visual comparisons using editorial split-screen style. Shows two contrasting concepts, states, or approaches with illustrated metaphors that make differences immediately obvious. Purple for one side, teal for the other (or purple on the preferred side).

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running the Comparison workflow", "voice_id": "25"}' \
  > /dev/null 2>&1 &
```

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Compare X vs Y"
- "Before and after"
- "This vs That"
- "Junior vs Senior"
- "Old way vs New way"
- Any content showing two contrasting approaches, states, or concepts
- Visual dichotomies and illustrated contrasts

## Workflow Steps (ALL 6 MANDATORY)

### Step 1: Define the Comparison

Identify what you are contrasting:

1. **What are the two sides?**
   - Side A: [Concept / State / Approach]
   - Side B: [Concept / State / Approach]

2. **What is the key difference?** [What fundamentally distinguishes them]

3. **What visual metaphors show the contrast?**
   - Side A metaphor: [Physical object/scene]
   - Side B metaphor: [Contrasting object/scene]

4. **Is one side "better" or are they equal?**
   - Better: Highlight that side in purple
   - Equal: Purple left, teal right (balanced)

**Template:**
```
COMPARISON: [Side A] vs [Side B]
CORE CONTRAST: [What's fundamentally different]
VISUAL METAPHORS:
  Side A: [Metaphor]
  Side B: [Contrasting metaphor]
VALUE JUDGMENT: [Neutral] or [Side X is preferred]
COLOR STRATEGY: [Purple left / Teal right] or [Purple on preferred]
```

### Step 2: Design Split Layout

**Split orientation options:**
- Vertical split (left/right) -- Classic comparison (default)
- Horizontal split (top/bottom) -- Before/after flow
- Diagonal split -- More dynamic

**Mirror elements:** What visual elements repeat on both sides for parallel structure

**Dividing line:** Strong black line, soft visual separation, or no line (color creates division)

**Color System:**
- Left/Top Side: Purple #4A148C accents
- Right/Bottom Side: Teal #00796B accents
- OR: Purple on "preferred" side, black on alternative
- Dividing line: Black #000000
- All text: Charcoal #2D2D2D
- Background: White #FFFFFF or Light Cream #F5E6D3

**Character Requirements (if figures present):**
- Angular planes, NOT round forms
- Adult proportions (1:7), NOT cute/stubby
- Minimal geometric faces
- Emotion through gesture/silhouette
- Constructivist/Bauhaus influence, NOT cartoonish

### Step 3: Construct Prompt

```
Hand-drawn split composition comparing two contrasting concepts in editorial style.

STYLE: Magazine comparison spread, split-screen editorial illustration
BACKGROUND: [White #FFFFFF or Light Cream #F5E6D3]

AESTHETIC:
- Split composition with [vertical/horizontal] division
- Hand-drawn black linework on both sides (imperfect, gestural)
- Mirror structure showing parallel concepts with visual contrast
- Editorial flat color with strategic purple/teal differentiation
- Variable stroke weight, organic lines

SPLIT: [Vertical left-to-right / Horizontal top-to-bottom]

TYPOGRAPHY (3-TIER):
TIER 1 - TITLE: "[SIDE A] VS [SIDE B]"
  Advocate style, extra bold, hand-lettered, all-caps, 3x body, black, top center
TIER 2 - SIDE LABELS: "[Side A]" and "[Side B]"
  Concourse geometric sans, medium, charcoal, headers for each side
TIER 3 - ANNOTATIONS: "*overthinks*" vs "*simplifies*"
  Advocate condensed italic, 60% of Tier 2, matching side color

LEFT/TOP SIDE - [SIDE A]:
- Visual metaphor: [Description]
- Color: Purple (#4A148C) accents on [elements]
- Black primary linework

RIGHT/BOTTOM SIDE - [SIDE B]:
- Visual metaphor: [Contrasting description]
- Color: Teal (#00796B) accents on [elements]
- Black primary linework

DIVIDING LINE: [Strong black line / Visual separation]

COLOR USAGE:
- Black: All linework both sides + dividing line
- Purple: Left/preferred side accents
- Teal: Right/alternative side accents
- Charcoal: All label text

CRITICAL:
- Hand-drawn editorial style on BOTH sides
- Clear visual contrast between sides
- Mirror structure -- parallel elements contrasted
- Equal visual weight to both sides
- No gradients, flat colors only
- Immediate visual understanding of the difference
```

### Step 4: Determine Aspect Ratio

| Split Type | Default Aspect Ratio |
|------------|---------------------|
| Vertical split (left/right) | 16:9 or 1:1 |
| Horizontal split (top/bottom) | 9:16 or 1:1 |
| Square balanced | 1:1 |
| Social media | 1:1 |

Default: 16:9 (classic side-by-side)

### Step 5: Generate

```bash
bun run ~/dev/cg-claude-workspaces-plugins/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[YOUR PROMPT]" \
  --size 2K \
  --aspect-ratio 16:9 \
  --output ~/Downloads/[descriptive-name].png
```

Then immediately open:
```bash
open ~/Downloads/[descriptive-name].png
```

### Step 6: Validate

**Must have:**
- [ ] Clear split -- obvious division between two sides
- [ ] Visual contrast -- metaphors clearly show the difference
- [ ] Balanced composition -- equal visual weight to both sides
- [ ] Readable labels -- side names and annotations legible
- [ ] Color differentiation -- purple/teal distinguishes sides
- [ ] Hand-drawn -- both sides maintain editorial aesthetic
- [ ] Immediate understanding -- difference obvious at a glance

**Must NOT have:**
- [ ] Unbalanced sides (one dominates)
- [ ] Unclear which is which
- [ ] Corporate comparison chart look
- [ ] Gradients or photorealistic elements
- [ ] Missing dividing line or separation

**If validation fails:**

| Problem | Fix |
|---------|-----|
| Sides unclear | "Strong black dividing line, clear LEFT: vs RIGHT: labels" |
| Not balanced | "Equal visual weight, mirror structure, parallel composition" |
| Contrast weak | "Stronger metaphor contrast: [Side A metaphor] vs [Side B opposite]" |
| Too complex | Simplify each side to single clear metaphor |
| Colors confusing | "Purple accents left side only, Teal accents right side only" |
| Looks corporate | "Editorial split composition, hand-drawn contrast illustration" |

## Model Selection

| User Says | Flag |
|---|---|
| "fast", "quick" | --model nano-banana |
| default / "best" | --model nano-banana-pro |
| "flux" | --model flux |

## Examples

| Comparison | Split | Left (Purple) | Right (Teal) |
|------------|-------|---------------|--------------|
| Junior vs Senior | Vertical | Complex spaghetti code | Simple elegant solution |
| Before AI vs After AI | Horizontal | Manual tedious work | Automated flow |
| Security Theater vs Real | Vertical | Fancy locks on cardboard | Simple solid construction |

## Outputs

| File | Use For |
|------|---------|
| `[name].png` | Full resolution comparison |
| Add `--thumbnail` | If going into blog (transparent + sepia versions) |
