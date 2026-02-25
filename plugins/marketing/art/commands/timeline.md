# /art:timeline -- Chronological Progressions & Evolution Timelines

## Purpose

Create hand-drawn illustrated timelines showing evolution, trends, and transformations with visual metaphors at each milestone. Unlike simple date lists, these timelines use illustrated milestones to show transformation, not just chronology. Shows the narrative arc of change over time.

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Show the evolution of X"
- "Create a timeline for..."
- "Trend analysis over time"
- "Historical perspective on..."
- "Before, during, after progression"
- "Transformation journey"
- Era comparisons, trend visualizations

## Workflow Steps (ALL 6 MANDATORY)

### Step 1: Define Timeline Structure

Identify what you are showing:

1. **What is evolving?** (e.g., AI development, security paradigms, organizational thinking)
2. **Time span?** (e.g., 1990-2025, past 5 years, projected future)
3. **Key milestones?** (List 4-8 major points -- too many becomes cluttered)
4. **What is the narrative arc?** (e.g., collapse -> crisis -> renewal, winter -> spring -> summer)

**Template:**
```
SUBJECT: [What's changing over time]
TIME SPAN: [Start] --> [End]
NARRATIVE ARC: [The transformation story]

KEY MILESTONES:
1. [Year/Period]: [Event] -- [Metaphor for this stage]
2. [Year/Period]: [Event] -- [Metaphor]
3. [Year/Period]: [Event] -- [Metaphor]
4. [Year/Period]: [Event] -- [Metaphor]
...

TURNING POINTS (Purple highlights):
- [Which 1-2 milestones are most critical]
```

### Step 2: Design Timeline Layout

**Orientation options:**
- Horizontal (left-to-right): Traditional, good for desktop/wide (DEFAULT)
- Vertical (top-to-bottom): Mobile-friendly, scrollable
- Curved/organic: More artistic, less rigid

**Milestone representation:**
- Small illustrated metaphor at each point (seedling, storm, sunrise, etc.)
- Size variation: bigger for more important events
- Milestones connect above/below the timeline spine

**Spacing:** Even (visual balance), proportional (matches time), or clustered (groups related events)

**Color System:**
- Black #000000: Timeline spine, all primary structure
- Purple #4A148C: 1-2 critical turning points
- Teal #00796B: Supporting important milestones
- Charcoal #2D2D2D: All text (dates, labels, annotations)
- Background: White #FFFFFF or Light Cream #F5E6D3

### Step 3: Construct Prompt

```
Hand-drawn conceptual timeline in editorial illustration style.

STYLE: Illustrated history timeline, hand-drawn progress chart
BACKGROUND: [White #FFFFFF or Light Cream #F5E6D3]

AESTHETIC:
- Hand-drawn timeline (organic line, slightly wobbly, NOT ruler-straight)
- Small illustrated metaphors at each milestone
- Variable stroke weight (timeline thicker, details thinner)
- Editorial flat color with strategic purple/teal accents

ORIENTATION: [Horizontal left-to-right / Vertical top-to-bottom]

TIMELINE STRUCTURE:
- Black (#000000) timeline spine running [direction]
- [Number] milestone points along timeline
- Each milestone: small circle/node + illustration + label
- Hand-drawn connecting line with slight organic waviness

TYPOGRAPHY (3-TIER):
TIER 1 - TITLE: "[TIMELINE TITLE]"
  Advocate style, extra bold, hand-lettered, all-caps, 3x body, black, top
TIER 2 - DATES/PERIODS: "[1990]", "[2000]", etc.
  Concourse geometric sans, medium, charcoal, along timeline
TIER 3 - MILESTONE DESCRIPTIONS: "*symbolic AI era*", "*breakthrough*"
  Advocate condensed italic, 60% of Tier 2, charcoal (or purple/teal for highlights)

MILESTONES:
1. [Year]: [Event]
   - Illustration: [Small hand-drawn icon/metaphor]
   - Color: Black node, charcoal text
2. [Year]: [CRITICAL EVENT]
   - Illustration: [Metaphor]
   - Color: Purple (#4A148C) node -- KEY TURNING POINT
3. [Year]: [Event]
   - Illustration: [Metaphor]
   - Color: Teal (#00796B) node
[Continue for all milestones...]

VISUAL METAPHORS:
- Each milestone illustrated with simple recognizable icon
- Icons show the nature/feeling of that era
- Hand-drawn sketch quality, not detailed
- Examples: seedling, storm cloud, rising sun, mountain peak, valley

COLOR USAGE:
- Black: Timeline spine and most nodes
- Purple: [1-2 critical turning points]
- Teal: [Supporting events]
- Charcoal: All text

CRITICAL:
- Hand-drawn timeline (NOT straight digital line)
- Clear temporal progression
- Small illustrated metaphors at each point
- 3-tier typography hierarchy
- Strategic color on key milestones only
- No gradients, flat colors only
```

### Step 4: Determine Aspect Ratio

| Timeline Type | Default Aspect Ratio |
|---------------|---------------------|
| Horizontal timeline | 16:9 (default) |
| Long historical | 21:9 |
| Vertical timeline | 9:16 |
| Balanced/compact | 1:1 |

Default: 16:9 (horizontal)

### Step 5: Generate

```bash
bun run ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art/tools/Generate.ts \
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
- [ ] Clear temporal flow -- obviously progresses through time
- [ ] Readable dates/labels -- all text legible in hierarchy
- [ ] Illustrated milestones -- visual metaphors at each point (not just dots)
- [ ] Hand-drawn timeline -- organic line, not digital/straight
- [ ] Narrative arc visible -- shows transformation, not just dates
- [ ] Strategic color -- purple on critical moments, not everywhere
- [ ] Scannable -- easy to follow progression at a glance

**Must NOT have:**
- [ ] Perfectly straight timeline
- [ ] Generic boring milestone markers (just dots)
- [ ] Illegible dates or cluttered text
- [ ] Too many milestones (overwhelming)
- [ ] Color chaos (everything highlighted)
- [ ] Looks like Gantt chart or business timeline

**If validation fails:**

| Problem | Fix |
|---------|-----|
| Timeline too straight | "Organic hand-drawn line, slight waviness, imperfect curve" |
| No visual interest | "Small illustrated metaphors at each milestone" |
| Text unreadable | Increase spacing, strengthen typography tier sizes |
| Too cluttered | Reduce milestones to 4-6 key points |
| Looks corporate | "Editorial illustration style, hand-drawn sketch aesthetic" |
| Missing narrative | Emphasize metaphors showing transformation |

## Model Selection

| User Says | Flag |
|---|---|
| "fast", "quick" | --model nano-banana |
| default / "best" | --model nano-banana-pro |
| "flux" | --model flux |

## Metaphor Selection Guide

Choose simple, recognizable icons for each era:

| Stage | Example Metaphors |
|-------|-------------------|
| Beginning | Seedling, spark, first step |
| Growth | Sprout, rising tide, climbing |
| Crisis | Storm cloud, crack, falling |
| Turning point | Lightning bolt, crossroads |
| Recovery | Sunrise, phoenix, bridge |
| Maturity | Oak tree, mountain summit |
| Decline | Sunset, falling leaves |
| Renewal | New seedling, spring bud |

## Outputs

| File | Use For |
|------|---------|
| `[name].png` | Full resolution timeline |
| Add `--thumbnail` | If going into blog (transparent + sepia versions) |
