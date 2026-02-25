# /prompting:generate -- Generate a structured prompt using Anthropic best practices

Generate an optimised, production-ready prompt from a plain-language description.

## ALL GENERATED FILES GO TO ~/Downloads/ FIRST

Save any generated prompt files to `~/Downloads/` — never directly into project directories.

---

## Process

### Step 1: Gather Intent

Ask:
1. What task should the prompt perform?
2. Who/what is the "agent" executing it? (Claude, a pipeline, a widget)
3. What does a great output look like? Any examples?
4. Any constraints? (length, format, tone, audience)

### Step 2: Apply Anthropic Best Practices

Structure the prompt using these principles:

### Core Structure

```markdown
## Role / Identity (optional but powerful)
[Who the model is acting as]

## Task
[Clear statement of what to do — imperative, not vague]

## Context
[Background the model needs that it may not have]

## Input Format
[How the input data is structured]

## Output Format
[Exact format expected — use examples liberally]

## Constraints
[What to avoid, limits, rules]

## Examples (Few-Shot)
[2-3 concrete input → output pairs when accuracy matters]
```

### Key Principles

- Markdown-first design (use `##` headers, bullet points, code fences)
- Put instructions before examples
- Be specific about output format — vague formats produce vague outputs
- Separate concerns: role ≠ task ≠ format
- Front-load the most critical constraint
- Use positive framing: "do X" beats "don't do Y"

### Step 3: Draft the Prompt

Generate the prompt applying the structure above. Include:
- Concrete output format example
- At least one few-shot example if the task is non-trivial
- Explicit constraints

### Step 4: Self-Review Checklist

- [ ] Task is unambiguous — two experts would execute it identically
- [ ] Output format is fully specified (no "respond appropriately")
- [ ] Constraints are positive where possible
- [ ] Length is appropriate — no padding, no missing context
- [ ] Examples, if included, are representative not cherry-picked

### Step 5: Output

Deliver the finished prompt in a code block plus a brief rationale for key design choices.

---

## Prompt Anti-Patterns to Avoid

| Anti-Pattern | Fix |
|---|---|
| "Be helpful and thorough" | State the specific task |
| "Respond in JSON" with no schema | Include the exact schema |
| Walls of XML tags | Use Markdown headers |
| Buried constraints at the end | Front-load critical rules |
| "Answer like an expert" with no domain | Specify the domain and expertise level |
