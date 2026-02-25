# /art:remove-bg -- Remove Image Background

## Purpose

Remove backgrounds from existing images to create transparent PNGs. Supports two methods: re-generation with the --remove-bg flag (for freshly generated images) and the remove.bg API (for existing photos or images).

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running the Remove Background workflow", "voice_id": "25"}' \
  > /dev/null 2>&1 &
```

## Output to Downloads First

ALL GENERATED IMAGES GO TO ~/Downloads/ FIRST -- NEVER directly to project directories.

## When to Use

- "Remove the background from this image"
- "Make this image transparent"
- "I need a transparent PNG of this"
- Converting diagrams to transparent backgrounds
- Preparing images for web display or overlay
- Creating icons with transparent backgrounds
- Cleaning up screenshots for composition
- Preparing headshots for thumbnail composition

---

## Workflow Steps (ALL MANDATORY)

### Step 1: Verify Input File

Confirm the source image exists and note its current format and size.

```bash
ls -lh [INPUT_PATH]
magick identify [INPUT_PATH]
```

If the file does not exist, ask the user for the correct path before proceeding.

### Step 2: Choose Method

**Method A -- Generate.ts --remove-bg** (for AI-generated images or re-generation)
Use when you are generating a new image and want transparency from the start, or when you can re-generate the image with the same prompt.

**Method B -- remove.bg API** (for existing photos, screenshots, or any image)
Use when you have an existing file that cannot be re-generated (photos, screenshots, downloaded images).

### Step 3A: Generate with Background Removal

Re-generate the image with the --remove-bg flag. This produces a transparent PNG directly.

```bash
bun run ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[ORIGINAL PROMPT OR DESCRIPTION OF DESIRED IMAGE]" \
  --size 2K \
  --aspect-ratio 1:1 \
  --remove-bg \
  --output ~/Downloads/[name]-transparent.png
```

### Step 3B: Remove Background via API

Use the remove.bg API to strip the background from an existing image.

**Prerequisite:** REMOVEBG_API_KEY must be set in ~/.claude/.env

```bash
# Load API key
source ~/.claude/.env

# Remove background
curl -X POST https://api.remove.bg/v1.0/removebg \
  -H "X-Api-Key: ${REMOVEBG_API_KEY}" \
  -F "image_file=@[INPUT_PATH]" \
  -F "size=auto" \
  -o ~/Downloads/[name]-transparent.png
```

**API size options:**
- `size=auto` -- Automatic size detection (recommended)
- `size=preview` -- Smaller preview (0.25 megapixels)
- `size=full` -- Full resolution (up to 25 megapixels)

**Rate limit:** Free tier allows 50 API calls per month. Check usage at https://www.remove.bg/dashboard

### Step 4: Verify Transparency

Confirm the output has actual transparency (not just a white or checkerboard background).

```bash
# Check file exists and size differs from input
ls -lh ~/Downloads/[name]-transparent.png

# Verify alpha channel exists
magick identify -verbose ~/Downloads/[name]-transparent.png | grep -A 5 "Alpha"

# Open for visual inspection
open ~/Downloads/[name]-transparent.png
```

### Step 5: Preview Result

Open the transparent PNG. In Preview/Finder, transparency appears as a checkerboard pattern behind the subject.

```bash
open ~/Downloads/[name]-transparent.png
```

If the result is unsatisfactory:
- Subject edges are rough: try `size=full` for higher resolution processing
- Wrong areas removed: the API works best with clear subject/background separation
- No transparency detected: check the API response for errors

---

## Batch Processing

To remove backgrounds from multiple images at once:

```bash
source ~/.claude/.env

for img in ~/Downloads/batch-*.png; do
  filename=$(basename "$img" .png)
  curl -X POST https://api.remove.bg/v1.0/removebg \
    -H "X-Api-Key: ${REMOVEBG_API_KEY}" \
    -F "image_file=@$img" \
    -F "size=auto" \
    -o ~/Downloads/${filename}-transparent.png
done
```

Note: Each image counts as one API call against the monthly limit.

---

## Tool Invocation

**Method A (Generate.ts):**
```bash
bun run ~/dev/cg-claude-workspaces-plugins/plugins/marketing/art/tools/Generate.ts \
  --model nano-banana-pro \
  --prompt "[PROMPT]" \
  --size [1K|2K|4K] \
  --aspect-ratio [1:1|16:9|etc] \
  --remove-bg \
  --output ~/Downloads/[name]-transparent.png
```

**Method B (remove.bg API):**
```bash
source ~/.claude/.env
curl -X POST https://api.remove.bg/v1.0/removebg \
  -H "X-Api-Key: ${REMOVEBG_API_KEY}" \
  -F "image_file=@[INPUT_PATH]" \
  -F "size=auto" \
  -o ~/Downloads/[name]-transparent.png
```

---

## Validation Checklist

- [ ] Input file exists and is a valid image
- [ ] REMOVEBG_API_KEY is set (if using API method)
- [ ] Output file created in ~/Downloads/
- [ ] Output file has alpha channel (actual transparency)
- [ ] Subject edges are clean (no halos or artifacts)
- [ ] Output opened for visual verification

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| "No onnxruntime backend found" | Do NOT use local rembg. Use the remove.bg API via curl. |
| "API key invalid" | Verify REMOVEBG_API_KEY is set correctly in ~/.claude/.env |
| Output file same size as input | Background removal may have failed. Check API response for errors. |
| Rough edges on subject | Try `size=full` for higher resolution processing |
| Wrong areas removed | API works best with clear subject/background separation |

---

## Outputs

| File | Description |
|------|-------------|
| ~/Downloads/[name]-transparent.png | Image with background removed (transparent PNG) |
