# /art:framework -- Visual Mental Models & Frameworks

## Purpose

Create hand-drawn visual frameworks -- 2x2 matrices, Venn diagrams, pyramids, spectrums, and conceptual relationship maps. These become THE signature reference image for a mental model, combining clear structure with editorial hand-drawn aesthetic. Purple for the optimal zone, teal for contrast.

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running the Framework workflow", "voice_id": "25"}' \
  > /dev/null 2>&1 &
```

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Create a 2x2 matrix for..."
- "Venn diagram showing..."
- "The framework for X"
- "Mental model for..."
- "Decision framework"
- "Pyramid diagram"
- Conceptual relationship maps and thinking tools
- Any structured mental model that needs a visual

## Supported Framework Types

| Type | Structure | Default Aspect |
|------|-----------|----------------|
| 2x2 Matrix | Two axes, four quadrants | 1:1 |
| Venn Diagram | 2-3 overlapping circles | 1:1 |
| Pyramid | Stacked levels, bottom to top | 1:1 or 4:3 |
| Spectrum/Continuum | Left-to-right range | 16:9 |
| Triangle | Three-way balance | 1:1 |
| Concentric Circles | Nested rings, center outward | 1:1 |

## Workflow Steps (ALL 6 MANDATORY)

### Step 1: Define Framework Structure

Identify the mental model:

1. **What framework type?** (2x2, Venn, pyramid, spectrum, triangle, other)
2. **What are the dimensions/concepts?**
   - For 2x2: X-axis concept, Y-axis concept
   - For Venn: Circle 1, Circle 2, overlap meaning
   - For pyramid: Levels from bottom to top
3. **What are the quadrants/areas/zones?** Name and describe each region
4. **Which zone is "optimal" or most important?**

**Template:**
```
FRAMEWORK TYPE: [2x2 Matrix / Venn Diagram / Pyramid / Spectrum / etc.]
FRAMEWORK NAME: "The [Name] Framework for [Topic]"

DIMENSIONS:
- X-axis: [Concept] (Low --> High)
- Y-axis: [Concept] (Low --> High)

QUADRANTS/AREAS:
1. [Name]: [Description] -- [Color if highlighted]
2. [Name]: [Description]
3. [Name]: [Description]
4. [Name]: [Description]

OPTIMAL ZONE: [Which quadrant/area is ideal]
```

### Step 2: Design Framework Visual

Plan the visual representation:

**Geometry:** Size, proportions, spacing, symmetry or intentional asymmetry

**Color Assignment:**
- Purple #4A148C: Optimal zone / primary concept (subtle accent, not solid fill)
- Teal #00796B: Contrast zone / secondary concept (subtle accent)
- Black #000000: All framework structure (axes, circles, boxes)
- Charcoal #2D2D2D: All text and labels
- Background: White #FFFFFF or Light Cream #F5E6D3

**Typography Placement:**
- Title (Tier 1): Top center or top-left
- Axis/zone labels (Tier 2): Along axes, inside quadrants
- Annotations (Tier 3): Near relevant zones: "*optimal zone*", "*avoid this*"

### Step 3: Construct Prompt

```
Hand-drawn conceptual framework diagram in editorial style.

