# Records-out request log

Log client or clinic requests and whether an authorization file is present. Do not interpret the chart. Do not invent a hold policy. Their written policy and the veterinarian decide releases and any balance questions. Record destination, date, method, and what was sent when they tell you. Minimum data in the write-up: requestor, patient ID, file names. Starter / guess until they teach who approves a release.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: records-out
steps:
  - id: log
    needs: []
    produces: rec-out
    produce_path: work/records-out.csv
    tool: docs/tools/records-pdf.md
    check: python docs/tools/checks/file-exists.py work/records-out.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [rec-out]
    produces: rec-out-writeup
    produce_path: out/records-out.md
    tool: docs/tools/records-pdf.md
    check: python docs/tools/checks/file-exists.py out/records-out.md
    on_fail: retry
    next: []
```
