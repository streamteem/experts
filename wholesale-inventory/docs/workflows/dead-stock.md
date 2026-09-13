# Slow-mover list

Only with last-movement or last-sale dates they provided, plus quantity. Do not call stock worthless or unsellable. Do not invent velocity. Days-on-hand needs their movement field. Keep owner and consignment labels out of house excess unless they said to include them. Kits can hide component movement; ask before you flag parts. You do not markdown, RTV, or dump. Quote the date column. Seasonal tags they stored stay visible.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: dead-stock
steps:
  - id: pull
    needs: []
    produces: move
    produce_path: work/movement.csv
    tool: docs/tools/item-master.md
    check: python docs/tools/checks/csv-has-columns.py work/movement.csv sku last_move
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [move]
    produces: dead-pack
    produce_path: out/slow-movers.md
    tool: docs/tools/item-master.md
    check: python docs/tools/checks/file-exists.py out/slow-movers.md
    on_fail: retry
    next: []
```
