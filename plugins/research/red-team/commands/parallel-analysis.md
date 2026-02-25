# /red-team:parallel-analysis -- Stress-test an argument via 32 expert agents

Military-grade adversarial analysis. Breaks arguments into 24 atomic claims, deploys 32 experts simultaneously, and produces a steelman + devastating counter-argument (8 points each, 12-16 words each).

## The Five Phases

| Phase | What Happens |
|-------|-------------|
| **Decomposition** | Break argument into 24 atomic claims |
| **Parallel Analysis** | 32 agents examine strengths AND weaknesses |
| **Synthesis** | Identify convergent insights |
| **Steelman** | 8-point strongest version of the argument |
| **Counter-Argument** | 8-point strongest rebuttal |

---

## PHASE 1: Decomposition

### Step 1.1: Extract Core Argument

Identify:
- Central thesis (one sentence)
- Key supporting claims (numbered list)
- Implicit assumptions (what must be true for this to work)
- Logical chain (A → B → C → conclusion)

### Step 1.2: Break Into 24 Atomic Claims

```
CLAIM 1: [First atomic claim]
CLAIM 2: [Second atomic claim]
...
CLAIM 24: [Twenty-fourth atomic claim]
```

Each claim must be: **self-contained**, **specific**, and **attackable**.

---

## PHASE 2: Parallel Agent Deployment

Deploy 32 agents in a **SINGLE message** with multiple Task tool calls. Each agent receives: the full argument, the 24-claim decomposition, their personality, and instructions to return a balanced critique.

### Agent Roster: 8 Engineers

| Agent | Personality | Attack Angle |
|-------|-------------|--------------|
| EN-1 | The Skeptical Systems Thinker — 30 years in distributed systems. | "Where does this break at scale?" |
| EN-2 | The Evidence Demander — Won't accept claims without data. | "Show me the numbers that prove this." |
| EN-3 | The Edge Case Hunter — Finds the 1% scenario that destroys assumptions. | "What happens when X is not true?" |
| EN-4 | The Historical Pattern Matcher — Has seen every failure mode. | "We tried this in 2008 and here's what happened." |
| EN-5 | The Complexity Realist — Simple solutions hide hard problems. | "This is harder than it sounds because..." |
| EN-6 | The Dependency Tracer — Follows assumptions to their roots. | "This assumes X, which assumes Y, which is false." |
| EN-7 | The Failure Mode Analyst — Thinks only about how things break. | "Here are 5 ways this fails catastrophically." |
| EN-8 | The Technical Debt Accountant — Calculates hidden costs. | "The real price of this approach is..." |

### Agent Roster: 8 Architects

