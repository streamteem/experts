# Reprint log

List reprint tickets with parent job, qty, and the required reason text. Do not invent a reason. Do not silently add a rerun to tidy waste or a short ship. Charge versus no-charge stays as they coded. Proof rules on reprints follow the new ticket. Write-up is the log plus missing-reason asks, not a blame verdict. Stock and calendar still have to fit the new run.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: reprint-log
steps:
  - id: tickets
    needs: []
    produces: tickets
    produce_path: work/job-tickets.csv
    tool: docs/tools/job-ticket-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/job-tickets.csv job qty due
    on_fail: retry
    next: [log]
  - id: log
    needs: [tickets]
    produces: reprint-log
    produce_path: out/reprint-log.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/reprint-log.md
    on_fail: retry
    next: []
```
