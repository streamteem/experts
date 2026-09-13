# Redo log

From their order sheet or redo workbook, list remake rows: original job, new job if assigned, and their reason code. Do not invent lab-error or non-adapt. Do not interpret the old or new Rx. Blank reason stays a question; do not treat the redo as complete. Warranty versus billable comes only from their warranty wording they already stored plus that code. Produce the log plus a write-up. Prefer job numbers. Extra complaint narrative stays out of docs/ when the code exists.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: redo-log
steps:
  - id: redos
    needs: []
    produces: redos
    produce_path: work/redo-log.csv
    tool: docs/tools/frame-order-sheet.md
    check: python docs/tools/checks/file-exists.py work/redo-log.csv
    on_fail: retry
    next: [columns]
  - id: columns
    needs: [redos]
    produces: redo-cols
    produce_path: work/redo-log.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/csv-has-columns.py work/redo-log.csv job reason
    on_fail: retry
    next: [write]
  - id: write
    needs: [redo-cols]
    produces: redo-writeup
    produce_path: out/redo-log.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/redo-log.md
    on_fail: retry
    next: []
```
