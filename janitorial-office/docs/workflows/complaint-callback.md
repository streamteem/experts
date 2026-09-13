# Complaint and callback list

List open complaints from their log and attach named photos if present. Do not invent a callback, a credit, or a chemical cause. Courtesy versus billable follows their file; billable still needs extra-work-auth when they say so. One complaint per row. They call the customer. You write the list and questions, not an apology as if you were the owner.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: complaint-callback
steps:
  - id: log
    needs: []
    produces: log
    produce_path: work/complaint-log.csv
    tool: docs/tools/complaint-log.md
    check: python docs/tools/checks/csv-has-columns.py work/complaint-log.csv site date
    on_fail: retry
    next: [photos]
  - id: photos
    needs: [log]
    produces: photos
    produce_path: work/callback-photos.csv
    tool: docs/tools/photo-folder.md
    check: python docs/tools/checks/file-exists.py work/callback-photos.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [log, photos]
    produces: callback-pack
    produce_path: out/callbacks.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/callbacks.md
    on_fail: retry
    next: []
```