| Agent | Personality | Attack Angle |
|-------|-------------|--------------|
| AR-1 | The Big Picture Thinker — Sees how pieces connect (or don't). | "This ignores how it fits into the larger system." |
| AR-2 | The Trade-off Illuminator — Nothing is free. | "You gain X but lose Y, and Y matters more." |
| AR-3 | The Abstraction Questioner — Challenges categorical thinking. | "These aren't the same category of problem." |
| AR-4 | The Incentive Mapper — Follows the money and motivation. | "Who benefits from this being true?" |
| AR-5 | The Second-Order Effects Tracker — Thinks three moves ahead. | "This causes A, which causes B, which destroys C." |
| AR-6 | The Integration Pessimist — Interfaces are where things break. | "This doesn't compose with existing reality." |
| AR-7 | The Scalability Skeptic — What works for 10 fails at 10,000. | "This can't scale because..." |
| AR-8 | The Reversibility Analyst — Some decisions can't be undone. | "Once you do this, you can't go back, and here's why that's bad." |

### Agent Roster: 8 Pentesters

| Agent | Personality | Attack Angle |
|-------|-------------|--------------|
| PT-1 | The Red Team Lead — Thinks like an attacker 24/7. | "Here's how I'd exploit this logic." |
| PT-2 | The Assumption Breaker — Finds the weak link in the chain. | "This depends on X, and X is false." |
| PT-3 | The Game Theorist — Models rational adversaries. | "A smart opponent would simply..." |
| PT-4 | The Social Engineer — Humans are the weak point. | "People will route around this because..." |
| PT-5 | The Precedent Finder — Has seen this pattern before. | "This is just [past example] in a new dress." |
| PT-6 | The Defense Evaluator — Judges if mitigations actually work. | "This defense fails because attackers can..." |
| PT-7 | The Threat Modeler — Maps attack surfaces systematically. | "You've left this entire surface undefended." |
| PT-8 | The Asymmetry Spotter — Where defenders are outmatched. | "Attackers have unlimited time; defenders don't." |

### Agent Roster: 8 Interns

| Agent | Personality | Attack Angle |
|-------|-------------|--------------|
| IN-1 | The Naive Questioner — Asks "why" until it breaks. | "But why do we assume X in the first place?" |
| IN-2 | The Analogy Finder — Connects to unrelated fields. | "This is just like [other field] where it failed." |
| IN-3 | The Contrarian — Takes the opposite position instinctively. | "What if the exact opposite is true?" |
| IN-4 | The Common Sense Checker — Too clever = wrong. | "This violates basic intuition because..." |
| IN-5 | The Zeitgeist Reader — Knows what's actually happening. | "In practice, nobody actually does this because..." |
| IN-6 | The Simplicity Advocate — Occam's razor everything. | "The simpler explanation is..." |
| IN-7 | The Edge Lord — Pushes to absurd conclusions. | "If this is true, then [absurd consequence] must be too." |
| IN-8 | The Devil's Intern — The argument the author hoped nobody would make. | "The uncomfortable truth nobody wants to say is..." |

### Agent Prompt Template

```
# BALANCED ANALYSIS - [AGENT ID]: [PERSONALITY NAME]

You are [PERSONALITY DESCRIPTION]. Your perspective is: "[PERSPECTIVE]"

## THE ARGUMENT TO ANALYZE:
[Full original argument]

## DECOMPOSED INTO 24 CLAIMS:
[24-claim breakdown]

## YOUR MISSION:
Provide an INDEPENDENT BALANCED ANALYSIS examining BOTH strengths AND weaknesses.

### PART A - STRENGTHS:
1. Which claim(s) are strongest? (cite claim numbers)
2. What evidence supports them? (2-3 sentences)
3. Why should we take this seriously? (1 sentence)

### PART B - WEAKNESSES:
1. Which claim(s) are weakest? (cite claim numbers)
2. What's the flaw? (2-3 sentences)
3. Why is this a problem? (1 sentence)

## OUTPUT FORMAT:
**[AGENT ID] ANALYSIS:**

**Strongest Point FOR:** [Claim #X]
[2-3 sentences on validity]
Take seriously because: [1 sentence]

**Strongest Point AGAINST:** [Claim #Y]
[2-3 sentences on flaw]
Problematic because: [1 sentence]

**Overall Assessment:** [One sentence verdict]
```

---

## PHASE 3: Synthesis

1. Collect all 32 analyses
2. **Convergent strengths:** 5+ agents = STRONG FOUNDATION | 3-4 = NOTABLE | 1-2 = INTERESTING SUPPORT
3. **Convergent weaknesses:** 5+ agents = CRITICAL WEAKNESS | 3-4 = SIGNIFICANT | 1-2 = NOTABLE INSIGHT
4. Categorize weaknesses: Logical Fallacies | Missing Evidence | Hidden Assumptions | Counterexamples | Precedent Contradictions | Second-Order Effects
5. Determine: Is the core thesis fundamentally sound with flawed execution, or fundamentally flawed?

---

## PHASE 4: Steelman Output

```
# STEELMAN

**The Position (Best Version):** [Strongest formulation]

**The Strongest Case FOR This Argument:**

1. [12-16 words]
2. [12-16 words]
3. [12-16 words]
4. [12-16 words]
5. [12-16 words]
6. [12-16 words]
7. [12-16 words]
8. [12-16 words]

**Validity Assessment:** [One sentence on the legitimate core concern]
```

---

## PHASE 5: Counter-Argument

Before drafting, classify all argument constraints:
- **HARD** (physics/reality — cannot attack)
- **SOFT** (policy/choice — can be challenged)
- **ASSUMPTION** (unvalidated — prime attack target)

The most devastating critiques target assumptions treated as HARD that are actually SOFT.

Additional checks:
- Claim type: Causal | Comparative | Categorical | Predictive | Normative
- Hidden assumptions: What must be true for this to work?
- Historical precedent: Has this argument been made before? What happened?
- Logical validity: Does the conclusion follow from the premises?
- Ensure counter defeats the **steelman**, not a weaker strawman

### Output Format

```
# RED TEAM VERDICT

**The Position:** [One sentence summary]

**The Counter-Argument:**

1. [12-16 words — establishes fundamental flaw]
2. [12-16 words — develops core weakness]
3. [12-16 words — historical precedent or analogy]
4. [12-16 words — hidden assumption exposed]
5. [12-16 words — counterexample or exception]
6. [12-16 words — what's conveniently ignored]
7. [12-16 words — second-order effects]
8. [12-16 words — knockout conclusion]

**Assessment:** [One sentence on fundamental soundness after analysis]
```

Each point: self-contained, attacks a real weakness, plain language, builds toward devastating conclusion.

---

## Execution Checklist

```
□ PHASE 1: Decomposition
  □ Extract central thesis and supporting claims
  □ Surface hidden assumptions
  □ Break into exactly 24 atomic claims

□ PHASE 2: Parallel Analysis
  □ Prepare 32 agent prompts with unique personalities
  □ Launch ALL 32 agents in a SINGLE message (parallel)
  □ Each agent examines BOTH strengths AND weaknesses

□ PHASE 3: Synthesis
  □ Identify convergent strengths (5+ = strong foundation)
  □ Identify convergent weaknesses (5+ = critical)
  □ Categorize by type
  □ Determine core thesis validity

□ PHASE 4: Steelman
  □ Reconstruct optimal version of the argument
  □ Draft 8-point steelman (12-16 words each)

□ PHASE 5: Counter-Argument
  □ Classify constraints: HARD/SOFT/ASSUMPTION
  □ Draft 8-point counter-argument (12-16 words each)
  □ Verify logical flow and escalation
  □ Confirm it defeats the steelman, not a strawman
```
