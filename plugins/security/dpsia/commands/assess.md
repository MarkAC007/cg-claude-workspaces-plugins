# /dpsia:assess -- Full vendor DPSIA assessment with CIA triad, risk scoring, and report generation

Perform a Data Protection Security Impact Assessment (DPSIA) on a vendor.

## Prerequisites

- Client name specified (or determinable from context)
- Task ticket ID (ClickUp or Jira) OR vendor name
- `GRC_VAULT_PATH` configured (see SETUP.md)
- Access to client task management system

## Assessment Framework Reference

### Minimum Certification Bar

| Certification | Status |
|---------------|--------|
| ISO 27001 | Required — minimum ISMS compliance bar |
| SOC 2 Type II | Required — ongoing control effectiveness |
| SOC 2 Type I | Conditional — acceptable with enhanced monitoring |
| ISO 27017/27018 | Bonus — cloud providers only |

### Risk Rating Matrix (5×5)

```
LIKELIHOOD: 1=Rare  2=Unlikely  3=Possible  4=Likely  5=Almost Certain
IMPACT:     1=Negligible  2=Minor  3=Moderate  4=Major  5=Catastrophic
SCORE = LIKELIHOOD × IMPACT

20-25 = CRITICAL (Do not proceed without exec approval)
15-19 = HIGH (Remediation required before engagement)
8-14  = MEDIUM (Accept with compensating controls)
1-7   = LOW (Accept with standard monitoring)
```

### Breach Research Sources

| Source | URL | Purpose |
|--------|-----|---------|
| Have I Been Pwned | haveibeenpwned.com | Domain breach search |
| GDPR Enforcement Tracker | enforcementtracker.com | EU/EEA fines |
| ICO Enforcement | ico.org.uk/action-weve-taken | UK enforcement |
| FTC Enforcement | ftc.gov/legal-library | US enforcement |
| CVE Details | cvedetails.com | Product vulnerabilities |
| CISA KEV | cisa.gov/known-exploited-vulnerabilities | Active exploits |

## Steps

### 1. Initialize Assessment

1. Identify client (from user input or context)
2. Read client config: `$GRC_VAULT_PATH/1-clients/[client-name]/Client Overview.md`
3. Extract metadata:
   ```yaml
   task-system: clickup | jira
   dpsia-workbench-path: /path/to/supplier/forms
   lightrag-endpoint: http://... (optional)
   ```
4. If ticket ID provided — fetch via ClickUp MCP or Jira MCP tools; extract vendor name, description, requester

### 2. Supplier Evaluation Form Check

1. Search `dpsia-workbench-path` for vendor name:
   ```bash
   find {dpsia-workbench-path} -iname "*{vendor}*"
   ```
2. If found — read and parse; extract claimed certifications, locations, compliance statements; flag for verification
3. If not found — ask user for path, or proceed without (note in report)

### 3. Independent Research

Launch parallel research for each area:

| Area | Sources |
|------|---------|
| Company Overview | Website, LinkedIn, Crunchbase |
| Certifications | ISO registry, AICPA SOC portal, vendor trust page |
| Breach History | HIBP, GDPR Tracker, ICO, FTC |
| Vulnerabilities | CVE Details, CISA KEV, vendor advisories |
| News & Reviews | Recent incidents, customer feedback |

### 4. CIA Triad Assessment

**Confidentiality:** Access controls, encryption (at rest + in transit), data classification, privacy controls

**Integrity:** Change management, audit logging, data validation, version control

**Availability:** SLA commitments, redundancy/failover, disaster recovery, incident response

### 5. Risk Scoring

For each risk area: assess Likelihood (1–5) and Impact (1–5), calculate Score = L × I, apply threshold from matrix above.

### 6. Verification Summary

Compare research findings to Supplier Evaluation Form claims:

| Status | Meaning |
|--------|---------|
| Confirmed | Research validates the claim |
| Unverified | Cannot confirm, no contradicting evidence |
| Discrepancy | Research contradicts claim |
| Anomaly | Unexpected finding not in form |

### 7. Generate Report

Save DPSIA report to Obsidian:
```
$GRC_VAULT_PATH/1-clients/[Client]/DPSIA/[Vendor]-DPSIA-[YYYY-MM-DD].md
```

Report sections:
1. Executive Summary (RAG status, recommendation, key findings)
2. Vendor Overview (company, services, data processing role)
3. Certification Status (ISO 27001, SOC 2, validity dates)
4. Breach History (findings from all research sources)
5. CIA Triad Assessment (per-pillar findings)
6. Data Handling (processing, storage, transmission)
7. Supplier Evaluation Form Verification (Confirmed/Unverified/Discrepancies)
8. Risk Assessment (inherent, control effectiveness, residual)
9. Recommendation (Approve/Conditional/Reject with rationale)
10. Follow-up Actions (subtasks to create)

### 8. Human Review

Present summary:
```
📋 DPSIA COMPLETE: [Vendor]

🚦 RAG Status: [RED/AMBER/GREEN]
📊 Risk Score: [X/25] - [LEVEL]
✅ Certifications: ISO 27001 ✓, SOC 2 Type II ✓

🔍 Key Findings:
- [Finding 1]
- [Finding 2]

📝 Recommendation: [APPROVE/CONDITIONAL/REJECT]

Report saved to: [path]

Convert to Word and upload to [ClickUp/Jira]? (y/n)
```

### 9. Task Manager Update (on approval)

1. Convert report to Word (use DocConverter)
2. Upload to ClickUp or Jira ticket
3. Create follow-up subtasks
4. Update ticket status to reflect recommendation

## Output

```
✅ DPSIA COMPLETE

📋 Vendor: {vendor_name}
👤 Client: {client_name}
🚦 RAG: {RED|AMBER|GREEN}
📊 Risk: {score}/25 ({CRITICAL|HIGH|MEDIUM|LOW})

📝 Report: $GRC_VAULT_PATH/1-clients/{client}/DPSIA/{vendor}-DPSIA-{date}.md
📎 Word: {path if converted}
🎫 Ticket: {ticket_url if updated}
```
