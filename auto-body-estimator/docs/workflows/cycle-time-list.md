# Cycle-time list

List stage dates from their cycle calendar joined to open estimates. Never invent a delivery day. Never promise rental days from a remembered average. Backorders and supplement waits stay visible. If calendar and estimate promise disagree, quote both. Write-up is the stage list plus conflicts, not a new promise to the customer or the DRP. You do not bump another job to invent open booth time. Write-up is dates from their file plus conflicts, not a new promise. Rental days still need the rental log, not this calendar alone.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: cycle-time-list
steps:
  - id: cal
    needs: []
    produces: calendar
    produce_path: work/cycle-calendar.csv
    tool: docs/tools/calendar-cycle.md
    check: python docs/tools/checks/file-exists.py work/cycle-calendar.csv
    on_fail: retry
    next: [est]
  - id: est
    needs: [calendar]
    produces: est
    produce_path: work/estimate-export.csv
    tool: docs/tools/estimate-export.md
    check: python docs/tools/checks/file-exists.py work/estimate-export.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [calendar, est]
    produces: cycle-pack
    produce_path: out/cycle-time-list.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/cycle-time-list.md
    on_fail: retry
    next: []
```
