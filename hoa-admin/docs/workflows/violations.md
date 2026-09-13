# Open violations

From their log or export, list open items, lots, categories they use, status against their adopted notice steps, and missing photos or blank lots. Produce the CSV the checks can see, then a write-up. No legal finding that a lot is in violation. Do not skip a logged step or mail as counsel. One association per list unless they asked to combine and each row names the community.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: violations
steps:
  - id: pull
    needs: []
    produces: viol-raw
    produce_path: work/violations.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py work/violations.csv
    on_fail: retry
    next: [columns]
  - id: columns
    needs: [viol-raw]
    produces: viol-cols
    produce_path: work/violations.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/csv-has-columns.py work/violations.csv lot status
    on_fail: retry
    next: [write]
  - id: write
    needs: [viol-cols]
    produces: viol-writeup
    produce_path: out/violations.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/violations.md
    on_fail: retry
    next: []
```
