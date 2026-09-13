# Custom cake board

List open cake and wedding tickets from the cake-order folder against the production calendar: due, flavor-from-menu, size, filling and buttercream names, deposit flag, photo present yes/no. Do not invent a formula, servings, or a due the calendar cannot meet. Do not store PAN. Tasting notes are not tickets. Write-up is the board plus missing fields. They bake and decorate. Missing formula pointers stay asks. They bake and decorate; you board.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: custom-cake-board
steps:
  - id: orders
    needs: []
    produces: orders
    produce_path: work/cake-orders.csv
    tool: docs/tools/cake-order-folder.md
    check: python docs/tools/checks/file-exists.py work/cake-orders.csv
    on_fail: retry
    next: [cal]
  - id: cal
    needs: [orders]
    produces: cal
    produce_path: work/production-calendar.csv
    tool: docs/tools/calendar.md
    check: python docs/tools/checks/file-exists.py work/production-calendar.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [orders, cal]
    produces: cake-pack
    produce_path: out/custom-cake-board.md
    tool: docs/tools/cake-order-folder.md
    check: python docs/tools/checks/file-exists.py out/custom-cake-board.md
    on_fail: retry
    next: []
```
