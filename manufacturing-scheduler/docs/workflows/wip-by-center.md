# WIP by work center

Group open work-order quantity by work center from the export and the work-center list. Do not hide WIP. Do not invent a location. Holds for shortage, ECO, or MRB stay labeled. Outside-process quantity stays on the outside row, not folded into an in-house center. If the export and a floor count they typed disagree, quote both. They move travelers; you list.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: wip-by-center
steps:
  - id: wo
    needs: []
    produces: wos
    produce_path: work/work-orders.csv
    tool: docs/tools/wo-export.md
    check: python docs/tools/checks/csv-has-columns.py work/work-orders.csv wo item qty
    on_fail: retry
    next: [centers]
  - id: centers
    needs: [wos]
    produces: centers
    produce_path: work/work-centers.csv
    tool: docs/tools/work-center-list.md
    check: python docs/tools/checks/file-exists.py work/work-centers.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [wos, centers]
    produces: wip-pack
    produce_path: out/wip-by-center.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/wip-by-center.md
    on_fail: retry
    next: []
```
