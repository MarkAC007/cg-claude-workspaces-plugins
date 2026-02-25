# /prompting:optimize -- Analyse and improve an existing prompt

Audit an existing prompt against Anthropic best practices and produce an improved version.

## Process

### Step 1: Receive the Prompt

Ask the user to paste the prompt they want to improve. Also ask:
1. What task is this prompt meant to accomplish?
2. What problem are you seeing? (low quality outputs, wrong format, inconsistency)
3. Do you have examples of good and bad outputs?

### Step 2: Audit the Prompt

Score each dimension 1-5 and note specific issues:

| Dimension | Score | Issues Found |
|-----------|-------|--------------|
| **Clarity** | ? | Is the task unambiguous? |
| **Structure** | ? | Is it organised with clear sections? |
| **Output spec** | ? | Is the format fully specified? |
| **Constraints** | ? | Are rules clear and positive? |
| **Examples** | ? | Are few-shot examples present when needed? |
| **Conciseness** | ? | Any padding or redundancy? |

### Step 3: Identify Root Causes

For each low score, identify the root cause:

- **Vague task**: No clear action verb or success criterion
- **Missing format**: Output format described loosely or not at all
- **Constraint overload**: Too many rules buried at the end
- **Over-engineering**: Unnecessary XML, excessive repetition
- **Missing context**: Model needs information it doesn't have

### Step 4: Rewrite

Apply fixes:

1. **Restructure** using Markdown headers (`## Task`, `## Output Format`, `## Constraints`)
2. **Specify output format** with a concrete schema or example
3. **Front-load** the most critical constraint
4. **Add few-shot examples** if the task requires precision or style matching
5. **Remove redundancy** — every sentence should earn its place

### Step 5: Diff the Changes

Present before/after with annotations:

```
BEFORE: "Please analyze the following text and provide insights"
AFTER:  "Analyse the text below. Return a JSON object with keys:
         summary (≤50 words), sentiment (positive|neutral|negative),
         key_claims (array of strings)"
WHY: Added output format spec — the original left format entirely to the model
```

### Step 6: Deliver

Output:
1. **Audit table** with scores and issues
2. **Optimised prompt** in a code block
3. **Summary of changes** — what was fixed and why

---

## Quick Fixes Reference

| Problem | Fix |
|---------|-----|
| Inconsistent outputs | Add few-shot examples |
| Wrong format | Add explicit format schema with example |
| Too long / rambling | Set word/sentence limits |
| Misses context | Add a `## Background` section |
| Ignores constraints | Move constraints before examples |
| Sounds robotic | Add persona or tone instruction |
