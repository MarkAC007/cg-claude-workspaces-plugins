# /art:stat -- Illustrated Stat Cards

## Purpose

Creates illustrated stat cards -- a single striking statistic made visual with a small supporting illustration. The number dominates (60-70% of the visual) with a brief illustration showing what the stat represents (20-30%). Purple (#4A148C) for the number. Designed for newsletters, social media, and quick visual facts.

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running the Stat workflow", "voice_id": "25"}' \
  > /dev/null 2>&1 &
```

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Make a stat card for..."
- "Visualize this statistic..."
- "Create an illustrated number for..."
- "Turn this data point into an image"
- Newsletter "by the numbers" sections
- Social media stat cards
- Quick visual facts and data highlights
- "78% of developers use AI daily" style visuals

## Workflow Steps (ALL MANDATORY)

### Step 1: Extract the Statistic

1. **Identify the number** -- the exact statistic (e.g., "78%", "$2.1B", "3.5X"). Must be striking or surprising.
2. **Define the metric** -- what is being measured? This becomes the text above the number (e.g., "of developers").
3. **Add context** -- brief description below the number (e.g., "use AI tools daily").
4. **Choose illustration** -- a small, simple visual that shows what the stat represents. NOT a complex scene, just a small icon or figure (20-30% of image). Examples: tiny developer at computer, stack of coins, growing arrow.

Output:
```
STATISTIC: [Number + unit]
METRIC: [What is being measured -- text above number]
CONTEXT: [What this means -- text below number]
ILLUSTRATION: [Small visual element and its meaning]
```

### Step 2: Design Stat Card Layout

Plan the visual composition:

1. **Number placement:**
   - Center dominant (number in middle) -- most common
   - Left number, right illustration
   - Top number, bottom illustration

2. **Number size:** Should fill 50-60% of image height, immediately visible.

3. **Illustration placement:** Relative to number (below, beside, integrated). Size: 20-30% of image.

4. **Text placement:**
   - Metric description above the number (small)
   - Context note below the number (small)

5. **Color scheme:**
   - Number: Purple (#4A148C) -- most common, brand emphasis
   - Number: Black (#000000) -- alternative classic
   - Illustration: Black linework with purple accents
   - Background: Light cream (#F5E6D3) or white (#FFFFFF)
   - Text: Charcoal (#2D2D2D)

### Step 3: Construct Prompt

Build the generation prompt:

```
Illustrated statistic card in editorial style.

STYLE: Data visualization, stat card, number + icon illustration. Number as dominant visual. Hand-drawn imperfect number rendering. Editorial flat color with strategic purple. Scannable, immediate impact.

BACKGROUND: [Light Cream #F5E6D3 / White #FFFFFF] -- flat, clean.

NUMBER TYPOGRAPHY (Advocate Block Display - MASSIVE):
"[STATISTIC]"
- Font: Advocate style extra bold, hand-lettered
- Size: MASSIVE -- 60-70% of image area
- Color: Deep Purple #4A148C
- Hand-lettered with imperfections, NOT digital font
- Position: [Center / Left / Top]

METRIC TEXT (Concourse Sans - Medium):
"[what the stat measures]"
- Size: 15-20% of number size
- Color: Charcoal (#2D2D2D)
- Position: Above number

CONTEXT TEXT (Advocate Condensed - Small):
"[additional context]"
- Size: 10-15% of number size
- Color: Charcoal (#2D2D2D)
- Position: Below number

ILLUSTRATION (Small, Simple):
- [Description of icon/figure]
- Hand-drawn black (#000000) linework
- Purple (#4A148C) accents on [specific elements]
- Position: [Bottom right / Next to number]
- Size: 20-30% of image area
- Simple sketch, not detailed

CRITICAL: Number is HERO (60-70%). Hand-lettered quality. Illustration SMALL and SIMPLE. High contrast. Strategic purple emphasis. No gradients. Scannable at thumbnail.
```

### Step 4: Determine Aspect Ratio

| Use Case | Aspect Ratio | Notes |
|----------|-------------|-------|
| Social media | 1:1 | Instagram/LinkedIn friendly |
| Newsletter inline | 16:9 | Fits email width |
| Mobile story | 9:16 | Instagram story format |

**Default: 1:1 (square)** -- most versatile.

### Step 5: Generate

```bash
bun run ~/dev/cg-claude-workspaces-plugins/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[YOUR CONSTRUCTED PROMPT]" \
  --size 2K \
  --aspect-ratio 1:1 \
  --output ~/Downloads/stat-card.png
```

Immediately open for review:
```bash
open ~/Downloads/stat-card.png
```

### Step 6: Validate

**Must Have:**
- [ ] Number dominant -- statistic is 60-70% of visual, immediately visible
- [ ] Readable number -- clear even at thumbnail size
- [ ] Hand-lettered -- imperfect, gestural quality (not digital font)
- [ ] Illustration simple -- small supporting visual, not complex scene
- [ ] Context clear -- metric/context text explains what number means
- [ ] High contrast -- purple or black number pops from background
- [ ] Scannable -- number jumps out immediately

**Must NOT Have:**
- [ ] Number too small
- [ ] Digital font rendering
- [ ] Complex detailed illustration
- [ ] Illustration competing with number
- [ ] Low contrast
- [ ] Missing context

**Fix Table:**

| Problem | Fix |
|---------|-----|
| Number too small | "MASSIVE hand-lettered number filling 65% of image height" |
| Looks digital | "Hand-drawn Advocate style, wobbly imperfect strokes" |
| Illustration too complex | "SMALL SIMPLE illustration, minimal detail, 25% of image" |
| Unclear meaning | Add metric text above and context text below the number |
| No visual interest | Add "Small illustrated [icon] showing what stat represents" |

## Outputs

- `~/Downloads/stat-card.png` -- the generated stat card image
- Move to project directory only after validation passes
