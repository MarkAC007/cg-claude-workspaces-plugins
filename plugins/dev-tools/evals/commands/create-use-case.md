# /evals:create-use-case -- Create a new evaluation use case with test cases and scoring criteria

## ALL GENERATED FILES GO TO ~/Downloads/ FIRST

Save all generated config files to `~/Downloads/evals/<name>/` before moving to the project.

---

## Prerequisites

- Clear understanding of what you're evaluating
- Example inputs and expected outputs
- Quality criteria defined

---

## Process

### Step 1: Gather Requirements

Ask:
1. What is this use case evaluating? (prompt, model, task)
2. What does "good" output look like?
3. Which criteria matter? (accuracy, format, style, etc.)
4. Do you have example inputs and outputs?

### Step 2: Create Directory Structure

```
UseCases/<name>/
├── config.yaml
├── README.md
├── test-cases/
│   ├── 001-basic.yaml
│   └── 002-edge.yaml
├── golden-outputs/   (optional)
└── prompts/
    └── v1.0.0.md
```

### Step 3: Write config.yaml

```yaml
name: <use_case_name>
description: |
  <What this evaluates and why>

version: "1.0.0"

target:
  type: prompt  # or "model", "agent"
  path: prompts/v1.0.0.md

criteria:
  deterministic:
    - scorer: "string_match"
      weight: 0.20
      params:
        contains: ["expected phrase"]
    - scorer: "format_validator"
      weight: 0.10
      params:
        required_sections: ["summary"]

  ai_based:
    - scorer: "llm_rubric"
      weight: 0.35
      params:
        judge_model: "claude-sonnet-4-6"
        reasoning_first: true
        scale: "1-5"
    - scorer: "natural_language_assert"
      weight: 0.35
      params:
        assertion: "Output correctly addresses the user's question"

pass_threshold: 0.75

models:
  - claude-sonnet-4-6
  - claude-haiku-4-5-20251001
```

### Step 4: Write Initial Prompt (prompts/v1.0.0.md)

```markdown
# [Task Name] Prompt v1.0.0

## System Context
[System prompt or context]

## Task Instructions
[Specific instructions]

## Output Format
[Expected format specification]

## Examples (Optional)
[Few-shot examples]
```

### Step 5: Create Test Cases

**Target distribution:** 2-3 easy, 3-4 medium, 2-3 hard.

Each test case YAML:

```yaml
id: "001-basic"
name: "Basic functionality test"
description: "Tests standard use case"
priority: high

input:
  content: |
    <The input content to test>

expected:
  format: "structured"
  contains:
    - "expected phrase"
  length:
    min_words: 50
    max_words: 200

golden_output: "../golden-outputs/001-basic.md"  # optional
```

### Step 6: Write README.md

Document the use case: purpose, criteria weights, test case table, version history.

### Step 7: Validate

Check all files are well-formed YAML and the config passes a mental dry-run: would the scorers produce valid output on the test cases?

---

## Grader Types Reference

### Code-Based (Fast, Deterministic)

| Grader | Use Case |
|--------|----------|
| `string_match` | Exact substring matching |
| `regex_match` | Pattern matching |
| `binary_tests` | Run test files |
| `static_analysis` | Lint / type-check |
| `state_check` | Verify system state after execution |
| `tool_calls` | Verify specific tools were called |

### Model-Based (Nuanced)

| Grader | Use Case |
|--------|----------|
| `llm_rubric` | Score against detailed rubric |
| `natural_language_assert` | Check assertions are true |
| `pairwise_comparison` | Compare to reference (use position swap) |

### Criteria Weights

| Pattern | Deterministic | AI-Based |
|---------|---------------|----------|
| Format-critical | 60-70% | 30-40% |
| Quality-critical | 30-40% | 60-70% |
| Balanced | 50% | 50% |
