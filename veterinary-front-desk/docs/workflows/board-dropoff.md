# Boarding and drop-off checklist

From their form, list pickup time, feeding as written, and missing signatures. Not medical advice. Copy belongings, emergency contacts, and authorized pickup names. Medication lines stay exact; do not convert units or add a drug. Surgery packets and daycare packets may differ; use the one they handed you. Unreadable writing is a question. Starter / guess until they teach who reviews the packet before kennel.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: board-dropoff
steps:
  - id: list
    needs: []
    produces: board-raw
    produce_path: work/boarding.csv
    tool: docs/tools/boarding-form.md
    check: python docs/tools/checks/file-exists.py work/boarding.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [board-raw]
    produces: board-writeup
    produce_path: out/boarding.md
    tool: docs/tools/boarding-form.md
    check: python docs/tools/checks/file-exists.py out/boarding.md
    on_fail: retry
    next: []
```
