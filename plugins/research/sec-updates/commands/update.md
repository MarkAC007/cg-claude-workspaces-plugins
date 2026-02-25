# /sec-updates:update -- Fetch and rank security news from major sources

Aggregate security news from multiple sources into crisp, ranked updates across three categories.

---

## Sources

| Source | URL | Type |
|--------|-----|------|
| tl;dr sec | https://tldrsec.com | Newsletter — comprehensive security roundup |
| No Security | https://no.security | Caleb Sima's security insights |
| Krebs on Security | https://krebsonsecurity.com | Investigative journalism |
| The Hacker News | https://thehackernews.com | Security news and analysis |
| Schneier on Security | https://schneier.com | Bruce Schneier's blog |
| Risky Business | https://risky.biz | Security podcast/news |

---

## Process

### Step 1: Fetch Sources (Parallel)

Use WebFetch on each source URL. For each:
> "Extract all article headlines and summaries from this security site. For each item: title, 1-2 sentence summary, publication date if available. Focus on content from the last 7 days."

### Step 2: Categorise Items

| Category | Criteria |
|----------|----------|
| 🔴 **News** | Breaches, incidents, active attacks, exploitations, ransomware |
| 🔬 **Research** | CVEs, vulnerabilities, techniques, tools, papers, bug bounty |
| 💡 **Ideas** | Opinions, trends, strategy, regulatory news, career, predictions |

### Step 3: Rank by Importance

Score items 1-10 per category:
- **Impact (0-3)**: How many affected? How severe?
- **Recency (0-3)**: How new?
- **Actionability (0-2)**: Can the reader act on this?
- **Novelty (0-2)**: Genuinely new information?

Sort descending by score within each category.

### Step 4: Apply Limits

- Max **32 items total**
- Target ~10-12 per category if content available
- Redistribute if one category is sparse
- Never exceed 32 total

### Step 5: Generate Output

```markdown
# Security Updates
**Generated:** [YYYY-MM-DD HH:MM TZ]
**Sources Checked:** [list of sources that responded]
**Period:** Since [last check date or "Last 7 days"]

---

## 🔴 Security News (Breaches & Incidents)

1. **[Headline]** — [1-2 sentence summary]. [Source]
2. ...

---

## 🔬 Security Research

1. **[Title]** — [1-2 sentence summary]. [Source]
2. ...

---

## 💡 Security Ideas

1. **[Title]** — [1-2 sentence summary]. [Source]
2. ...

---

## 📊 Summary
| Category | Count | Top Item |
|----------|-------|----------|
| News | X | [headline] |
| Research | X | [title] |
| Ideas | X | [title] |

**Total:** X/32 items
```

---

## Anti-Patterns

| Bad | Good |
|-----|------|
| Long paragraph summaries | 1-2 crisp sentences |
| Unranked list dumps | Importance-ordered items |
| 50+ items | Max 32, quality curated |
| Mixing categories | Clear News / Research / Ideas separation |
| Old news | Only items from last check period |
