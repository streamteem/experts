# Wire-fraud checklist (their process)

From their document index and working sheet, list whether their written wire-fraud or callback checklist rows are marked as they marked them. Do not send a wire. Do not republish wiring instructions or account numbers. Do not move funds. FBI and FTC pages are orientation only. Write-up is present-missing of their process rows, not a new instruction set. They verify. You list.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: wire-fraud-checklist-their-process
steps:
  - id: index
    needs: []
    produces: index
    produce_path: work/document-index.csv
    tool: docs/tools/document-folder-index.md
    check: python docs/tools/checks/csv-has-columns.py work/document-index.csv loan document
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [index]
    produces: wire-pack
    produce_path: out/wire-fraud-checklist.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/wire-fraud-checklist.md
    on_fail: retry
    next: []
```
