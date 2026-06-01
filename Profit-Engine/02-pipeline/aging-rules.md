# AR Aging Rules

## Buckets

| Bucket | Days Outstanding | Action Required |
|--------|-----------------|------------------|
| Current | 0–30 | No action — monitor |
| Early Overdue | 31–60 | Friendly reminder email |
| Overdue | 61–90 | Phone call + escalation email to decision-maker |
| Seriously Overdue | 91–120 | Final notice + late fee assessment |
| Collections | 120+ | Hand off to collections / legal review |

## Escalation Triggers

- Any single invoice > $10,000 overdue by 15+ days → immediate manager alert.
- Same customer with 2+ open invoices in any bucket → flag for relationship review.
- Customer moves from Overdue → Seriously Overdue → auto-generate collections letter draft.

## Late Fees

- Assessed at 1.5% per month on any balance 31+ days overdue.
- Must be disclosed in original contract for enforcement.
- Fee can be waived once per customer per year as a goodwill gesture.

## Weekly Review Cadence

Run `/profit-engine:pipeline-review` every Monday morning.
Update invoice statuses in `invoices.json` after each payment received.
