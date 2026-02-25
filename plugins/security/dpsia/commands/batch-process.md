# /dpsia:batch-process -- Process multiple pending DPSIA tickets for a client in batch

Process multiple vendor DPSIA assessments from a client's task management system.

## Prerequisites

- Client must be specified
- Access to client's task management system (ClickUp or Jira)
- `GRC_VAULT_PATH` configured (see SETUP.md)

## Steps

### 1. Initialize Batch

1. Identify client from user input; read client config for task system
2. Query pending tickets:

   **ClickUp:** Filter by DPSIA list/folder, status = pending/to-do/open

   **Jira:**
   ```jql
   project = [PROJECT] AND
   type = "Vendor Assessment" AND
   status IN ("To Do", "Open", "Pending")
   ```

3. Present ticket list for confirmation:
   ```
   📋 DPSIA BATCH: {client}

   Found {N} pending tickets:
   1. [TICKET-001] Acme Corp - Created 2025-01-05
   2. [TICKET-002] Beta Inc - Created 2025-01-06

   Process all? Select specific? (all/1,2,3/cancel)
   ```

### 2. Batch Execution

For each selected ticket:
1. Run the `assess` workflow (pass ticket ID and client)
2. Track progress:
   ```
   Processing: [2/5] Beta Inc
   ✅ Acme Corp - GREEN (Low Risk)
   ⏳ Beta Inc - In Progress...
   ⏸️ Gamma Ltd - Queued
   ```
3. Handle errors gracefully — log failures, continue with remaining tickets

### 3. Generate Batch Summary

Save to: `$GRC_VAULT_PATH/1-clients/[Client]/DPSIA/Batch-Summary-[YYYY-MM-DD].md`

```markdown
# DPSIA Batch Summary - {Client}
Date: {date}

## Overview
- Total Processed: {N}
- Approved (GREEN): {count}
- Conditional (AMBER): {count}
- Rejected (RED): {count}
- Failed/Skipped: {count}

## Results

| Vendor | RAG | Risk Score | Recommendation | Report |
|--------|-----|------------|----------------|--------|
| Acme Corp | 🟢 | 6/25 | Approve | [[Acme-DPSIA]] |
| Beta Inc | 🟡 | 12/25 | Conditional | [[Beta-DPSIA]] |
| Gamma Ltd | 🔴 | 18/25 | Reject | [[Gamma-DPSIA]] |

## Action Items
- [ ] Beta Inc: Request SOC 2 Type II report
- [ ] Gamma Ltd: Escalate to CISO for review
```

### 4. Human Review Gate

Before bulk task manager updates:
```
📋 BATCH COMPLETE

Summary:
✅ 3 Approved (GREEN)
⚠️ 1 Conditional (AMBER)
❌ 1 Rejected (RED)

Proceed with task manager updates? (y/n)
Review individual reports first? (review)
```

### 5. Task Manager Updates (on approval)

For each processed ticket: update status, attach individual DPSIA report, create follow-up subtasks.

## Error Handling

| Error | Action |
|-------|--------|
| Ticket fetch failed | Log and skip; report at end |
| Research timeout | Use partial data; note in report |
| Form not found | Proceed without; note in report |
| Task update failed | Log error; provide manual instructions |

## Output

```
✅ BATCH PROCESSING COMPLETE

📋 Client: {client_name}
📊 Processed: {total} tickets

Results:
🟢 Approved: {count}
🟡 Conditional: {count}
🔴 Rejected: {count}
❌ Failed: {count}

📝 Summary: $GRC_VAULT_PATH/1-clients/{client}/DPSIA/Batch-Summary-{date}.md
🎫 Tickets Updated: {count}
```

## Performance Notes

- Process tickets sequentially to avoid API rate limits
- Allow ~2–5 minutes per vendor for thorough research
- Save progress incrementally in case of interruption
