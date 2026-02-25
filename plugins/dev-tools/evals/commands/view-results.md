# /evals:view-results -- Query and display evaluation results and trends

## Prerequisites

- Evaluations have been run (results stored as JSON files in `Results/`)

---

## Process

### Step 1: Identify the Query

Ask:
1. Which use case?
2. What time range? (latest, last week, specific run)
3. What to show? (summary, details, comparison, trends)
4. Any filters? (failures only, specific model, specific test)

### Step 2: Locate Results

Results are stored in `Results/<use-case>/<run-id>/`:
- `results.json` — full per-test-case breakdown
- `summary.yaml` — aggregated metrics

List available runs:
```bash
ls Results/<use-case>/
```

### Step 3: Parse and Display Results

Read the most recent `results.json` and present:

```markdown
📋 SUMMARY: Evaluation results for <use-case>

📊 STATUS:
| Metric | Value |
|--------|-------|
| Run ID | <run-id> |
| Date | <date> |
| Model | <model> |
| Pass Rate | X% |
| Mean Score | X.XX |
| Total Tests | N |
| Passed | N |
| Failed | N |

### Per-Test Results

| Test ID | Score | Passed | Failing Criteria |
|---------|-------|--------|-----------------|
| 001-basic | 0.85 | ✓ | — |
| 002-edge | 0.58 | ✗ | llm_rubric |

### Key Findings
1. [What went well]
2. [What failed and why]
3. [Recommendation]
```

### Step 4: Trend Analysis (Multi-Run)

If multiple runs exist, show score trends:

```
📈 Trend: <use-case> (last N runs)

Date       | Pass Rate | Mean Score | Change
-----------|-----------|------------|--------
2026-02-25 | 92%       | 4.3        | +5%
2026-02-20 | 87%       | 4.1        | -2%
2026-02-15 | 89%       | 4.2        | baseline

Trend: ↑ Improving
```

### Step 5: Failure Analysis

For failed test cases, dig into the specifics:
- Which scorer failed?
- What was the actual vs. expected?
- Is this a systematic failure (multiple cases) or an outlier?

---

## Result Interpretation Guide

| Pass Rate | Signal | Action |
|-----------|--------|--------|
| 95%+ | Ready for regression | Graduate to regression suite |
| 80-95% | Good — minor issues | Fix failing cases, re-run |
| 60-80% | Issues present | Investigate systematically |
| <60% | Significant problems | Revisit prompt or criteria |

---

## Common Queries

| Question | What to Look At |
|----------|----------------|
| "How did the last eval go?" | Latest run summary |
| "Why did test X fail?" | Per-test detail for that ID |
| "Is performance improving?" | Trend across runs |
| "Which model is best?" | Cross-model comparison |
| "Show me all failures this week" | Filter `passed: false` in results |
