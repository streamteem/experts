# Open common-area work orders

From their export, list open common-area jobs, locations, vendors, and missing vendor or photo fields. No engineering judgment and no owner-versus-association legal call unless you quote their matrix. Emergency flags use their on-call list, not a web search. One community per list unless they asked for a labeled portfolio. Produce the CSV the checks can see, then the write-up. Confirm the association name on the export header before you list jobs.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: work-orders
steps:
  - id: pull
    needs: []
    produces: wo-raw
    produce_path: work/work-orders.csv
    tool: docs/tools/work-order-export.md
    check: python docs/tools/checks/file-exists.py work/work-orders.csv
    on_fail: retry
    next: [columns]
  - id: columns
    needs: [wo-raw]
    produces: wo-cols
    produce_path: work/work-orders.csv
    tool: docs/tools/work-order-export.md
    check: python docs/tools/checks/csv-has-columns.py work/work-orders.csv wo status
    on_fail: retry
    next: [write]
  - id: write
    needs: [wo-cols]
    produces: wo-writeup
    produce_path: out/work-orders.md
    tool: docs/tools/work-order-export.md
    check: python docs/tools/checks/file-exists.py out/work-orders.md
    on_fail: retry
    next: []
```
