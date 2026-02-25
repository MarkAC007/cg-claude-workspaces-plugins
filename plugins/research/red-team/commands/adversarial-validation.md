# /red-team:adversarial-validation -- Produce superior output through competing agents + critic

Use competing agents and a brutal critic to generate decisions, designs, or content that withstands scrutiny. Best when quality matters more than speed.

**When to use:** Feature specs, architectural decisions, code reviews with multiple valid approaches, content that needs to withstand scrutiny.

**vs. parallel-analysis:** `parallel-analysis` stress-tests existing content. `adversarial-validation` produces *new* content through competition.

---

## The Three-Round Protocol

### Round 1: Competing Proposals

Launch 2-3 specialized agents to produce competing solutions from different perspectives.

**Agent prompt:**
```
ADVERSARIAL VALIDATION - ROUND 1 (COMPETING PROPOSALS):

You are [PERSONA]. Generate your best solution to this problem.

Your perspective emphasizes:
- [Key concern 1]
- [Key concern 2]
- [Key concern 3]

Produce a complete solution that optimizes for YOUR priorities.
Be specific and detailed — this will be compared against other proposals.

[Problem/Task description]
```

**Suggested persona combinations:**

| Decision Type | Personas |
|---------------|---------|
| Architecture | Engineer (implementation ease), Architect (scalability/patterns), Security (attack surface) |
| Feature specs | Product (user value/simplicity), Engineer (feasibility/complexity), QA (testability/edge cases) |
| Content/writing | Subject Matter Expert (accuracy/depth), Audience Rep (clarity/engagement), Editor (structure/flow) |

### Round 2: Brutal Critique

A critic agent reads ALL proposals and evaluates each:

```
ADVERSARIAL VALIDATION - ROUND 2 (BRUTAL CRITIQUE):

You are the Harsh Critic. You have received [N] proposals for [problem].

For EACH proposal:

1. **What they got RIGHT:**
   - Acknowledge genuine strengths (be specific)

2. **What they got WRONG:**
   - Identify flaws, gaps, weaknesses
   - Point out what they conveniently ignored
   - Where does their perspective blind them?

3. **The Uncomfortable Truth:**
   - What none of them want to hear?
   - What's the real problem they're all dancing around?

4. **If forced to pick one:**
   - Which has the strongest foundation?
   - Why?

Be harsh but fair. The goal is truth, not destruction.

[Proposals from Round 1]
```

### Round 3: Collaborative Synthesis

The original agents read the critique and produce a unified solution:

```
ADVERSARIAL VALIDATION - ROUND 3 (COLLABORATIVE SYNTHESIS):

You are [PERSONA]. You've seen the Critic's brutal assessment.

Produce a SINGLE UNIFIED solution that:
- Addresses the valid criticisms
- Incorporates the best elements from each proposal
- Resolves the tensions between perspectives
- Acknowledges remaining trade-offs honestly

This is not compromise — it's synthesis. The final output should be BETTER
than any individual proposal, not just a blend.

[Original proposals + Critic's assessment]
```

---

## Single-Prompt Template

For quick execution without separate agent calls:

```
ADVERSARIAL VALIDATION - FULL PROTOCOL:

ROUND 1 - COMPETING PROPOSALS:
Generate 3 distinct solutions from different perspectives:

Proposal A (Pragmatist): Prioritizes ease of implementation and quick wins
Proposal B (Idealist): Prioritizes best practices and long-term quality
Proposal C (Skeptic): Prioritizes risk reduction and failure prevention

Each proposal should be complete and defensible.

ROUND 2 - BRUTAL CRITIQUE:
As a harsh but fair critic, evaluate all three:
- What each got right
- What each got wrong
- The uncomfortable truth none addressed
- Which has the strongest foundation

ROUND 3 - COLLABORATIVE SYNTHESIS:
Synthesize the best elements into a single superior solution that:
- Addresses valid criticisms
- Incorporates strengths from each proposal
- Resolves tensions between perspectives
- Honestly acknowledges remaining trade-offs

OUTPUT:
- Brief summary of the three proposals
- Key critique points
- Final synthesized recommendation with clear rationale

[Problem/Task to validate]
```

---

## Quality Signals

**Good output:**
- Each proposal genuinely represents its perspective (not strawmen)
- Critic finds real flaws, not nitpicks
- Synthesis is demonstrably better than any individual proposal
- Trade-offs are honestly acknowledged

**Bad signs:**
- Proposals are too similar
- Critic is too gentle or too destructive
- "Synthesis" is just one proposal with minor tweaks
- Trade-offs handwaved away

---

## When NOT to Use

- Simple decisions with obvious answers
- Time-critical situations
- Creative tasks where multiple valid outputs are fine
- Problems where expert consensus already exists
