# PTO log

List balances and requests from their PTO sheet. Keep their column names for vacation, sick, or combined banks. Status stays as they coded it. You do not approve or deny. You do not invent remaining hours or an accrual rate. If balance is blank, ask or leave blank. Overlaps are flags they resolve. Write the log and a short write-up. Holiday calendars stay a separate file unless they already rolled hours in.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: pto-log
steps:
  - id: pto
    needs: []
    produces: pto
    produce_path: work/pto.csv
    tool: docs/tools/pto-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/pto.csv name
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [pto]
    produces: pto-pack
    produce_path: out/pto-log.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/pto-log.md
    on_fail: retry
    next: []
```
