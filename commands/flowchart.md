# /art:flowchart -- Excalidraw-Style Mermaid Diagrams

## Purpose

Create Excalidraw-style Mermaid diagrams -- flowcharts, sequence diagrams, state machines, class diagrams, and ER diagrams with a hand-drawn whiteboard aesthetic. Combines Mermaid structural grammar with wobbly boxes, sketchy lines, and hand-lettered text. NOT for freeform architecture diagrams (use /art:diagram).

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running the Flowchart workflow", "voice_id": "25"}' \
  > /dev/null 2>&1 &
```

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Create a flowchart for this process"
- "Draw a sequence diagram"
- "State machine diagram for..."
- "ER diagram for this schema"
- Decision trees, algorithmic logic, process flows with conditions
- Interactions between entities over time
- State transitions and lifecycle flows
- NOT for freeform architecture (use /art:diagram)
- NOT for abstract illustrations (use /art:generate)

## Supported Diagram Types

| Type | When to Use | Layout |
|------|-------------|--------|
| Flowchart | Decision trees, process flows with if/then | Top-down or left-right |
| Sequence Diagram | Entity interactions over time, API calls | Actors across top, time down |
| State Diagram | State machines, status transitions, lifecycle | Circular or network |
| Class Diagram | Object relationships, inheritance | Hierarchical tree |
| ER Diagram | Database schemas, data models | Entity spread |
| Gantt Chart | Project timelines, task dependencies | Horizontal timeline |
| Git Graph | Branching strategies, merge flows | Branching horizontal |

## Workflow Steps (ALL 8 MANDATORY)

### Step 1: Run Story Explanation on Content

```
/cse [content or URL]
```

The 24-item output reveals: process flows, decision points, state transitions, entity relationships, temporal ordering.

DO NOT skip this step. DO NOT manually derive diagram structure without running /cse first.

### Step 2: Determine Optimal Diagram Type

**Decision Framework:**

| Choose... | When content has... |
|-----------|---------------------|
| FLOWCHART | Process with decision points, if/then/else logic |
| SEQUENCE DIAGRAM | Interactions between entities over time |
| STATE DIAGRAM | Distinct states with event-driven transitions |
| CLASS/ER DIAGRAM | Object relationships, data structures |
| GANTT CHART | Project timeline, task dependencies |
| GIT GRAPH | Version control workflow, branching |

### Step 3: Extract Diagram Structure from CSE

Map the 24-item story explanation to diagram components:

**For Flowcharts:** Start node, process nodes (rectangles), decision nodes (diamonds), end nodes, flows with labels
**For Sequence Diagrams:** Actors/entities, messages, temporal order, activations
**For State Diagrams:** States, initial/final states, transitions with conditions
**For Class/ER Diagrams:** Entities, attributes, relationships with cardinality

Identify the CRITICAL PATH (highlighted in purple) and ALTERNATIVE PATHS (teal).

### Step 4: Design Excalidraw-Style Layout

**Excalidraw Aesthetic Principles:**
- Wobbly boxes -- rectangles with rough, hand-drawn edges
- Sketchy arrows -- slight wobble, not ruler-straight
- Rough edges -- everything has organic imperfection
- Hand-lettered text -- labels look handwritten, not typed
- Variable line weight -- heavier for boxes, lighter for arrows
- Circles slightly oval, diamonds asymmetric

**Color System:**
- Black #000000: All primary linework (boxes, arrows, decision diamonds)
- Purple #4A148C: Critical path nodes, main flow (10-20% of nodes)
- Teal #00796B: Alternative paths, secondary flows (5-10%)
- Charcoal #2D2D2D: All text labels and annotations
- Background: Light Cream #F5E6D3 or White #FFFFFF

### Step 5: Construct Comprehensive Prompt

```
Hand-drawn Mermaid [DIAGRAM TYPE] in Excalidraw whiteboard sketch style.

STYLE: Excalidraw hand-drawn (wobbly, sketchy, organic)
BACKGROUND: Light Cream #F5E6D3

