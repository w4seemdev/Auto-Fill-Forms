---
description: Show application progress and follow-up reminders from the log
---

Read `applications-log.md` and report concisely:

1. **Totals by status**: `submitted-confirmed`, `submitted-unconfirmed`, `skipped`, `abandoned`, `interview`, `offer`, `rejected`.
2. **Recent applications**: a table of the most recent 15 rows (date, company, role, status).
3. **Follow-up flags**: first get today's date deterministically (run `Get-Date -Format yyyy-MM-dd` in PowerShell, or `date +%F`), then flag any row with a `submitted*` status dated 7+ days before it, with no later stage → list under "Consider a follow-up". Never guess today's date.
4. **Needs attention**: any `submitted-unconfirmed` row (submission may not have gone through) → tell the user to re-check.

If the log has no data rows yet, say so and point to `/apply`.
