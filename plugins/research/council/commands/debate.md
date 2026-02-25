# /council:debate -- Full 3-round structured multi-agent debate with transcript

Structured debate where 4 specialized agents discuss a topic across 3 rounds (Initial Positions → Responses → Synthesis), producing visible transcript and final recommendation.

**Default council:** Architect, Designer, Engineer, Researcher

**Total time:** 30-90 seconds (parallel execution within rounds)

---

## Execution

### Step 1: Announce the Council

```markdown
## Council Debate: [Topic]

**Council Members:** [List agents participating]
**Rounds:** 3 (Positions → Responses → Synthesis)
```

### Step 2: Round 1 — Initial Positions

Launch 4 parallel Task calls (one per council member).

**Agent prompt:**
```
You are [Agent Name], [brief role description].

COUNCIL DEBATE - ROUND 1: INITIAL POSITIONS

Topic: [The topic being debated]

Give your initial position from your specialized perspective.
- Speak in first person
- Be specific and substantive (50-150 words)
- State your key concern, recommendation, or insight
- You'll respond to other council members in Round 2

Your perspective focuses on: [agent's domain]
```

**Agent domains:**
- **Architect**: System design, patterns, scalability, long-term architectural implications
- **Designer**: User experience, accessibility, user needs, interface implications
- **Engineer**: Implementation reality, tech debt, maintenance burden, practical constraints
- **Researcher**: Data, precedent, external examples, what others have done

**Output:**
```markdown
### Round 1: Initial Positions

**Architect:**
[Response]

**Designer:**
[Response]

**Engineer:**
[Response]

**Researcher:**
[Response]
```

### Step 3: Round 2 — Responses & Challenges

Launch 4 parallel Task calls with Round 1 transcript included.

**Agent prompt:**
```
You are [Agent Name], [brief role description].

COUNCIL DEBATE - ROUND 2: RESPONSES & CHALLENGES

Topic: [The topic being debated]

Here's what the council said in Round 1:
[Full Round 1 transcript]

Now respond to the other council members:
- Reference specific points they made ("I disagree with [Name]'s point about X...")
- Challenge assumptions or add nuance
- Build on points you agree with
- Maintain your specialized perspective
- 50-150 words

The value is in genuine intellectual friction—engage with their actual arguments.
```

**Output:**
```markdown
### Round 2: Responses & Challenges

**Architect:**
[Response referencing others' points]

**Designer:**
[Response referencing others' points]

**Engineer:**
[Response referencing others' points]

**Researcher:**
[Response referencing others' points]
```

### Step 4: Round 3 — Synthesis

Launch 4 parallel Task calls with Round 1 + Round 2 transcripts.

**Agent prompt:**
```
You are [Agent Name], [brief role description].

COUNCIL DEBATE - ROUND 3: SYNTHESIS

Topic: [The topic being debated]

Full debate transcript:
[Round 1 + Round 2 transcripts]

Final synthesis from your perspective:
- Where does the council agree?
- Where do you still disagree with others?
- What's your final recommendation given the full discussion?
- 50-150 words

Be honest about remaining disagreements—forced consensus is worse than acknowledged tension.
```

**Output:**
```markdown
### Round 3: Synthesis

**Architect:**
[Final synthesis]

**Designer:**
[Final synthesis]

**Engineer:**
[Final synthesis]

**Researcher:**
[Final synthesis]
```

### Step 5: Council Synthesis

```markdown
### Council Synthesis

**Areas of Convergence:**
- [Points where 3+ agents agreed]
- [Shared concerns or recommendations]

**Remaining Disagreements:**
- [Points still contested]
- [Trade-offs that couldn't be resolved]

**Recommended Path:**
[Based on convergence and weight of arguments...]
```

---

## Custom Council Members

| Request | Adjustment |
|---------|-----------|
| "Council with security" | Add security/pentester agent |
| "Council with intern" | Add intern agent (fresh perspective) |
| "Council with writer" | Add writer agent (communication focus) |
| "Just architect and engineer" | Only those two agents |

---

## When to Use vs. Quick

Use **Debate** for important decisions with real trade-offs. Use `/council:quick` for sanity checks and fast validation.
