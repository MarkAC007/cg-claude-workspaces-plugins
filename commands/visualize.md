# /art:visualize -- Adaptive Multi-Modal Visualization

## Purpose

Intelligent visualization orchestrator that analyzes content and selects the optimal approach -- single-mode, hybrid, or multi-panel infographic. Uses Excalidraw whiteboard aesthetic for infographics with rich hand-drawn graphics. Default background: Light Cream #F5E6D3.

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running the Visualize workflow", "voice_id": "25"}' \
  > /dev/null 2>&1 &
```

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Visualize this content"
- "What's the best way to show this?"
- Content with multiple dimensions (data + narrative + concepts)
- Professional infographics or slides
- When you aren't sure which specific art command to use
- NOT for blog headers (use /art:generate) or technical diagrams (use /art:diagram)

## Workflow Steps (ALL 6 MANDATORY)

### Step 1: Deep Content Analysis (Use Extended Thinking)

Analyze the content across these dimensions:

**A. Content Type Identification:**
- [ ] Quantitative data (numbers, statistics, metrics)
- [ ] Qualitative concepts (ideas, principles, arguments)
- [ ] Narrative elements (stories, sequences, transformations)
- [ ] Comparative elements (X vs Y, before/after)
- [ ] Hierarchical structures (taxonomies, frameworks)
- [ ] Temporal elements (timelines, evolution)
- [ ] Process flows (steps, recipes, methodologies)

**B. Communication Goal:**
- Explain complex concept --> Conceptual visualization
- Show data insights --> Data visualization dominant
- Compare alternatives --> Comparison/split approach
- Tell a story --> Sequential/narrative visualization
- Organize information --> Taxonomy/grid approach
- Make memorable --> Metaphor + data hybrid

**C. Complexity Assessment:**
- Simple (1-2 key points): Single focused visualization
- Medium (3-5 dimensions): Hybrid or two-element composition
- Complex (6+ dimensions): Multi-panel infographic or dashboard

Output:
```
CONTENT TYPE: [Primary and secondary types]
INFORMATION DENSITY: [Simple / Medium / Complex]
COMMUNICATION GOAL: [Primary purpose]
KEY ELEMENTS TO VISUALIZE: [List elements by type]
```

### Step 2: Visualization Strategy Selection (Use Extended Thinking)

**Decision Framework:**

```
IF content has 1 primary dimension:
  --> Use specialized workflow directly (editorial, technical, timeline, etc.)

IF content has 2-3 dimensions of equal importance:
  --> Design HYBRID composition

IF content has 4+ distinct dimensions:
  --> Design MULTI-PANEL infographic

IF primarily quantitative:
  --> Lead with DATA VISUALIZATION, add conceptual context

IF primarily conceptual:
  --> Lead with METAPHOR/FRAMEWORK, add data as evidence

IF tells a story:
  --> Use SEQUENTIAL approach (comic, timeline, multi-step)
```

**Strategy Options:**

| Strategy | When | Example |
|----------|------|---------|
| Single-Mode | Content fits one type | Pure data chart, single framework |
| Hybrid | 2-3 equal dimensions | Data + Metaphor, Timeline + Data |
| Multi-Panel | 4+ dimensions, complex | Dashboard grid, layered infographic |

Output:
```
VISUALIZATION STRATEGY: [Single-mode / Hybrid / Multi-panel]
COMPOSITION ELEMENTS:
  Primary (60-70%): [Type and purpose]
  Secondary (20-30%): [Type and purpose]
  Tertiary (10%): [Optional]
ASPECT RATIO: [1:1 / 16:9 / 9:16 / 4:3]
```

### Step 3: Design Composition (Use Extended Thinking)

**Excalidraw Infographic Aesthetic (for infographics):**
- WOBBLY BOXES -- rectangles with rough, hand-drawn edges
- SKETCHY LINES -- arrows and connections with slight wobble
- IMPERFECT SHAPES -- circles slightly oval, diamonds asymmetric
- HAND-LETTERED TEXT -- labels look handwritten, not typed
- VARIABLE LINE WEIGHT -- heavier for boxes, lighter for details

**Color Strategy:**
- Black (#000000): All primary structure (boxes, arrows, icons)
- Deep Purple (#4A148C): Critical elements, key stats, title (10-20%)
- Deep Teal (#00796B): Secondary highlights (5-10%)
- Charcoal (#2D2D2D): All text labels
- Background: Light Cream #F5E6D3 (DEFAULT)

**Typography System (3-Tier):**

| Tier | Font Style | Usage | Size |
|------|-----------|-------|------|
| 1 | Valkyrie serif italic (title), regular (subtitle) | Main header + subtitle | 3-4x body (title), 1-1.5x (subtitle) |
| 2 | Concourse geometric sans | Panel headers, labels | Medium readable |
| 3 | Advocate condensed italic | Annotations, insights | 60% of Tier 2 |

Title and subtitle ALWAYS left-justified, never centered.

### Step 4: Construct Comprehensive Prompt (Use Extended Thinking)

Build using the template:

```
[VISUALIZATION TYPE] in editorial infographic style optimized for Nano Banana Pro.

