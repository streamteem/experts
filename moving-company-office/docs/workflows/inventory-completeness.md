# Inventory completeness

Compare the inventory sheet to rooms, PBO versus CP codes, and the high-value list if their rule requires one. Flag missing rooms, blank cube columns, and “see photos” with no photo. Do not invent a piece, a cube, or a pound. Photos they stored get an index; you do not invent a shot. They resurvey. You write the hole list and write-up the check can see.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: inventory-completeness
steps:
  - id: inv
    needs: []
    produces: inv
    produce_path: work/inventory.csv
    tool: docs/tools/inventory-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/inventory.csv job item qty
    on_fail: retry
    next: [photos]
  - id: photos
    needs: [inv]
    produces: photos
    produce_path: work/photo-index.csv
    tool: docs/tools/photo-folder.md
    check: python docs/tools/checks/file-exists.py work/photo-index.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [inv, photos]
    produces: inv-pack
    produce_path: out/inventory-completeness.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/inventory-completeness.md
    on_fail: retry
    next: []
```
