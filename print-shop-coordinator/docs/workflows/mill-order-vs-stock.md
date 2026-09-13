# Mill order versus stock

Join the mill-order sheet to on-hand stock: promised dock dates, special-order flags, and which open tickets wait on paper. Do not invent a mill promise. Do not pay the mill. If a promise is after a job due, flag infeasible. Receipts that have not hit inventory stay not-on-hand. Write-up is late paper plus affected jobs, not a substitute you pick.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: mill-order-vs-stock
steps:
  - id: mill
    needs: []
    produces: mill
    produce_path: work/mill-orders.csv
    tool: docs/tools/mill-order-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/mill-orders.csv item date
    on_fail: retry
    next: [stock]
  - id: stock
    needs: [mill]
    produces: stock
    produce_path: work/stock.csv
    tool: docs/tools/stock-csv.md
    check: python docs/tools/checks/file-exists.py work/stock.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [mill, stock]
    produces: mill-pack
    produce_path: out/mill-order-vs-stock.md
    tool: docs/tools/mill-order-sheet.md
    check: python docs/tools/checks/file-exists.py out/mill-order-vs-stock.md
    on_fail: retry
    next: []
```
