# Day occupancy / boarding list

From their boarding export, list the stay date by patient-dog, client label they allow, stay type, and crate or playgroup as stored. Confirm the file date before you treat it as today. Do not invent a missing card. Do not diagnose from a floor note. Do not decide a vaccine is due. Never release a dog from this list. If capacity and booked disagree, quote both in the write-up. Starter / guess until they teach which report is today’s board.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: boarding-day
steps:
  - id: pull
    needs: []
    produces: board
    produce_path: work/boarding.csv
    tool: docs/tools/boarding-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/boarding.csv patient stay
    on_fail: retry
    next: [cap]
  - id: cap
    needs: [board]
    produces: cap
    produce_path: work/capacity.csv
    tool: docs/tools/capacity-file.md
    check: python docs/tools/checks/csv-has-columns.py work/capacity.csv room max
    on_fail: retry
    next: [write]
  - id: write
    needs: [board, cap]
    produces: board-pack
    produce_path: out/boarding-day.md
    tool: docs/tools/boarding-csv.md
    check: python docs/tools/checks/file-exists.py out/boarding-day.md
    on_fail: retry
    next: []
```