STYLE: Mental model illustration, conceptual diagram with personality
BACKGROUND: [White #FFFFFF or Light Cream #F5E6D3]

AESTHETIC:
- Hand-drawn framework structure (wobbly lines, organic shapes)
- Variable stroke weight (axes thicker, details thinner)
- Imperfect but intentional geometry
- Editorial flat color with strategic purple/teal accents

FRAMEWORK TYPE: [2x2 Matrix / Venn / Pyramid / etc.]

FRAMEWORK STRUCTURE:
[Describe specific geometry, e.g.:]
- Two hand-drawn perpendicular axes (black) forming cross
- X-axis: [Low concept] left --> [High concept] right
- Y-axis: [Low concept] bottom --> [High concept] top
- Four quadrants created by intersection

TYPOGRAPHY (3-TIER):
TIER 1 - TITLE: "[FRAMEWORK NAME]"
  Advocate style, extra bold, hand-lettered, all-caps, 3x body, black, top center
TIER 2 - LABELS: Axis labels and quadrant names
  Concourse geometric sans, medium, charcoal, along axes and inside quadrants
TIER 3 - ANNOTATIONS: "*optimal zone*", "*avoid this quadrant*"
  Advocate condensed italic, 60% of Tier 2, purple or teal

QUADRANTS/AREAS:
TOP-RIGHT: [Name] -- Purple (#4A148C) subtle accent -- OPTIMAL ZONE
  Annotation: "*ideal state*" in purple italic
TOP-LEFT: [Name] -- Black structure only
BOTTOM-RIGHT: [Name] -- Teal (#00796B) subtle accent -- CONTRAST ZONE
BOTTOM-LEFT: [Name] -- Black structure only

COLOR USAGE:
- Black: All framework structure
- Purple: [Optimal zone] subtle fill or accent
- Teal: [Contrast zone] subtle accent
- Charcoal: All text except emphasized annotations

CRITICAL:
- Hand-drawn imperfect geometry (NOT digital precision)
- Framework structure immediately recognizable
- Clear labels in 3-tier hierarchy
- Strategic color on 1-2 key zones only (subtle, not solid fills)
- No gradients, flat colors only
- Conceptually clear and memorable
```

### Step 4: Determine Aspect Ratio

| Framework Type | Default Aspect Ratio |
|----------------|---------------------|
| 2x2 Matrix | 1:1 |
| Venn Diagram | 1:1 |
| Pyramid | 1:1 or 4:3 |
| Spectrum | 16:9 |
| Triangle | 1:1 |

Default: 1:1 (square)

### Step 5: Generate

```bash
bun run ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[YOUR PROMPT]" \
  --size 2K \
  --aspect-ratio 1:1 \
  --output ~/Downloads/[descriptive-name].png
```

Then immediately open:
```bash
open ~/Downloads/[descriptive-name].png
```

### Step 6: Validate

**Must have:**
- [ ] Framework structure clear -- 2x2/Venn/Pyramid immediately recognizable
- [ ] Readable labels -- all text legible in 3-tier hierarchy
- [ ] Hand-drawn aesthetic -- imperfect lines, organic shapes, human quality
- [ ] Strategic color -- purple on optimal zone, teal on contrast, not everywhere
- [ ] Conceptually memorable -- becomes THE reference image for this framework
- [ ] Editorial style -- flat color, black linework

**Must NOT have:**
- [ ] Perfect digital geometry (too clean)
- [ ] Illegible or cluttered text
- [ ] Color overload (solid fills everywhere)
- [ ] Confusing structure (can't identify framework type)
- [ ] Corporate/boring diagram look
- [ ] Gradients or shadows

**If validation fails:**

| Problem | Fix |
|---------|-----|
| Too precise/digital | "Hand-drawn wobbly axes, organic imperfect shapes" |
| Text unreadable | Increase label sizes, simplify annotations |
| Over-colored | "Subtle purple accent on optimal zone only, rest black" |
| Confusing structure | Simplify, stronger geometry cues |
| Looks corporate | "Editorial conceptual illustration, Saul Steinberg style" |
| Not memorable | Add annotation: "*this is the sweet spot*" |

## Model Selection

| User Says | Flag |
|---|---|
| "fast", "quick" | --model nano-banana |
| default / "best" | --model nano-banana-pro |
| "flux" | --model flux |

## Examples

| Framework | Type | Optimal Zone (Purple) |
|-----------|------|----------------------|
| Security vs Convenience | 2x2 Matrix | "Balanced" quadrant (high both) |
| Human + AI Capabilities | Venn (3 circles) | Center overlap |
| Threat Modeling | Pyramid (4 levels) | Top level (Mitigations) |

## Outputs

| File | Use For |
|------|---------|
| `[name].png` | Full resolution framework |
| Add `--thumbnail` | If going into blog (transparent + sepia versions) |
