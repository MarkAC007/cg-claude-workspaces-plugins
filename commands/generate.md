# /art:generate -- Blog Headers & Editorial Illustrations

## Purpose

Generate charcoal architectural sketch illustrations for blog headers and editorial content. Uses gestural linework, hatching, and cross-hatching to depict content-relevant subjects -- NOT defaulting to buildings. Architecture is the TECHNIQUE, not the subject.

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running the Generate workflow", "voice_id": "25"}' \
  > /dev/null 2>&1 &
```

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Generate a blog header for this post"
- "Create an illustration for my essay"
- "Make a header image"
- Any blog post, essay, or editorial content needing a charcoal sketch header
- When you need the `--thumbnail` flag for transparent + sepia-background versions

## Workflow Steps (ALL 8 MANDATORY)

### Step 1: Deeply Understand the Request

Read and comprehend the full content before doing anything.

1. **What is the content?** Read the full blog post, essay, or input material
2. **What is it ABOUT?** The core concept/argument, not surface-level
3. **What are the key concrete elements?** Nouns, metaphors, imagery FROM the content
4. **What should NOT be drawn?** Architecture/buildings -- UNLESS the content is about those
5. **Did the user provide GUIDANCE?** User direction takes PRIORITY over your interpretation

Output: Clear understanding of the content's core subject matter + any user-provided guidance.

### Step 2: Run Create Story Explanation Level 24

Extract the FULL narrative arc to understand the emotional core.

```
/cse [paste the content or URL]
```

What CSE-24 gives you:
- Complete narrative arc: setup, tension, transformation, resolution
- Key metaphors and imagery
- The emotional journey
- What the piece is REALLY about

DO NOT PROCEED until you have run CSE and identified key metaphors and emotional beats.

### Step 3: Identify Emotional Register

Match the content to an emotional register:

| Register | When to Use |
|----------|-------------|
| DREAD / FEAR | AI takeover, existential risk, loss of control |
| HOPE / POSSIBILITY | Human potential, growth, positive futures |
| CONTEMPLATION | Philosophy, meaning, deep questions |
| URGENCY / WARNING | Security threats, calls to action |
| WONDER / DISCOVERY | Breakthroughs, encountering the vast |
| DETERMINATION / EFFORT | Overcoming obstacles, hard work |
| MELANCHOLY / LOSS | Endings, what's lost to progress |
| CONNECTION / KINDNESS | Human bonds, community |

Output: Selected emotional register with specific vocabulary.

### Step 4: Design Composition

Identify the PROBLEM the essay addresses (from CSE-24), then design what to draw.

**Problem Type Framework:**

| Problem Type | Visual Metaphor |
|--------------|-----------------|
| SORTING/CLASSIFICATION | Scattered items + empty labeled bins |
| COMMUNICATION | Tangled speech, broken telephone |
| DOUBLE STANDARD | Tilted scales, unfair judges |
| MISDIRECTION | Looking left while danger is right |
| OVERWHELM | Flood of items, buried figure |
| MISSING FRAMEWORK | Chaos vs. empty scaffolding |
| FALSE DICHOTOMY | Two doors, hidden third path |
| COMPLEXITY | Tangled vs. straight path |
| BLINDSPOT | Figure ignoring elephant |

Fill out this template:

```
THE PROBLEM: [What's WRONG that this essay addresses?]
SUBJECT: [What to draw that makes the PROBLEM visible]
VISUAL METAPHOR: [Core image representing the problem]
FIGURE TREATMENT: [If applicable -- who is judging, making mistakes, etc.]
EMOTIONAL REGISTER: [From Step 3]
COMPOSITION: [Arrangement making the PROBLEM OBVIOUS]
COLOR APPROACH: [Warm:Cool ratio, sienna:purple placement]
```

### Step 5: Construct the Prompt

Use the charcoal sketch TECHNIQUE template:

```
Sophisticated charcoal sketch using architectural rendering TECHNIQUE.

THE PROBLEM THIS ESSAY ADDRESSES:
[What's WRONG -- drives the entire composition]

SUBJECT (WHAT TO DRAW -- showing the problem):
[NOT defaulting to architecture -- draw what makes the problem clear]

EMOTIONAL REGISTER: [From Step 3]

TECHNIQUE -- GESTURAL ARCHITECTURAL SKETCH STYLE:
- GESTURAL -- quick, confident, energetic marks
- OVERLAPPING LINES -- multiple strokes suggesting form
- HATCHING -- cross-hatching creates depth and tone
- Loose charcoal/graphite pencil strokes throughout
- Variable line weight, some lines trailing off
- Like Paul Rudolph, Lebbeus Woods sketches

HUMAN FIGURES (if present) -- GESTURAL ABSTRACTED:
- MULTIPLE OVERLAPPING LINES suggesting the form
- 20-40 overlapping strokes creating the form
- FACES via simple charcoal marks
- Burnt Sienna (#8B4513) WASH accent on human elements

COMPOSITION -- FULL FRAME IS MANDATORY:
- SUBJECTS MUST FILL THE ENTIRE FRAME edge to edge
- NO large empty margins on any side
- MINIMALIST means few elements, NOT small elements

COLOR -- CHARCOAL DOMINANT:
- CHARCOAL AND GRAY DOMINANT -- 70-80% of image
- BURNT SIENNA (#8B4513) -- human warmth (MANDATORY)
- DEEP PURPLE (#4A148C) -- tech/capital/cold power (MANDATORY)
- Colors INTEGRATED INTO forms, not splattered on top
- Sienna on human/warm elements, Purple on tech/cold elements

NO borders, frames, background shading, gradients, or decorative elements.
Optional: Sign small in bottom right corner in charcoal.
NO other text.
```

**Prompt Quality Checklist (before generating):**
- [ ] PROBLEM IS VISIBLE -- someone could understand what's wrong from the image
- [ ] Concrete subjects present -- nouns from content appear visually
- [ ] Emotional register explicitly stated
- [ ] Burnt Sienna (#8B4513) AND Deep Purple (#4A148C) both specified
- [ ] "Charcoal sketch", "gestural", "hatching" explicitly stated
- [ ] SPECIFIC to this content -- couldn't be about something else

### Step 6: Execute the Generation

```bash
bun run ~/dev/cg-claude-workspaces-plugins/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[PROMPT FROM STEP 5]" \
  --size 2K \
  --aspect-ratio 1:1 \
  --thumbnail \
  --output ~/Downloads/[descriptive-name].png
```

The `--thumbnail` flag generates TWO versions:
- `output.png` -- Transparent background (for inline blog display)
- `output-thumb.png` -- With #EAE9DF sepia background (for social/OG thumbnails)

Then immediately open:
```bash
open ~/Downloads/[descriptive-name].png
```

### Step 7: Optimize Images

```bash
# Resize main image to 1024x1024 for web
magick "~/Downloads/[name].png" -resize 1024x1024 "~/Downloads/[name]-1024.png"

# Convert to WebP for inline blog display
cwebp -q 75 "~/Downloads/[name]-1024.png" -o "~/Downloads/[name].webp"

# Create optimized thumbnail for social media (512x512)
magick "~/Downloads/[name]-thumb.png" -resize 512x512 -quality 80 "~/Downloads/[name]-thumb-optimized.png"

# Clean up temp file
rm "~/Downloads/[name]-1024.png"

# Verify sizes
ls -lh ~/Downloads/[name].webp ~/Downloads/[name]-thumb-optimized.png
```

Expected: WebP ~150-500KB, thumbnail ~300-600KB.

### Step 8: Validate

Open and ACTUALLY LOOK at the image. Check these:

**Mandatory Checklist:**
- [ ] Subject matches CONTENT -- drew what the piece is ABOUT
- [ ] PROBLEM TYPE VISIBLE -- immediately obvious what kind of problem
- [ ] Concrete subjects visible -- key nouns/metaphors from content appear
- [ ] NOT defaulting to buildings/spaces (unless content is about architecture)
- [ ] BURNT SIENNA (#8B4513) present on human/warm elements
- [ ] DEEP PURPLE (#4A148C) present on tech/capital/cold elements
- [ ] Charcoal sketch quality -- visible strokes, hatching, gestural marks
- [ ] Gestural overlapping lines suggesting form (not clean vectors)
- [ ] FULL FRAME -- subjects nearly touch all edges, no large empty margins
- [ ] NO background fill -- floats in empty/transparent space
- [ ] Gallery-worthy sophistication
- [ ] Background removed (transparent)

**If validation fails:** Identify failed criteria, update prompt with specific fixes, regenerate, re-validate.

## Model Selection

| User Says | Flag |
|---|---|
| "fast", "quick", "draft" | --model nano-banana |
| default / "best" / "high quality" | --model nano-banana-pro |
| "flux", "stylistic variety" | --model flux |

## Size Selection

| User Says | Flag |
|---|---|
| "thumbnail", "small" | --size 1K |
| default / "standard" | --size 2K |
| "high res", "large", "print" | --size 4K |

## Aspect Ratio

| User Says | Flag |
|---|---|
| "square" (default) | --aspect-ratio 1:1 |
| "wide", "landscape", "banner" | --aspect-ratio 16:9 |
| "portrait", "vertical" | --aspect-ratio 9:16 |
| "ultrawide" | --aspect-ratio 21:9 |

## Emotional Quick-Select

| Content About... | Register | Warm:Cool |
|------------------|----------|-----------|
| AI danger | Dread | 20:80 |
| Human potential | Hope | 80:20 |
| Philosophy | Contemplation | 50:50 |
| Security threats | Urgency | 60:40 |
| Discoveries | Wonder | 40:60 |
| Building skills | Determination | 70:30 |
| What's lost | Melancholy | 40:60 |
| Community | Connection | 90:10 |

## Outputs

| File | Use For |
|------|---------|
| `[name].png` | Archive (original transparent, ~7.5MB) |
| `[name].webp` | Inline blog display (~400KB) |
| `[name]-thumb.png` | Archive (original sepia background) |
| `[name]-thumb-optimized.png` | Social media / thumbnail frontmatter (~500KB) |
