# /evals:compare-models -- Compare multiple models on the same prompt to find the best performer

## Prerequisites

- Existing use case with test cases and a prompt
- Clear comparison criteria
- Access to the models being compared

---

## Process

### Step 1: Define the Comparison

Ask:
1. Which use case?
2. Which models? (Claude, GPT-4, Gemini, etc.)
3. Primary evaluation criterion?
4. Any cost/latency constraints?

### Step 2: Create Model Comparison Config

```yaml
model_comparison:
  name: "Claude vs GPT-4o vs Gemini"
  hypothesis: |
    Testing which model produces the best outputs for this use case.

  prompt: "prompts/v1.0.0.md"

  models:
    - id: "claude-sonnet-4-6"
      name: "Claude Sonnet 4.6"
      provider: "anthropic"
    - id: "gpt-4o"
      name: "GPT-4o"
      provider: "openai"
    - id: "gemini-1.5-pro"
      name: "Gemini 1.5 Pro"
      provider: "google"

  settings:
    runs_per_model: 1
    temperature: 0.7

  track_costs: true
  track_latency: true
```

### Step 3: Run Evaluations

For each model, run all test cases through the prompt and apply your scoring criteria. Track:
- Pass rate (% tests above threshold)
- Mean score across all tests
- Latency (approximate)
- Relative cost

### Step 4: Analyse Results

**Multi-Model Summary:**

| Model | Pass Rate | Mean Score | Cost | Latency |
|-------|-----------|------------|------|---------|
| Claude Sonnet 4.6 | X% | X.X | $$ | Xs |
| GPT-4o | X% | X.X | $$$ | Xs |
| Gemini 1.5 Pro | X% | X.X | $$ | Xs |

**Per-Dimension Breakdown:**

| Model | Accuracy | Style | Format |
|-------|----------|-------|--------|
| ... | | | |

### Step 5: Make Recommendation

Use this decision framework:

| Factor | Weight | Best Model |
|--------|--------|------------|
| Quality | 50% | [Best performer] |
| Cost | 25% | [Cheapest acceptable] |
| Latency | 25% | [Fastest acceptable] |

**Decision Matrix:**
- **Primary use**: Best overall quality model
- **Budget option**: Best quality-per-dollar model
- **High-volume**: Cheapest with acceptable quality

### Step 6: Document Decision

Record in use case README:
```markdown
## Model Comparison: [Date]
**Purpose:** [Why this comparison was run]
**Winner:** [Model] — [reason]
**Runner-up:** [Model] — [use case]
**Deprecated:** [Model] — [why not chosen]
```

---

## Best Practices

| Rule | Why |
|------|-----|
| Same prompt for all models | Fair comparison |
| Same temperature (0.7) | Comparable variance |
| Use a different judge model | Prevents self-serving bias — use GPT-4 to judge Claude outputs |
| Multiple runs per model | Accounts for variance |
| Track cost + latency | Quality alone doesn't make a decision |

## Model Selection Guide

| Use Case | Recommended | Why |
|----------|-------------|-----|
| Quality-critical, flexible budget | Best-scoring model | Quality justified |
| High-volume, cost-sensitive | Best quality-per-dollar | Economics matter |
| Latency-critical | Fastest with acceptable quality | UX matters |
| Structured output | Check format adherence specifically | Models vary on JSON/YAML |
