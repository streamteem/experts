# Frame and lens order completeness

From their frame-order sheet, list missing required fields as questions: frame SKU, lens type as already stored, treatments they checked, PD and add only if on file, lab destination, job number. Do not interpret the Rx to finish a blank ticket. Do not invent a frame price; use the fee file when they asked for a posted amount. Do not pick a progressive or AR. Redo rows still need their reason code. Produce the missing-fields list plus a write-up. They send the ticket to the lab.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: frame-lens-order-completeness
steps:
  - id: orders
    needs: []
    produces: orders
    produce_path: work/frame-orders.csv
    tool: docs/tools/frame-order-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/frame-orders.csv chart job
    on_fail: retry
    next: [fees]
  - id: fees
    needs: [orders]
    produces: fees
    produce_path: work/fee-file.csv
    tool: docs/tools/fee-file.md
    check: python docs/tools/checks/file-exists.py work/fee-file.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [orders, fees]
    produces: order-writeup
    produce_path: out/frame-lens-missing.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/frame-lens-missing.md
    on_fail: retry
    next: []
```
