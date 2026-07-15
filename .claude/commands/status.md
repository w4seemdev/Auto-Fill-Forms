---
description: Show application progress and follow-up reminders from the log
---

Read `applications-log.md` and report concisely:

1. **Totals by status**: `submitted-confirmed`, `submitted-unconfirmed`, `skipped`, `abandoned`, `interview`, `offer`, `rejected`.
2. **Recent applications**: a table of the most recent 15 rows (date, company, role, status).
3. **Follow-up flags**: any row with a `submitted*` status dated 7+ days ago (use today's date to compute age) with no later stage → list under "Consider a follow-up".
4. **Needs attention**: any `submitted-unconfirmed` row (submission may not have gone through) → tell the user to re-check.

If the log has no data rows yet, say so and point to `/apply`.
