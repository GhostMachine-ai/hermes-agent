---
description: Draft follow-up actions for leads based on cadence history. Reads cadence-log.json and the specified lead file. Usage: /profit-engine:follow-up [lead-id or "all"]
---

Review leads and draft next follow-up actions based on cadence history.

## Steps

1. If a specific lead-id was given, read `Profit-Engine/03-crm/leads/<lead-id>.md`.
   If "all" was given, list all files in `Profit-Engine/03-crm/leads/` (skip `_template.md`) and process each.
2. Read `Profit-Engine/03-crm/cadence-log.json` and filter entries for the relevant lead(s).
3. For each lead:
   a. Determine the current stage from the frontmatter.
   b. Find the most recent cadence entry and the `next_due` date.
   c. Check if follow-up is overdue (`next_due` < today).
4. Draft a follow-up message using the ghost persona (`Profit-Engine/04-coach/ghost-persona.md`):
   - Email if last channel was email and <24h response time expected.
   - Phone/LinkedIn if email has been tried twice with no response.
   - Adjust tone by stage: warmer for prospects, more direct for negotiation.
5. Output for each lead:

   **Lead**: [name] @ [company] | Stage: [stage] | Last touch: [date] | Next due: [date]  
   **Suggested channel**: [email / phone / LinkedIn]  
   **Draft message**:
   > [draft follow-up text]

   **Cadence-log entry to add** (copy-paste ready JSON):
   ```json
   { "lead_id": "...", "date": "...", "channel": "...", "summary": "...", "outcome": "pending", "next_due": "..." }
   ```

6. After the user approves, remind them to append the cadence-log entry to `cadence-log.json`.
