# Traveler completeness pack

Check traveler PDFs against the work-order export and the drawing index. Flag missing operations, revision mismatches, missing outside rows, and unsigned boxes as completeness only. Do not sign a box. Do not invent a missing operation. Do not treat the newest drawing as released. First-article and cert flags stay as their form printed them. They reprint; you list gaps. Outside-process rows that the job has and the PDF lacks stay on the exception list. They reprint; you do not rebuild a traveler from memory.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: traveler-completeness
steps:
  - id: wo
    needs: []
    produces: wos
    produce_path: work/work-orders.csv
    tool: docs/tools/wo-export.md
    check: python docs/tools/checks/csv-has-columns.py work/work-orders.csv wo item qty
    on_fail: retry
    next: [pdf]
  - id: pdf
    needs: [wos]
    produces: travelers
    produce_path: work/travelers-index.csv
    tool: docs/tools/traveler-pdf.md
    check: python docs/tools/checks/file-exists.py work/travelers-index.csv
    on_fail: retry
    next: [dwg]
  - id: dwg
    needs: [wos, travelers]
    produces: drawings
    produce_path: work/drawing-index.csv
    tool: docs/tools/drawing-index.md
    check: python docs/tools/checks/file-exists.py work/drawing-index.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [wos, travelers, drawings]
    produces: traveler-pack
    produce_path: out/traveler-completeness.md
    tool: docs/tools/traveler-pdf.md
    check: python docs/tools/checks/file-exists.py out/traveler-completeness.md
    on_fail: retry
    next: []
```