OVERALL CONCEPT: "[What this visualization communicates]"

STYLE: [For infographics] Excalidraw whiteboard sketch aesthetic
- Wobbly rectangles with rough edges
- Sketchy arrows with slight wobble
- Imperfect shapes throughout
- Hand-lettered text labels
- Whiteboard/sketch paper feel

BACKGROUND: Light Cream #F5E6D3

TYPOGRAPHY SYSTEM (3-TIER):
TIER 1 - TITLE: "[Title]" Valkyrie serif italic, LEFT-JUSTIFIED, large
SUBTITLE: "[Subtitle]" Valkyrie serif regular, below title
TIER 2 - LABELS: Concourse geometric sans, medium, charcoal
TIER 3 - ANNOTATIONS: Advocate condensed italic, small, purple or teal

[ELEMENT SPECIFICATIONS for each major element:]
- Type (chart/icon/illustration/text)
- Size (% of canvas), Position, Style
- Color assignments

COLOR USAGE:
- Black: All primary structure
- Purple #4A148C: Critical data points, key insights
- Teal #00796B: Secondary data, supporting elements
- Charcoal #2D2D2D: All text

CRITICAL: Flat colors only, no gradients. Strategic color, not everywhere.
```

### Step 5: Generate

```bash
bun run ~/dev/cg-claude-workspaces-plugins/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[YOUR COMPREHENSIVE PROMPT]" \
  --size 2K \
  --aspect-ratio [chosen ratio] \
  --output ~/Downloads/[descriptive-name].png
```

Then immediately open:
```bash
open ~/Downloads/[descriptive-name].png
```

### Step 6: Comprehensive Validation

**Information Effectiveness:**
- [ ] Primary message clear within 3 seconds
- [ ] Data accuracy -- numbers, proportions correct
- [ ] Visual hierarchy works -- eye flows primary to secondary to tertiary
- [ ] All elements readable
- [ ] Story cohesion -- elements work together

**Design Quality:**
- [ ] Professional deliverable quality
- [ ] Typography hierarchy clear -- 3 tiers obviously distinct
- [ ] Color strategic -- purple/teal highlight key elements, not overwhelming
- [ ] Composition balanced
- [ ] Excalidraw hand-drawn aesthetic (for infographics)

**Technical Execution:**
- [ ] Text rendering clean
- [ ] No gradients or shadows -- flat aesthetic
- [ ] Aspect ratio appropriate
- [ ] Scale works -- readable as thumbnail AND full-size

**If validation fails:** Diagnose using this table, fix, regenerate.

| Problem | Fix |
|---------|-----|
| Too cluttered | Reduce to 2-3 main elements, increase whitespace |
| Message unclear | Strengthen primary element (larger, add purple) |
| Text unreadable | Increase label sizes, strengthen tier differentiation |
| Looks generic | Add hand-drawn editorial elements, strategic purple/teal |
| Color chaos | Limit purple to 2-3 key elements, teal to 1-2, rest black |

## Model Selection

| User Says | Flag |
|---|---|
| "fast", "quick", "draft" | --model nano-banana |
| default / "best" | --model nano-banana-pro |
| "flux" | --model flux |

## Visualization Pattern Library

| Pattern | When | Layout |
|---------|------|--------|
| Data + Metaphor | Data needs context | 50% data + 40% illustration + 10% text |
| Comparative Dashboard | Multiple comparison dimensions | Split or grid |
| Process + Outcomes | Method with results | Vertical or horizontal flow |
| Icon Quantification | Showing quantities | Grid of icons |
| Annotated Data Story | Data needs narrative | Chart with hand-drawn annotations |
| Multi-Chart Dashboard | Multiple related datasets | 2-4 chart grid |
| Framework + Data | Conceptual model + evidence | Framework structure with data per zone |
| Infographic Slide | Comprehensive presentation | Title + mini-charts + stats + insight |

## Outputs

| File | Use For |
|------|---------|
| `[name].png` | Full resolution visualization |
| Add `--thumbnail` flag | If going into blog post (creates transparent + sepia versions) |
