# Kit list

Build a pick or kit list from the bill export times job qty, then mark short lines from the inventory export. Do not invent a component or a lot. Do not mark a kit complete when a line is short. Cert-required lines stay present-or-missing. Floor-stock labels stay as the BOM wrote them. They pick. You list. Write-up names the inventory export date.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: kit-list
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
    produces: kit-pack
    produce_path: out/kit-list.md
    tool: docs/tools/shortage-sheet.md
    check: python docs/tools/checks/file-exists.py out/kit-list.md
    on_fail: retry
    next: []
```
