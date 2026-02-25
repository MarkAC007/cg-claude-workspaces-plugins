# /first-principles:reconstruct -- Build an optimal solution using only fundamental truths

**Core principle:** "If we knew nothing about how this is currently done, and only knew the fundamental truths, what would we build?"

Optimise for **function** (what to accomplish) not **form** (how it's traditionally done).

**When to use:** After Deconstruct + Challenge, when existing solutions are clearly suboptimal, when you need to escape local maxima.

---

## Process

### Step 1: State Only the Hard Constraints

From your Challenge analysis, list ONLY:
- Laws of physics
- Mathematical requirements
- Verified empirical facts
- True immutable requirements

**Exclude:** Soft constraints, assumptions, "how it's always been done."

**Write:** "The only things that MUST be true: [list]"

### Step 2: Define the Function

What is the actual outcome you need?

| Form (wrong) | Function (right) |
|---|---|
| "We need a database" | "We need to persist and retrieve user data reliably" |
| "We need microservices" | "We need to deploy and scale components independently" |
| "We need a mobile app" | "Users need to accomplish X from anywhere" |

**Write:** "The function we're optimising for: [outcome]"

### Step 3: Blank Slate Design

Pretend you've never seen the current solution. Ask:
- If an alien with perfect engineering knowledge landed today, what would they build?
- If we were starting a new company to solve only this problem, what would we do?

**Generate 3+ approaches** without filtering for feasibility yet.

### Step 4: Cross-Domain Synthesis

Solutions in unrelated fields often apply:
- What industry has solved an analogous problem?
- What technology from another domain could apply?

**The snowmobile insight:** Tank treads + Boat motor + Bicycle seat = new category

### Step 5: Evaluate Against Function

| Solution | Satisfies Hard Constraints? | Achieves Function? | Simpler Than Current? |
|----------|----------------------------|--------------------|-----------------------|
| Option A | Yes/No | Yes/No | Yes/No |
| Option B | Yes/No | Yes/No | Yes/No |

Best solution: satisfies constraints, achieves function, maximises simplicity.

### Step 6: Compare to Current Approach

| Aspect | Current | Reconstructed | Delta |
|--------|---------|---------------|-------|
| Complexity | [X] | [Y] | Simpler/Same/More |
| Cost | [X] | [Y] | Lower/Same/Higher |
| Performance | [X] | [Y] | Better/Same/Worse |

---

## Output Template

```markdown
## Reconstruction: [Subject]

### Hard Constraints Only
1. [Immutable constraint 1]
2. [Immutable constraint 2]

### Function to Optimise
[Outcome, not method]

### Blank Slate Solutions

**Option A: [Name]**
- Approach: [Description]
- Satisfies constraints: [How]
- Pros: [Benefits] | Cons: [Drawbacks]

**Option B: [Name]**
- Approach: [Description]
- Satisfies constraints: [How]
- Pros: [Benefits] | Cons: [Drawbacks]

### Cross-Domain Insights
- From [Field]: [Applicable concept]

### Recommended Solution
**[Option X]** because [reasoning]

### What We're Eliminating
- [Complexity that wasn't fundamental]

### Implementation Path
1. [First step]
2. [Second step]
```

---

## Common Reconstruction Patterns

**"Do We Even Need This?"** — Often the reconstructed solution eliminates entire components:
- "We need a message queue" → Direct calls work at our scale
- "We need Kubernetes" → A single server handles our load

**"Different Technology, Same Function"** — Form changes completely:
- "Web app" → "CLI tool" (if users are technical)
- "Custom solution" → "Spreadsheet" (if sufficient)

**"Combine Steps"** — Removing soft constraints allows simplification:
- "Microservices" → "Modular monolith"
- "ETL pipeline" → "Query on read"
