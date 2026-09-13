# Missing Rx on order

From the frame-order sheet, list jobs that their process says need a spectacle or contact-lens Rx file and the file is not present. Do not interpret a Rx image to finish the ticket. Do not invent PD, add, or lens type. Do not mark the ticket complete. Outside-Rx transfers still need a named file. Produce the missing-Rx list plus a write-up. They obtain the file. Prefer chart and job number. Extra refraction values stay out of docs/ when a present-or-missing flag will do.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: missing-rx-on-order
steps:
  - id: orders
    needs: []
    produces: orders
    produce_path: work/frame-orders.csv
    tool: docs/tools/frame-order-sheet.md
    check: python docs/tools/checks/file-exists.py work/frame-orders.csv
    on_fail: retry
    next: [columns]
  - id: columns
    needs: [orders]
    produces: order-cols
    produce_path: work/frame-orders.csv
    tool: docs/tools/frame-order-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/frame-orders.csv chart job
    on_fail: retry
    next: [write]
  - id: write
    needs: [order-cols]
    produces: rx-writeup
    produce_path: out/missing-rx.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/missing-rx.md
    on_fail: retry
    next: []
```
