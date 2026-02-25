# /evals:run-eval -- Execute an evaluation suite against test cases

## Prerequisites

- Use case config.yaml exists
- Test cases defined
- Scoring criteria configured

---

## Process

### Step 1: Validate Setup

Check the use case structure is complete:
```
UseCases/<name>/
├── config.yaml    ✓
├── test-cases/    ✓ (at least 1 file)
└── prompts/       ✓
```

If missing, run `/evals:create-use-case` first.

### Step 2: Load the Prompt

Read the target prompt from `prompts/v<version>.md`.

### Step 3: Execute Test Cases

For each test case YAML in `test-cases/`:

1. Extract the `input.content` field
2. Run the prompt with that input
3. Capture the full output

### Step 4: Apply Deterministic Scorers

For each deterministic criterion in config.yaml:

| Scorer | How to Check |
|--------|-------------|
| `string_match` | Does output contain the required substring? |
| `regex_match` | Does output match the regex pattern? |
| `format_validator` | Are required sections present? |
| `length_check` | Is output within min/max word bounds? |

Score: 1 (pass) or 0 (fail). Apply weight.

### Step 5: Apply AI-Based Scorers

For each `llm_rubric` or `natural_language_assert` criterion:
- Construct the judge prompt (see `/evals:create-judge`)
- Run it against the output
- Parse the JSON score
- Apply weight

### Step 6: Calculate Final Score

```
weighted_score = Σ (scorer_score × scorer_weight)
pass = weighted_score >= pass_threshold
```

### Step 7: Report Results

```markdown
📋 SUMMARY: Evaluation completed for <use-case>

📊 STATUS:
| Metric | Value |
|--------|-------|
| Total Tests | N |
| Passed | N |
| Failed | N |
| Pass Rate | X% |
| Mean Score | X.XX |

### Test Case Results

| Test ID | Score | Passed | Failing Criteria |
|---------|-------|--------|-----------------|
| 001-basic | 0.85 | ✓ | — |
| 002-edge | 0.62 | ✗ | format_validator |

### Findings

1. [Key finding about top performers]
2. [Key finding about failures]
3. [Recommendation]
```

---

## Interpreting Results

| Pass Rate | Action |
|-----------|--------|
| 95%+ | Graduate to regression suite |
| 75-95% | Normal iteration — investigate failures |
| 50-75% | Significant issues — rethink prompt |
| <50% | Fundamental problem — revisit use case design |

---

## Best Practices (from Anthropic)

1. **Start with 20-50 real failures** — don't overthink, capture what actually broke
2. **Unambiguous tasks** — two experts should reach identical verdicts
3. **Balanced problem sets** — test both "should do" AND "should NOT do"
4. **Grade outputs, not paths** — don't penalise valid creative solutions
5. **Check transcripts regularly** — verify graders work correctly
6. **Monitor saturation** — graduate to regression when hitting 95%+
