# /art:taxonomy -- Classification Grids & Periodic Tables

## Purpose

Create hand-drawn classification systems -- periodic tables of X, organized categorization grids, capability matrices, and reference cards. Uses grid structure with hand-drawn imperfection, consistent 3-tier typography (Advocate titles, Concourse labels, italic annotations), and purple/teal category color coding.

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running the Taxonomy workflow", "voice_id": "25"}' \
  > /dev/null 2>&1 &
```

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Create a periodic table of X"
- "Classification grid for..."
- "Capability matrix"
- "Taxonomy of..."
- "Categorize these into a visual"
- "Reference card for..."
- Organized typologies, systematic categorizations
- Any structured grid-based classification system

## Workflow Steps (ALL 6 MANDATORY)

### Step 1: Define Classification System

Identify what you are classifying:

1. **What is being categorized?** (e.g., AI capabilities, security threats, business models)
2. **What are the organizing dimensions?** (e.g., complexity vs. impact, offensive vs. defensive)
3. **How many categories?** (e.g., 6 types, 12 elements, 4x4 grid)
4. **What is the hierarchy?** (major categories -> subcategories)

**Template:**
```
CLASSIFICATION SUBJECT: [What you're organizing]

ORGANIZING DIMENSIONS:
- Dimension 1: [e.g., Complexity: Simple --> Complex]
- Dimension 2: [e.g., Impact: Low --> High]

CATEGORIES:
1. [Category name] -- [Description]
2. [Category name] -- [Description]
3. [Category name] -- [Description]
...

ITEMS TO CLASSIFY:
- [Item 1] belongs to [Category]
- [Item 2] belongs to [Category]
...
```

### Step 2: Design Grid Layout

**Layout types:**
- Periodic table grid (rows and columns)
- Matrix (2x2, 3x3, 4x4)
- Hierarchical tree
- Grouped clusters
- Linear taxonomy (top to bottom)

**Cell structure:**
- What information in each cell (icon/symbol + label)
- Size of cells (uniform or varied)
- How categories are grouped visually

**Color assignment:**
- Purple #4A148C: Category 1 headers/highlights (10%)
- Teal #00796B: Category 2 headers/highlights (10%)
- Black #000000: All grid lines, cell borders (80%)
- Charcoal #2D2D2D: All body text and labels
- Background: White #FFFFFF or Light Cream #F5E6D3

### Step 3: Construct Prompt

```
Hand-drawn taxonomy grid in editorial notebook style.

STYLE: Periodic table, field guide illustration, reference card aesthetic
BACKGROUND: [White #FFFFFF or Light Cream #F5E6D3]

AESTHETIC:
- Hand-drawn imperfect grid lines (slightly wobbly, human quality)
- Variable stroke weight (grid structure in black)
- Cell borders with slight waviness (not perfect rectangles)
- Editorial flat color with strategic accents
- Organized layout but hand-crafted feel

LAYOUT TYPE: [Periodic table / Matrix / Hierarchical tree / etc.]

GRID STRUCTURE:
- [Rows] by [Columns] of cells
- Each cell contains: [category icon/symbol] + [label text]
- Cells grouped by color into [categories]
- Clear visual separation between category groups

TYPOGRAPHY (3-TIER):

TIER 1 - HEADER & SUBTITLE (Valkyrie Two-Part System):
Header: "[Title]"
  Font: Valkyrie serif italic, large (3-4x body), left-justified, top-left
  Color: Black #000000 or Purple #4A148C
Subtitle: "[Subtitle]"
  Font: Valkyrie serif regular (NOT italic), smaller (1-1.5x body)
  Color: Charcoal #2D2D2D, below header, left-aligned

TIER 2 - CATEGORY HEADERS (Concourse Sans):
  "[Category 1]", "[Category 2]", etc.
  Font: Concourse geometric sans, clean, modern, medium
  Color: Purple #4A148C for Category 1, Teal #00796B for Category 2

TIER 3 - ITEM LABELS (Advocate Condensed):
  Individual items within cells
  Font: Advocate condensed, 60% of Tier 2
  Color: Charcoal #2D2D2D

CONTENT:
CATEGORY 1 (Purple #4A148C headers):
- Item A: [label]
- Item B: [label]
- Item C: [label]

CATEGORY 2 (Teal #00796B headers):
- Item D: [label]
- Item E: [label]
[Continue for all categories...]

COLOR USAGE:
- Black: All grid structure, cell borders
- Purple: [Category 1] headers and accents
- Teal: [Category 2] headers and accents
- Charcoal: All item labels and body text

CRITICAL:
- Hand-drawn sketch quality -- NOT polished digital grid
- Grid lines wobble slightly (human imperfection)
- Cells roughly aligned but organic
- No gradients, no shadows, flat colors only
- Clear 3-tier typography hierarchy
- Scannable and reference-friendly
- Strategic color coding for categories
```

### Step 4: Determine Aspect Ratio

| Taxonomy Type | Default Aspect Ratio |
|---------------|---------------------|
| Wide grid (many columns) | 16:9 or 21:9 |
| Tall hierarchy | 9:16 |
| Square matrix | 1:1 |
| Reference card | 1:1 or 4:3 |

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
- [ ] Clear grid structure -- organized layout with visible cells/categories
- [ ] Readable text -- all labels legible in 3-tier hierarchy
- [ ] Hand-drawn aesthetic -- wobbly lines, imperfect cells, human feel
- [ ] Strategic color -- purple/teal differentiate categories, not overwhelming
- [ ] Scannable -- easy to find and reference specific items
- [ ] Hierarchical clarity -- Title > Categories > Items is obvious
- [ ] Flat aesthetic -- no gradients

**Must NOT have:**
- [ ] Perfect straight grid lines
- [ ] Polished vector graphics
- [ ] Gradients or shadows
- [ ] Illegible or tiny text
- [ ] Color chaos (too many colors)
- [ ] Confusing organization

**If validation fails:**

| Problem | Fix |
|---------|-----|
| Grid too perfect | "Wobbly hand-drawn grid lines, organic imperfection" |
| Text unreadable | Increase text size, strengthen typography tiers |
| Too colorful | "Strategic color -- purple for [specific], teal for [specific], rest black" |
| Unclear organization | Simplify grid, reduce categories, clarify groupings |
| Looks digital | "Hand-drawn field guide, editorial notebook aesthetic" |

## Model Selection

| User Says | Flag |
|---|---|
| "fast", "quick" | --model nano-banana |
| default / "best" | --model nano-banana-pro |
| "flux" | --model flux |

## Examples

| Taxonomy | Layout | Purple Category | Teal Category |
|----------|--------|----------------|---------------|
| AI Capabilities | 5x6 periodic table | Reasoning | Creativity |
| Cybersecurity Threats | Hierarchical tree | Network threats | Application threats |
| Business Models | 3x3 matrix | High-scalability | Low-complexity |

## Color Distribution

```
80% Black structure (grid lines, borders)
10% Purple (Category 1 headers/accents)
10% Teal (Category 2 headers/accents)
All body text: Charcoal #2D2D2D
```

## Outputs

| File | Use For |
|------|---------|
| `[name].png` | Full resolution taxonomy |
| Add `--thumbnail` | If going into blog (transparent + sepia versions) |
