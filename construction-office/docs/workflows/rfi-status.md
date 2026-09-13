# RFI status pack

From their RFI export, list open, overdue versus their due column, and returned. Do not answer design questions or pick a detail. Keep their numbers and status words. Flag cost or time only when their log already has that mark; otherwise say unknown and ask. Truncated question text points at the PDF, not a rewrite. Aging is a date compare they can correct, not a claim. The pack quotes the export they dropped and does not invent due dates from a five-day custom.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: rfi-status
steps:
  - id: pull
    needs: []
    produces: rfi-raw
    produce_path: work/rfi-log.csv
    tool: docs/tools/rfi-log.md
    check: python docs/tools/checks/csv-has-columns.py work/rfi-log.csv number status
    on_fail: retry
    next: [age]
  - id: age
    needs: [rfi-raw]
    produces: rfi-aged
    produce_path: work/rfi-aged.csv
    tool: docs/tools/rfi-log.md
    check: python docs/tools/checks/csv-has-columns.py work/rfi-aged.csv number status
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [rfi-aged]
    produces: rfi-pack
    produce_path: out/rfi-status.md
    tool: docs/tools/procore-pattern.md
    check: python docs/tools/checks/file-exists.py out/rfi-status.md
    on_fail: retry
    next: []
```
