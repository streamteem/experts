# Pending ECO as file

List open work orders against the ECO log and the drawing index. Pending changes stay pending. You do not approve an ECO. You do not mark a job safe to run through a hold. Effectivity blanks stay blank and become asks. Traveler rev versus to-rev mismatches stay on the pack. They stamp the change. You only show the file. Hold-WIP notes on the log keep those jobs visible as held on any dispatch you also touch. You do not approve the change.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: eco-pending-as-file
steps:
  - id: eco
    needs: []
    produces: eco
    produce_path: work/eco-log.csv
    tool: docs/tools/eco-log.md
    check: python docs/tools/checks/file-exists.py work/eco-log.csv
    on_fail: retry
    next: [wo]
  - id: wo
    needs: [eco]
    produces: wos
    produce_path: work/work-orders.csv
    tool: docs/tools/wo-export.md
    check: python docs/tools/checks/csv-has-columns.py work/work-orders.csv wo item qty
    on_fail: retry
    next: [dwg]
  - id: dwg
    needs: [eco, wos]
    produces: drawings
    produce_path: work/drawing-index.csv
    tool: docs/tools/drawing-index.md
    check: python docs/tools/checks/file-exists.py work/drawing-index.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [eco, wos, drawings]
    produces: eco-pack
    produce_path: out/eco-pending.md
    tool: docs/tools/eco-log.md
    check: python docs/tools/checks/file-exists.py out/eco-pending.md
    on_fail: retry
    next: []
```
