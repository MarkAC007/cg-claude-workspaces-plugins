# /art:diagram -- Technical Diagrams (Excalidraw-Style)

## Purpose

Create clean Excalidraw-style technical diagrams for system architecture, process flows, pipelines, infrastructure maps, and board presentations. Uses a pure sepia #EAE9DF background with NO grid, Butterick font hierarchy (Valkyrie, Concourse, Advocate), and strategic purple/teal accents.

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running the Diagram workflow", "voice_id": "25"}' \
  > /dev/null 2>&1 &
```

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Create an architecture diagram"
- "Draw a system diagram"
- "Make a process flow diagram"
- "Infrastructure diagram for..."
- Freeform architecture diagrams, pipelines, infrastructure maps
- Board presentation visuals
- NOT for Mermaid-structured diagrams (use /art:flowchart instead)

## Workflow Steps (ALL MANDATORY)

### Step 1: Run Story Explanation on Content

Extract the full narrative arc from the content using CSE-24:

```
/cse [content or URL]
```

This reveals the structure that needs to be diagrammed -- processes, entities, relationships, decision points.

### Step 2: Think Deeply About the Diagram

Think deeply about how to construct the content into a technical diagram:
- What components/nodes exist?
- What are the relationships between them?
- What is the hierarchy or flow direction?
- What are the critical paths vs. secondary paths?

### Step 3: Design the Composition

**Core Visual Rules:**
- Pure sepia #EAE9DF background -- NO grid lines, NO texture, NO decorations
- Excalidraw style -- clean lines, slightly organic, professional
- Architect-artist whiteboard aesthetic
- All art components and labels should look hand-drawn

**Background:** Pure Black #000000 (for the AI prompt -- renders as dark architect board)

**Color Palette:**

| Color | Hex | Usage | Amount |
|-------|-----|-------|--------|
| Sepia | #EAE9DF | Background | 100% |
| Purple | #4A148C | Key components, insights | 10% |
| Teal | #00796B | Flows, connections | 5% |
| Charcoal | #2D2D2D | Text, labels | 5% |
| White | #FFFFFF | Primary structure | 80% |

### Step 4: Construct the Prompt

**Typography System (3-Tier -- Butterick Fonts):**

**TIER 1 -- Headers (Valkyrie Serif):**
- Header: Elegant wedge-serif ITALIC, large (3-4x body), black, top-left, left-justified
- Subtitle: Same wedge-serif REGULAR (not italic), smaller (1.3x body), charcoal, below header
- Wedge-shaped serifs, high stroke contrast, like Palatino but more refined

**TIER 2 -- Labels (Concourse T3 Geometric Sans):**
- Box labels, node names, technical identifiers
- Geometric sans-serif (like Avenir/Futura but warmer), clean, even stroke weight
- Medium size, charcoal or black
- Hand-drawn versions

**TIER 3 -- Insights (Advocate Condensed Italic):**
- Key insights, commentary, callouts
- Condensed italic sans-serif, sporty editorial feel
- Smaller (60-70% of labels), Purple #4A148C or Teal #00796B
- Always italic, with asterisks: "*this is the bottleneck*"
- Include 1-3 insights per image

**Prompt Structure:**

```
Create a consistent, styled technical diagram using ALL styling guidelines.

BACKGROUND: Pure Black #000000 -- NO grid lines, NO texture, completely clean.

STYLE: Architect aesthetic -- like an architect artist on a whiteboard

TYPOGRAPHY:
HEADER: "[TITLE]" -- Elegant wedge-serif italic, large, black, top-left
SUBTITLE: "[SUBTITLE]" -- Same serif regular, smaller, charcoal, below header
LABELS: Geometric sans-serif (warm Avenir-like), medium, charcoal, hand-drawn
INSIGHTS: Condensed italic sans (sporty editorial), small, Purple #4A148C

DIAGRAM CONTENT:
Title: '[TITLE]' (Top left, left-justified)
Subtitle: '[SUBTITLE]' (left-justified below header)

[Describe the full diagram layout, nodes, connections, and flow]

Art and labels should look like Excalidraw but hand-drawn by a talented
Architect Artist. Objects should be technically-drawn, NOT cartoony.

Overall: Whiteboard by an extremely talented artist with Architect training.
```

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
- [ ] Pure sepia background #EAE9DF (NO grid or decorations)
- [ ] Elegant wedge-serif for headers (Valkyrie-style)
- [ ] Geometric sans labels (Concourse-style)
- [ ] A title and subtitle in the top left
- [ ] 1-3 condensed italic insights (Advocate-style)
- [ ] Strategic color usage (accents only, 70% shades of grey and black)
- [ ] Highly technical, stylish, Architect-style Excalidraw feel

**Must NOT have:**
- [ ] Grid lines or texture on background
- [ ] Generic or ugly fonts
- [ ] Cartoony or overly casual shapes or styling
- [ ] Over-coloring (everything purple/teal)

**If validation fails:** Identify issues, update prompt, regenerate, re-validate.

## Model Selection

| User Says | Flag |
|---|---|
| "fast", "quick", "draft" | --model nano-banana |
| default / "best" | --model nano-banana-pro |
| "flux" | --model flux |

## Aspect Ratio

| User Says | Flag |
|---|---|
| "wide", "slide", "presentation" (default) | --aspect-ratio 16:9 |
| "square" | --aspect-ratio 1:1 |
| "ultrawide", "panoramic" | --aspect-ratio 21:9 |

## Post-Processing

| User Says | Flag |
|---|---|
| "blog", "website" | --thumbnail |
| "transparent" | --remove-bg |
| "variations" | --creative-variations 3 |

## Outputs

| File | Use For |
|------|---------|
| `[name].png` | Full resolution diagram |
| `[name]-thumb.png` | Thumbnail (if --thumbnail used) |
