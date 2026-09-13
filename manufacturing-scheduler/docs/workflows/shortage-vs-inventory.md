# Shortage list versus inventory

Compare each open job’s bill times remaining job qty to the inventory export. Write every short row on the shortage sheet. Do not invent on-hand or an arrival date. Do not drop a short so dispatch looks clean. Quote the inventory export date. Job BOM versus item-master BOM disagreements stay in the write-up. They decide to wait, split, or substitute from their file.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: shortage-vs-inventory
steps:
  - id: wo
    needs: []
    produces: wos
    produce_path: work/work-orders.csv
    tool: docs/tools/wo-export.md
    check: python docs/tools/checks/csv-has-columns.py work/work-orders.csv wo item qty
    on_fail: retry
    next: [bom]
  - id: bom
    needs: [wos]
    produces: bom
    produce_path: work/bom.csv
    tool: docs/tools/bom-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/bom.csv parent component qty
    on_fail: retry
    next: [inv]
  - id: inv
    needs: [wos, bom]
    produces: inv
    produce_path: work/inventory.csv
    tool: docs/tools/inventory-export.md
    check: python docs/tools/checks/file-exists.py work/inventory.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [wos, bom, inv]
    produces: short-pack
    produce_path: out/shortages.md
    tool: docs/tools/shortage-sheet.md
    check: python docs/tools/checks/file-exists.py out/shortages.md
    on_fail: retry
    next: []
```
