# /first-principles:deconstruct -- Break any problem into fundamental constituent parts and irreducible truths

**When to use:** Starting a first principles analysis, when a problem seems intractable, when costs/complexity seem fixed, when inherited solutions feel wrong.

---

## Process

### Step 1: Identify the Subject

What are we deconstructing?
- A problem to solve
- A system to understand
- A cost to reduce
- A constraint to examine
- An architecture to evaluate

**Write:** "We are deconstructing: [subject]"

### Step 2: List Stated Components

What does everyone say this is made of?
- What are the commonly accepted parts?
- What does the market/industry say?
- What would a typical description list?

List all stated components without judgment.

### Step 3: Go Deeper — Actual Constituents

For each component, ask: "What is THIS actually made of?"

- What are the material/physical constituents?
- What are the actual inputs required?
- What is the minimum viable version of this?
- If we bought raw materials, what would they cost?

**Classic example — Battery Pack:**
- Stated: "Battery pack = $600/kWh"
- Deeper: Cobalt + Nickel + Aluminum + Carbon + Polymers + Seal
- Actual: Raw materials on commodity market = ~$80/kWh
- Insight: 87% of cost is assembly/margin, not fundamental

### Step 4: Identify the Fundamental Truths

What remains when you can't decompose further?

**Fundamental truths are:**
- Laws of physics
- Mathematical certainties
- Empirically verified facts
- Irreducible requirements

**NOT fundamental truths:**
- Industry best practices
- "How it's always been done"
- Market prices
- Conventional wisdom

### Step 5: Map the Gap

| Stated Component | Actual Constituents | Gap / Insight |
|------------------|---------------------|---------------|
| [Market view] | [Fundamental parts] | [What we learned] |

---

## Output Template

```markdown
## Deconstruction: [Subject]

### What We're Told
[Common description]

### Stated Components
1. [Component 1]
2. [Component 2]

### Actual Constituents

**[Component 1]:**
- Actual parts: [list]
- Real cost/value: [amount]
- Insight: [what's different from stated]

### Fundamental Truths (Irreducible)
1. [Cannot be decomposed further]
2. [Physics/math/verified fact]

### Key Gaps Identified
| Stated | Actual | Gap |
|--------|--------|-----|
| [X costs $Y] | [Materials cost $Z] | [$Y-Z is not fundamental] |

### Implications
- [What this means for our approach]
- [What becomes possible now]
```

---

## Next Steps

After Deconstruct, flow to:
- `/first-principles:challenge` — question each constraint classification
- `/first-principles:reconstruct` — build optimal solution from fundamental truths
