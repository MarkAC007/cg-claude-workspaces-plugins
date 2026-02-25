# /evals:create-judge -- Create a custom LLM-as-Judge for evaluating AI outputs

## ALL GENERATED FILES GO TO ~/Downloads/ FIRST

---

## Prerequisites

- Use case exists or is being created
- Clear evaluation criteria defined
- Understanding of what "good" looks like

---

## Process

### Step 1: Gather Requirements

Ask:
1. What are you evaluating? (content type, task)
2. What criteria matter? (accuracy, style, format, etc.)
3. What scale? (1-5 recommended; binary for pass/fail)
4. Should reasoning be required before scoring? (Yes — adds 13% accuracy)

### Step 2: Create judge-config.yaml

```yaml
judge:
  name: <Descriptive Name> Judge
  focus: accuracy  # or: style, completeness, custom
  scale:
    type: 1-5   # or "binary"
  criteria:
    - name: Factual Correctness
      description: All claims match source material
      weight: 0.5
    - name: Completeness
      description: Covers all key points from source
      weight: 0.3
    - name: No Hallucinations
      description: No invented or fabricated information
      weight: 0.2
  reasoning_required: true
  position_swap: false  # Set true for A/B comparisons

context:
  task_description: |
    <Describe the original task the output was meant to complete>
  golden_output: |
    <Optional: reference "perfect" output for comparison>

output:
  format: json
```

### Step 3: Build the Judge Prompt

Expand the config into a full LLM judge prompt:

```markdown
## Judge Task

You are evaluating AI-generated outputs for a task: [task_description]

## Evaluation Criteria

Score each criterion on a 1-5 scale (1=very poor, 5=excellent).

**[Criterion 1]** (weight: X%)
[Description of what this measures and what high/low scores look like]

**[Criterion 2]** (weight: Y%)
[Description]

## Instructions

1. Read the output carefully
2. Reason through each criterion BEFORE assigning scores
3. Assign a score 1-5 for each criterion
4. Calculate the weighted score

## Output Format (JSON)

{
  "reasoning": "[Your analysis before scoring]",
  "scores": {
    "[criterion_1]": N,
    "[criterion_2]": N
  },
  "weighted_score": N,
  "pass": true/false
}
```

### Step 4: Integrate with Use Case

Update `config.yaml`:

```yaml
criteria:
  ai_based:
    - scorer: "custom_judge"
      weight: 0.40
      params:
        judge_prompt: "[the judge prompt above]"
        judge_model: "claude-sonnet-4-6"
```

### Step 5: Test

Run against a single test case manually — paste the judge prompt + a sample output into a conversation and verify:
- Does the judge produce valid JSON?
- Is the reasoning coherent?
- Are scores in the expected range?

---

## Best Practices

| Rule | Why |
|------|-----|
| 3-5 criteria max | More is hard to calibrate |
| reasoning_required: true | 13%+ accuracy improvement (research-backed) |
| 1-5 scale | Most reliable; avoid 0-100 (poor calibration) |
| position_swap: true for A/B tests | Eliminates LLM position bias |
| Use a different judge model than tested model | Prevents self-serving bias |

## Scale Reference

| Scale | When to Use |
|-------|-------------|
| 1-5 | Most reliable, nuanced |
| Binary | Simple pass/fail |
| 1-3 | When fine gradations aren't meaningful |
