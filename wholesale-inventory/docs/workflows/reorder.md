# Reorder list

List SKUs at or below their min from their stock file, using their on-hand and on-order columns if present. Do not invent mins or demand. Do not place a purchase order or pay a vendor. Say which UOM the suggestion uses and convert only with their pack. MOQ and price breaks are copied, not reasons to overload a dead SKU. Consignment and customer-owned lines stay out of house buys unless they said to include them.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: reorder
steps:
  - id: pull
    needs: []
    produces: stock
    produce_path: work/stock.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/csv-has-columns.py work/stock.csv sku on_hand min
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [stock]
    produces: reorder-pack
    produce_path: out/reorder.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/reorder.md
    on_fail: retry
    next: []
```
