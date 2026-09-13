# Count versus guarantee

List expected, guaranteed, and any actual they recorded, plus vegetarian, kids, and vendor-meal splits as their sheet adds them. Flag missing guarantees past cutoff and math that does not add. Guarantee wins kitchen and pack-out math. Do not invent a count from a room size or a saved BEO occupancy line. Do not lower a guarantee to tidy a package. Write-up quotes the source file for each number. They collect finals. You list holes.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: count-vs-guarantee
steps:
  - id: orders
    needs: []
    produces: orders
    produce_path: work/count-orders.csv
    tool: docs/tools/event-order-pdf.md
    check: python docs/tools/checks/csv-has-columns.py work/count-orders.csv event guarantee
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [orders]
    produces: count-pack
    produce_path: out/count-vs-guarantee.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/count-vs-guarantee.md
    on_fail: retry
    next: []
```
