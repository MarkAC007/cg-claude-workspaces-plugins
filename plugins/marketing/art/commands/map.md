# /art:map -- Conceptual Maps of Idea Territories

## Purpose

Creates conceptual maps -- illustrated landscape metaphors for domains and idea territories. These are NOT geographic maps. They are hand-drawn cartographic illustrations where islands, continents, rivers, and mountains represent concepts and their relationships. Purple (#4A148C) for key domains, teal (#00796B) for secondary. Hand-drawn imperfect coastlines. Editorial aesthetic.

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Map the landscape of..."
- "Create a conceptual map of..."
- "Show the territory of..."
- "Visualize how these domains relate"
- "The Landscape of AI Safety" style visualizations
- Domain overviews showing relationships
- Orientation guides for complex topics
- Conceptual geography of a field

## Workflow Steps (ALL MANDATORY)

### Step 1: Define Conceptual Geography

Identify the territories and their relationships.

1. **What domain are you mapping?** The subject area (e.g., AI capabilities, security landscape).
2. **List 4-8 major territories** -- each territory is a concept or domain.
3. **Map spatial relationships:**
   - Close territories = related concepts
   - Ocean between = very different domains
   - Mountains = barriers or challenges
   - Rivers = connections or flows
   - Bridges = integration points
   - Peninsulas = partially connected concepts
   - Islands = isolated domains

Output:
```
MAP SUBJECT: "The [Domain] Landscape"

TERRITORIES:
1. [Territory name] -- [What it represents]
2. [Territory name] -- [What it represents]
3. [Territory name] -- [What it represents]
4. [Territory name] -- [What it represents]
...

SPATIAL RELATIONSHIPS:
- [Territory A] and [Territory B]: Adjacent (related)
- [Territory C]: Island (isolated domain)
- Ocean between [X] and [Y]: Very different
- Mountain range along [Z]: Barrier/challenge
- River connecting [A] to [B]: Data or information flow

KEY TERRITORY (Purple): [Which territory is primary]
SECONDARY TERRITORY (Teal): [Which is secondary]
```

### Step 2: Design Map Layout

Plan the cartography:

1. **Map orientation:** North-up traditional, centered around key territory, horizontal spread.
2. **Territory shapes:** Continents (large connected domains), islands (isolated concepts), archipelagos (related clusters), peninsulas (partially connected).
3. **Features:** Coastlines/borders, mountains, rivers, bridges, compass rose, legend.
4. **Labels:** Map title (Tier 1), territory names (Tier 2), feature labels (Tier 3).

### Step 3: Construct Prompt

Build the generation prompt:

```
Hand-drawn conceptual map in editorial cartography style.

STYLE: Fantasy map, hand-drawn cartography, illustrated territory map. Wobbly coastlines, imperfect borders. Variable stroke weight. Editorial flat color with strategic purple/teal territories. Sketch quality, not polished digital map.

BACKGROUND: Light Cream #F5E6D3 -- represents ocean/empty space.

MAP SUBJECT: "[The X Landscape]"

TYPOGRAPHY SYSTEM (3-TIER):
TIER 1 - MAP TITLE (Valkyrie Serif Italic):
"[Title]" -- large at top-left, elegant, sophisticated. 3-4x body text.

TIER 2 - TERRITORY NAMES (Concourse Sans):
"[Domain 1]", "[Domain 2]", etc. -- medium readable, inside territory borders. Charcoal #2D2D2D.

TIER 3 - FEATURE LABELS (Advocate Condensed Italic):
"mountains of complexity", "river of data" -- 60% of Tier 2 size, near relevant features.

TERRITORIES:
CENTRAL: [Primary Domain] -- Large irregular continent. Hand-drawn wobbly coastline. Subtle purple (#4A148C) tint fill. Label inside.
EASTERN: [Secondary Domain] -- Medium island. Subtle teal (#00796B) tint fill.
WESTERN: [Domain] -- Peninsula connected to center. Light cream fill.
[Continue for all territories...]

GEOGRAPHIC FEATURES:
- Mountain range along [border]: Hand-drawn peaks, black linework. Represents [barrier].
- Rivers: Wobbly flowing lines connecting territories. Represents [connections].
- Bridges: Small illustrated bridges. Represents [integration points].
- Compass rose: Small decorative compass in corner, purple north arrow.

COLOR: Black (#000000) for all coastlines, borders, features. Purple (#4A148C) subtle fill on primary territory. Teal (#00796B) subtle fill on secondary. Charcoal (#2D2D2D) for all text. No gradients, flat colors only.
```

### Step 4: Determine Aspect Ratio

| Map Type | Aspect Ratio | Notes |
|----------|-------------|-------|
| Wide horizontal | 16:9 or 21:9 | Spread-out territories |
| Balanced | 1:1 | Symmetric distribution |
| Classic poster | 4:3 | Traditional map proportions |

**Default: 16:9 (horizontal)** -- classic map orientation.

### Step 5: Generate

```bash
bun run ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[YOUR CONSTRUCTED PROMPT]" \
  --size 2K \
  --aspect-ratio 16:9 \
  --output ~/Downloads/conceptual-map.png
```

Immediately open for review:
```bash
open ~/Downloads/conceptual-map.png
```

### Step 6: Validate

**Must Have:**
- [ ] Map structure clear -- territories, coastlines, borders obvious
- [ ] Conceptual geography -- physical features represent ideas
- [ ] Readable labels -- territory names and feature labels legible
- [ ] Hand-drawn -- wobbly coastlines, imperfect borders, human quality
- [ ] Strategic color -- purple/teal on key territories (subtle fills)
- [ ] Navigable -- helps understand relationships between concepts
- [ ] Editorial aesthetic -- flat color, black linework

**Must NOT Have:**
- [ ] Perfect digital map (too clean)
- [ ] Realistic geographic features
- [ ] Illegible territory names
- [ ] Color chaos (too many territory colors)
- [ ] Gradients or shadows

**Fix Table:**

| Problem | Fix |
|---------|-----|
| Too precise/digital | "Hand-drawn wobbly coastlines, imperfect borders, sketch quality" |
| Unclear metaphors | Strengthen "mountains represent [specific barrier]" |
| Labels unreadable | Increase label sizes, clearer placement inside territories |
| Too complex | Reduce to 4-6 major territories, simplify features |
| Looks like real map | "Conceptual geography, metaphorical territories, abstract cartography" |

## Outputs

- `~/Downloads/conceptual-map.png` -- the generated conceptual map image
- Move to project directory only after validation passes
