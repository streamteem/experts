# RMA / returns pack

List open RMAs from their sheet: number, sku, qty, reason, and restock path as written. Do not invent an RMA. Attach damage-photo filenames if they stored them. Restock qty stays their inspect columns, not hope. You do not pay return postage and you do not apply a customer credit. They approve returns and they receive if that is their split. You do not invent a restock quantity.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: rma-returns
steps:
  - id: rma
    needs: []
    produces: rma
    produce_path: work/rma.csv
    tool: docs/tools/rma-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/rma.csv sku qty
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [rma]
    produces: rma-pack
    produce_path: out/rma-returns.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/rma-returns.md
    on_fail: retry
    next: []
```