AESTHETIC:
- Wobbly rectangles, sketchy arrows, hand-lettered text
- Rough edges on all shapes, variable line weight
- NO digital precision, NO perfect geometry, NO smooth vectors

DIAGRAM TYPE: [Flowchart / Sequence / State / etc.]

TYPOGRAPHY (3-TIER):
TIER 1 - TITLE: "[Title]" Valkyrie serif italic, large, top-left
SUBTITLE: "[Subtitle]" Valkyrie serif regular, smaller, below title

TIER 2 - NODE LABELS:
- Technical identifiers: Concourse T3 geometric sans, medium, charcoal
- Process descriptions: Valkyrie serif, warm, readable

TIER 3 - EDGE LABELS & INSIGHTS:
- Arrow conditions: Advocate condensed or Valkyrie, 60% of Tier 2
- Commentary: Advocate condensed italic, Purple or Teal
- Examples: "*this is where it breaks*", "*performance bottleneck*"

DIAGRAM COMPONENTS:
[List each node with shape, label, style, color, position]
[List each arrow/connection with path, label, color]

COLOR USAGE:
- Black (#000000): All primary structure
- Purple (#4A148C): Critical path (10-20% of nodes)
- Teal (#00796B): Alternative paths (5-10%)
- Charcoal (#2D2D2D): All text

CRITICAL: Excalidraw hand-drawn, Mermaid structure, UL color scheme.
All shapes imperfect, all lines wobbly. Readable despite sketch style.
```

### Step 6: Determine Aspect Ratio

| Diagram Type | Default Aspect Ratio |
|--------------|---------------------|
| Flowchart (vertical) | 9:16 or 4:3 |
| Flowchart (horizontal) | 16:9 |
| Sequence diagram | 16:9 |
| State diagram | 1:1 |
| Class/ER diagram | 16:9 or 1:1 |
| Gantt chart | 16:9 or 21:9 |

Default: 16:9

### Step 7: Generate

```bash
bun run ~/dev/cg-claude-workspaces-plugins/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[YOUR PROMPT]" \
  --size 2K \
  --aspect-ratio [chosen ratio] \
  --output ~/Downloads/[descriptive-name].png
```

Then immediately open:
```bash
open ~/Downloads/[descriptive-name].png
```

### Step 8: Comprehensive Validation

**Diagram Correctness:**
- [ ] Structure follows [type] conventions
- [ ] Logic clear -- flow/sequence/states make sense
- [ ] All elements from CSE represented
- [ ] Connections point to right places
- [ ] Labels accurate

**Excalidraw Aesthetic:**
- [ ] Hand-drawn feel -- looks sketched on whiteboard
- [ ] Wobbly shapes -- no perfect rectangles/circles
- [ ] Sketchy arrows -- organic curves, not ruler-straight
- [ ] Variable line weight

**UL Editorial Style:**
- [ ] Color strategic -- purple critical (10-20%), teal secondary (5-10%)
- [ ] Black dominant for most structure
- [ ] Typography 3-tier hierarchy clear
- [ ] No gradients -- flat colors

**Readability:**
- [ ] Labels readable despite hand-drawn style
- [ ] Flow obvious -- can follow the diagram easily
- [ ] Critical path clear (purple highlights)
- [ ] Not cluttered -- adequate spacing

**If validation fails:**

| Problem | Fix |
|---------|-----|
| Too polished/digital | "Wobbly rectangles, sketchy arrows, hand-drawn on whiteboard" |
| Perfect geometry | "All rectangles rough edges, circles slightly oval" |
| Can't follow flow | Strengthen arrows, add labels, clarify critical path with purple |
| Labels unreadable | Increase size: "Readable hand-lettered style" |
| Color overload | "Purple on 2-3 critical nodes only, teal on 1-2, rest black" |

## Model Selection

| User Says | Flag |
|---|---|
| "fast", "quick" | --model nano-banana |
| default / "best" | --model nano-banana-pro |
| "flux" | --model flux |

## Outputs

| File | Use For |
|------|---------|
| `[name].png` | Full resolution diagram |
| Add `--thumbnail` | If going into blog (transparent + sepia versions) |
| Add `--remove-bg` | For transparent background overlay |
