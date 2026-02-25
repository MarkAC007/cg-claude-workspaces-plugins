# /council:quick -- Fast single-round perspective check from 4 specialized agents

Gather immediate takes from 4 specialized agents in parallel. Use for sanity checks and quick validation before committing to a direction.

**Total time:** 10-20 seconds

---

## Execution

### Step 1: Announce Quick Council

```markdown
## Quick Council: [Topic]

**Council Members:** [List agents]
**Mode:** Single round (fast perspectives)
```

### Step 2: Parallel Perspective Gathering

Launch all council members in parallel (single Task call batch).

**Agent prompt:**
```
You are [Agent Name], [brief role description].

QUICK COUNCIL CHECK

Topic: [The topic]

Give your immediate take from your specialized perspective:
- Key concern, insight, or recommendation
- 30-50 words max
- Be direct and specific

This is a quick sanity check, not a full debate.
```

### Step 3: Output Perspectives

```markdown
### Perspectives

**Architect:**
[Brief take]

**Designer:**
[Brief take]

**Engineer:**
[Brief take]

**Researcher:**
[Brief take]

### Quick Summary

**Consensus:** [Do they generally agree? On what?]
**Concerns:** [Any red flags raised?]
**Recommendation:** [Proceed / Reconsider / Need full debate]
```

---

## When to Escalate

If the quick check reveals significant disagreement or complex trade-offs:

```
⚠️ This topic has enough complexity for a full council debate.
Run: /council:debate for 3-round structured discussion.
```
