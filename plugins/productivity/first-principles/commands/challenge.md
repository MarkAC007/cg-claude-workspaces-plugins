# /first-principles:challenge -- Systematically challenge every assumption and constraint

**Core question for every constraint:** "Is this a law of physics, or is it a choice someone made?"

**When to use:** After Deconstruct, when requirements feel overly restrictive, when "we can't do X" is stated without evidence, for adversarial analysis.

---

## Process

### Step 1: List All Stated Constraints

Gather everything presented as a constraint:
- Requirements documents
- "We have to..." statements
- Industry best practices
- Historical decisions
- Budget/timeline limits
- Technical limitations
- Policy requirements

List every constraint without filtering.

### Step 2: Classify Each Constraint

| Type | Definition | Test |
|------|------------|------|
| **HARD** | Physics/math/reality | Would violating this break laws of nature? |
| **SOFT** | Policy/choice/convention | Could a decision-maker change this? |
| **ASSUMPTION** | Unvalidated belief | Has this been tested? What's the evidence? |

### Step 3: Challenge Each Non-Hard Constraint

**For SOFT constraints:**
- Who made this decision and why?
- What would happen if we violated it?
- Is the original reason still valid?

**For ASSUMPTIONS:**
- What evidence supports this?
- Has anyone tested the opposite?
- What would prove this wrong?

### Step 4: The "Remove It" Test

For each soft constraint and assumption:
> "If we removed this entirely, what would become possible?"

If removing it unlocks significant value → worth challenging.

### Step 5: Find Hidden Assumptions

The most dangerous constraints are the ones so assumed they're never stated:
- "Of course we need a database" — Do we?
- "Obviously this needs authentication" — Does it?
- "Users expect a web interface" — Do they?

---

## Output Template

```markdown
## Constraint Analysis: [Subject]

### HARD Constraints (Physics/Reality)
| Constraint | Why It's Hard |
|------------|---------------|
| [X] | [Physics law — cannot change] |

### SOFT Constraints (Policy/Choice)
| Constraint | Who Decided | Original Reason | Still Valid? | If Removed? |
|------------|-------------|-----------------|--------------|-------------|
| [X] | [Person/team] | [Why] | Yes/No | [What's possible] |

### ASSUMPTIONS (Unvalidated)
| Assumption | Evidence | Counter-Evidence | How to Test |
|------------|----------|------------------|-------------|
| [X] | [Supports it] | [Contradicts it] | [Method] |

### Hidden Constraints Found
- [Implicit assumption never stated]

### Constraints Worth Challenging
1. **[Constraint]:** [Why, what becomes possible]

### Recommended Actions
- [ ] Validate assumption: [X] by [method]
- [ ] Challenge soft constraint: [Y] with [stakeholder]
- [ ] Accept hard constraint: [Z] and design around it
```

---

## Challenge Questions by Domain

**Technical:** Is this a language limitation or fundamental? Could different tech remove it?

**Business:** Is this budget fixed or just "the obvious solution" budget? Is the deadline real or arbitrary?

**Security:** Is this control preventing a real attack or a theoretical one? Security or security theater?

**UX:** Have we tested this with actual users? Are we confusing user needs with user habits?

**Architecture:** Is this pattern required or just familiar? Could a simpler solution work?

---

## Next Step

Flow to `/first-principles:reconstruct` → build optimal solution using only hard constraints.
