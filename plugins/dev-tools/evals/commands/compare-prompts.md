# /evals:compare-prompts -- A/B test two prompt versions to find the better performer

**Implements the Science Protocol for prompt experimentation.**

---

## Pre-Commitment (Do BEFORE running)

- [ ] Success criteria defined — what score/metric means "better"?
- [ ] Pass threshold locked — what difference is meaningful?
- [ ] Hypothesis is falsifiable — what result would **disprove** it?

> "If you cannot state what would disprove your hypothesis, you don't have a scientific hypothesis."

**Example:**
- Hypothesis: "v1.1.0 improves accuracy due to source verification instructions"
- Falsifiable if: "v1.1.0 accuracy ≤ v1.0.0 accuracy, or difference < 5%"

---

## Process

### Step 1: Define the Comparison

Ask:
1. Which use case?
2. Which prompt versions? (consider 3+ variants — reduces confirmation bias)
3. What's the hypothesis and why might one be better?
4. **What would DISPROVE this hypothesis?**
5. Which metrics matter most?
6. What threshold defines "significantly better"?

### Step 2: Verify Both Prompts Exist

Confirm `prompts/v1.0.0.md` and `prompts/v1.1.0.md` exist in the use case directory.

### Step 3: Create Comparison Config

```yaml
comparison:
  name: "v1.0.0 vs v1.1.0"
  hypothesis: |
    v1.1.0 produces more accurate summaries due to added source verification instructions.

  variants:
    a:
      name: "v1.0.0 (Baseline)"
      prompt: "prompts/v1.0.0.md"
    b:
      name: "v1.1.0 (Candidate)"
      prompt: "prompts/v1.1.0.md"

  test_cases: all
  settings:
    position_swap: true
    confidence_level: 0.95
    model: "claude-sonnet-4-6"
```

### Step 4: Run the Comparison

For each test case:
1. Run Variant A, capture output
2. Run Variant B, capture output
3. Apply judges to both outputs
4. Record scores

**Position Swapping Protocol** (when `position_swap: true`):
- Run 1: A = "Option 1", B = "Option 2"
- Run 2: B = "Option 1", A = "Option 2"
- Average scores — eliminates LLM position bias

### Step 5: Interpret Results

```markdown
## A/B Test Results: v1.0.0 vs v1.1.0

| Metric | v1.0.0 (A) | v1.1.0 (B) |
|--------|------------|------------|
| Win Rate | 42% | 58% |
| Avg Score | 4.2 | 4.5 |

### Statistical Significance
- p-value: 0.03
- Significant at 95%: Yes

### Per-Dimension Breakdown
| Dimension | A Wins | B Wins |
|-----------|--------|--------|
| Accuracy  | 3 | 7 |
| Style     | 5 | 4 |
```

### Step 6: Make the Decision

| Outcome | Action |
|---------|--------|
| B significantly better | Deploy B, archive A |
| A significantly better | Keep A, iterate on B |
| No significant difference | Keep simpler prompt |
| Mixed results | Consider hybrid or gather more data |

---

## Paradigm Check (When Iterations Stall)

If 3+ comparisons show no meaningful improvement:

| Signal | Question |
|--------|----------|
| All variants score similarly | Is the metric measuring what matters? |
| Scores are high but output feels wrong | Is there an unmeasured dimension? |
| Improvements don't compound | Is the base prompt fundamentally limited? |

**Consider:** redesigning the test cases or rethinking the entire prompt approach.

---

## Best Practices

| Rule | Why |
|------|-----|
| Pre-commit success criteria | Prevents post-hoc rationalisation |
| Position swap always on | LLMs have strong position bias |
| Use a different judge model | Prevents self-serving bias |
| Min 20-30 test cases | Statistical power (10 = weak, 50+ = ideal) |
| Test 3 variants not 2 | Reduces confirmation bias |
