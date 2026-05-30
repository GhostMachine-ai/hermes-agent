---
description: Run a weekly AR pipeline review. Reads invoices.json and aging-rules.md, then fills in the weekly-snapshot.md template. Usage: /profit-engine:pipeline-review
---

Produce a weekly accounts-receivable pipeline snapshot.

## Steps

1. Read `Profit-Engine/02-pipeline/invoices.json` to load all invoice records.
2. Read `Profit-Engine/02-pipeline/aging-rules.md` for bucket definitions and escalation triggers.
3. Classify each invoice into its aging bucket based on `days_outstanding`.
4. Calculate totals per bucket and overall AR balance.
5. Identify any escalation triggers:
   - Invoices > $10,000 with 15+ days outstanding → flag immediately.
   - Customers with 2+ open invoices in any bucket → flag for relationship review.
   - Invoices crossing from Overdue into Seriously Overdue → note for collections letter.
6. Suggest specific next actions per at-risk account, referencing the contact field.
7. Fill in and output the snapshot using the template in `Profit-Engine/02-pipeline/weekly-snapshot.md`.

## Output format

Use the weekly-snapshot.md template exactly. Fill in every field.
End the snapshot with a prioritized **Actions Due Next Week** list — most urgent first.

## After review

Remind the user:
- Update invoice statuses in `invoices.json` after any payments received.
- Save the completed snapshot by renaming it `weekly-snapshot-YYYY-MM-DD.md` before the next run.
