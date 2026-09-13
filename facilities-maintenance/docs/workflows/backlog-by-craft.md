# Backlog by craft

Group approved, not-complete work orders by the craft they stored. Show ticket count and planned hours only when hours are on the file. Do not invent hours to fill a chart. Do not drop waiting-parts or waiting-shutdown if they still count those statuses. Write-up is a backlog pack for an in-house plant, not a construction punch and not a sold-but-unscheduled field-trade board.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: backlog-by-craft
steps:
  - id: tickets
    needs: []
    produces: tickets
    produce_path: work/wo.csv
    tool: docs/tools/wo-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/wo.csv wo craft status
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [tickets]
    produces: backlog
    produce_path: out/backlog-by-craft.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/backlog-by-craft.md
    on_fail: retry
    next: []
```
