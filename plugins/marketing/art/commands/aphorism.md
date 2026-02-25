# /art:aphorism -- Visual Quote Cards

## Purpose

Creates visual aphorism cards -- giant bold typography as the hero element with a minimal hand-drawn accent. The quote IS the visual (80-90% of the image). Designed for shareable social media content, newsletter pull quotes, and thought leadership visuals. Square 1:1 format. High contrast. Hand-lettered quality.

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Make a quote card for..."
- "Create a visual aphorism..."
- "Turn this quote into an image"
- "Make a shareable image with this text"
- Social media quote cards (LinkedIn, Instagram, X)
- Newsletter pull quotes
- Thought leadership visuals
- "HUMANS NEED ENTROPY" style statements

## Workflow Steps (ALL MANDATORY)

### Step 1: Select and Prepare the Aphorism

1. **Extract the quote** -- must be punchy and memorable. Ideal length: 2-8 words.
2. **Identify the insight** -- why is this quote powerful? Why is it shareable?
3. **Choose a tiny visual accent** -- NOT a full illustration. A small simple element reinforcing the idea (5-10% of image area). Examples: scattered dots for entropy, em dash symbol for typography, lightning bolt for insight.

Output:
```
APHORISM: "[QUOTE IN ALL-CAPS]"
LENGTH: [X words]
INSIGHT: [Why this quote resonates]
ACCENT ELEMENT: [Tiny illustration description]
```

### Step 2: Design Typography Layout

Plan the visual composition:

1. **Typography arrangement:**
   - All one line (short quote, 2-3 words)
   - Multiple lines (longer quote, natural line breaks)
   - Stacked words (vertical emphasis)
   - Asymmetric layout (dynamic placement)

2. **Size and weight:**
   - Text fills 80-90% of frame
   - Line breaks create rhythm and emphasis
   - Key words can be larger than others

3. **Color scheme** (pick one):
   - Black text on light cream (#F5E6D3) -- most common
   - Purple (#4A148C) text on white -- bold brand
   - White text on black -- high drama
   - White text on purple (#4A148C) -- bold brand dark

4. **Accent placement:**
   - Bottom right corner (most common)
   - Top left (alternative)
   - Must NOT compete with text
   - Size: 5-10% of image area
   - Color: Purple (#4A148C) or Teal (#00796B)

### Step 3: Construct Prompt

Build the generation prompt:

```
Typographic quote card in editorial hand-lettered style.

STYLE: Bold typography poster, quote card, hand-lettered aphorism. Typography as primary visual (dominates composition). Hand-lettered Advocate style (imperfect, gestural, bold). Massive scale lettering fills 80-90% of frame. Minimal accent illustration (subtle, not competing). High contrast for readability. Square 1:1 format.

BACKGROUND: [Light Cream #F5E6D3 / White #FFFFFF / Black #000000 / Purple #4A148C] -- flat, solid.

TYPOGRAPHY (Advocate Block Display - MASSIVE):
"[APHORISM TEXT IN ALL-CAPS]"
- Font: Advocate style extra bold, hand-lettered, all-caps
- Size: MASSIVE -- fills most of image area
- Layout: [Single line / Multi-line / Stacked]
- Line breaks:
  Line 1: "[FIRST PART]"
  Line 2: "[SECOND PART]" (optionally larger)
- Color: [Black #000000 / Purple #4A148C / White #FFFFFF]
- Hand-lettered with imperfections, NOT perfect digital font
- Variable letter sizing for emphasis

ACCENT ILLUSTRATION (Minimal):
- [Small simple element description]
- Hand-drawn, simple, editorial style
- Position: [Bottom right / Top left]
- Size: 5-10% of image area
- Color: [Purple #4A148C / Teal #00796B]
- Subtle visual reinforcement, NOT competing focal point

CRITICAL: Typography is HERO. Hand-lettered quality. NOT a digital font. Accent MINIMAL. High contrast readability. No gradients, flat colors only. Shareable social media quality.
```

### Step 4: Aspect Ratio

**Always 1:1 (square)** -- optimized for social media (Instagram, LinkedIn, X).

### Step 5: Generate

```bash
bun run ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[YOUR CONSTRUCTED PROMPT]" \
  --size 2K \
  --aspect-ratio 1:1 \
  --output ~/Downloads/aphorism.png
```

Immediately open for review:
```bash
open ~/Downloads/aphorism.png
```

### Step 6: Validate

**Must Have:**
- [ ] Quote readable -- instantly legible even at thumbnail size
- [ ] Typography dominant -- quote is 80-90% of visual
- [ ] Hand-lettered -- imperfect, gestural quality (not digital font)
- [ ] High contrast -- text pops from background
- [ ] Minimal accent -- small element supports, does not compete
- [ ] Shareable -- works as social media post
- [ ] Brand presence -- purple visible somewhere

**Must NOT Have:**
- [ ] Perfect digital font
- [ ] Busy background or complex illustration
- [ ] Low contrast
- [ ] Accent competing with quote
- [ ] Tiny text
- [ ] Gradients or shadows

**Fix Table:**

| Problem | Fix |
|---------|-----|
| Text too small | "MASSIVE hand-lettered typography filling 85% of frame" |
| Looks like digital font | "Hand-drawn Advocate letters, imperfect wobbly strokes" |
| Accent too busy | "MINIMAL accent: small simple [element], 8% of image" |
| No brand presence | "Purple (#4A148C) on [accent / text / background]" |
| Too complex | "Typography IS the visual, quote dominant, minimal everything else" |

## Outputs

- `~/Downloads/aphorism.png` -- the generated quote card image (1:1 square)
- Move to project directory only after validation passes
