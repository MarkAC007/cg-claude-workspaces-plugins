# /art:thumbnail-checklist -- YouTube Thumbnail Validation

## Purpose

Two-phase validation system for YouTube thumbnails: PRE-generation checklist (before creating assets) and POST-generation checklist (after composition). Run this to validate thumbnails before and after generating them.

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running the Thumbnail Checklist workflow", "voice_id": "25"}' \
  > /dev/null 2>&1 &
```

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Validate this thumbnail"
- "Check my thumbnail before I upload"
- "Run the thumbnail checklist"
- Before generating a thumbnail (pre-generation)
- After generating a thumbnail (post-generation)
- When a thumbnail looks wrong and needs diagnosis

---

## Workflow Steps (ALL MANDATORY)

### PHASE 1: PRE-GENERATION CHECKLIST

Complete this BEFORE running any generation commands. If ANY item fails, STOP and fix it.

#### 1A: Reference Analysis

```
[ ] Reviewed thumbnail specifications (1280x720, 16px border, face-only headshot)
[ ] Identified which style/mood matches this use case
[ ] Noted target colors (title: cyan #7dcfff default, border: #bb9af7)
[ ] Confirmed text sizing (100pt title, 50pt subtitle)
[ ] Confirmed border thickness (16px) and color (#bb9af7)
```

#### 1B: Content Preparation

```
[ ] Extracted title text from content (3-7 words max)
[ ] Extracted subtitle text (up to 12 words)
[ ] Identified content mood/tone for headshot expression
[ ] Selected headshot reference image OR planned new generation
[ ] Determined headshot position (left/center/right)
[ ] Planned background style (dark tech, specific topic context)
```

#### 1C: Font Verification

```bash
# Verify fonts are available
magick -list font | grep -i helvetica
```

```
[ ] Confirmed exact font name available in ImageMagick
[ ] Confirmed Bold weight is available
[ ] If fonts missing: installed required fonts first
```

#### 1D: Specification Confirmation

```
[ ] Canvas size: 1280x720 confirmed
[ ] Border: 16px #bb9af7 confirmed
[ ] Title: 100pt bold, 4px stroke, CYAN (#7dcfff) default
[ ] Subtitle: 50pt bold, 3px stroke, white (#FFFFFF)
[ ] Headshot: FACE ONLY (forehead to chin), transparent background
[ ] Background: Dark futuristic tech, NO faces, NO text
[ ] Layer order: background -> headshot -> text -> border
[ ] Output path: ~/Downloads/
```

#### 1E: Asset Generation Plan

**Background:**
```
[ ] Prompt includes dark tech aesthetic keywords
[ ] Prompt explicitly states "NO FACES, NO TEXT"
[ ] Prompt includes topic context for relevance
[ ] Generation model: nano-banana (NOT nano-banana-pro for backgrounds)
```

**Headshot:**
```
[ ] Prompt specifies FACE ONLY (forehead to chin, ear to ear)
[ ] Prompt includes NO shoulders, NO neck, NO body
[ ] Reference image identified for likeness
[ ] Expression/mood specified for this specific thumbnail
[ ] Variation selected (angle + expression + lighting differ from previous)
[ ] Model: nano-banana-pro with --remove-bg flag
```

#### 1F: Command Validation

```
[ ] All file paths confirmed to exist
[ ] All hex colors confirmed from specification
[ ] Output path is ~/Downloads/
[ ] Output filename includes timestamp
```

---

### PHASE 2: POST-GENERATION CHECKLIST

Complete this AFTER generating the thumbnail. If ANY item fails, regenerate with corrections.

#### 2A: File Validation

```bash
# Check file exists and dimensions
magick identify -format "%wx%h" ~/Downloads/yt-thumbnail-[TIMESTAMP].png
# Expected: 1280x720

ls -lh ~/Downloads/yt-thumbnail-[TIMESTAMP].png
```

```
[ ] File exists at specified path
[ ] File size is reasonable (not 0 bytes or corrupted)
[ ] File opens in Preview/Finder
[ ] Resolution is EXACTLY 1280x720 pixels
[ ] File format is PNG
```

#### 2B: Border and Canvas Validation

```
[ ] Border color is #bb9af7 (Tokyo Night purple)
[ ] Border thickness is 16px on all four sides
[ ] Border is consistent (no gaps, no artifacts)
[ ] Background fills entire canvas behind border
```

#### 2C: Headshot Validation

```
[ ] Headshot is present
[ ] Headshot is FACE ONLY (NO shoulders, NO neck, NO body)
[ ] Face fills 90%+ of headshot area
[ ] Background removed cleanly (transparent, no artifacts)
[ ] Expression matches intended mood
[ ] Headshot position matches specification (left/center/right)
[ ] Headshot is DIFFERENT from previous thumbnails (varied expression, angle, lighting)
```

#### 2D: Typography Validation

```
[ ] Title text is present and readable
[ ] Title color is CYAN (#7dcfff) or specified vibrant color (NOT plain white)
[ ] Title has visible stroke outline (4px)
[ ] Subtitle text is present and readable
[ ] Subtitle color is white (#FFFFFF)
[ ] Subtitle has visible stroke outline (3px)
[ ] Text FILLS the available space (billboard-style, not small)
[ ] Text does NOT overlap headshot
[ ] Text is grouped as a unit (title + subtitle together)
```

#### 2E: Background Art Validation

```
[ ] Background is present (dark futuristic tech aesthetic)
[ ] Background uses dark color palette (no light backgrounds)
[ ] NO faces in the background
[ ] NO text in the background
[ ] Background does not compete with headshot or title text
[ ] Background blends naturally with overall composition
```

#### 2F: Composition Validation

```
[ ] Text block and headshot occupy separate zones (no overlap)
[ ] Visual hierarchy is clear (face + title draw eye first)
[ ] Balance between text/headshot/background is professional
[ ] Overall impression is billboard-quality (not document-quality)
```

#### 2G: Small-Size Readability (MANDATORY)

```bash
# Create YouTube grid preview size
magick ~/Downloads/yt-thumbnail-[TIMESTAMP].png -resize 320x180 /tmp/yt-preview.png
open /tmp/yt-preview.png
```

```
[ ] Title text READABLE at 320x180
[ ] Headshot face RECOGNIZABLE at 320x180
[ ] Colors have sufficient contrast at small size
[ ] Overall composition is clear at small size
[ ] Would stand out in a YouTube sidebar/grid
```

#### 2H: Professional Quality

```
[ ] No pixelation or compression artifacts
[ ] Text is sharp and crisp
[ ] Headshot is high quality
[ ] Colors are vibrant but not oversaturated
[ ] Professional polish -- would be acceptable for public YouTube upload
[ ] No amateur mistakes (wrong fonts, bad spacing, overlapping elements)
```

---

## Validation Decision Tree

```
ALL POST-GENERATION CHECKS PASSED?
    YES -> Thumbnail is complete, present to user
    NO  -> Continue below

WHICH PHASE FAILED?
    Border/Canvas    -> Fix border color/thickness, regenerate
    Headshot         -> Regenerate headshot with stricter FACE-ONLY prompt
    Typography       -> Fix text color/size/position, recompose
    Background       -> Generate new background, recompose
    Composition      -> Adjust layout/position, recompose
    Readability      -> Increase contrast, simplify text, regenerate
    Quality          -> Identify specific defect, regenerate affected asset

AFTER FIX -> RERUN ENTIRE POST-GENERATION CHECKLIST
```

---

## Critical Failure Modes

These are the most common ways thumbnails fail. Check TWICE:

1. **Body visible in headshot** -- Regenerate with stricter FACE-ONLY prompt
2. **Text too small** -- Must use 100pt title / 50pt subtitle
3. **Title is plain white** -- Must be CYAN (#7dcfff) or another vibrant color
4. **Text not readable at 320x180** -- Increase size, stroke, contrast
5. **Text overlaps headshot** -- Check position flag (left/center/right)
6. **Same headshot as previous** -- Must vary angle, expression, and lighting
7. **Light background** -- Background must be dark tech aesthetic
8. **Faces in background** -- Background prompt must say NO FACES
9. **Wrong dimensions** -- Must be exactly 1280x720

---

## Outputs

This command produces no files directly. It validates existing thumbnail files:
- Input: ~/Downloads/yt-thumbnail-{timestamp}.png
- Preview: /tmp/yt-preview.png (320x180 test image)

NO THUMBNAIL IS COMPLETE UNTIL EVERY CHECKLIST ITEM PASSES.
