# Recall list file

Build or clean a recall CSV from their export for them to send. You do not message patients. Keep their due dates and type labels; do not fill a generic six-month date if the column is missing. You do not say the patient is clinically due and you do not pick a CDT code. Respect hours and holiday files. Prefer chart number. Extra phones the task does not need stay out of the write-up. One location unless they asked.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: recall-list
steps:
  - id: pull
    needs: []
    produces: recall-raw
    produce_path: work/recall.csv
    tool: docs/tools/recall-csv.md
    check: python docs/tools/checks/file-exists.py work/recall.csv
    on_fail: retry
    next: [columns]
  - id: columns
    needs: [recall-raw]
    produces: recall-cols
    produce_path: work/recall.csv
    tool: docs/tools/recall-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/recall.csv due
    on_fail: retry
    next: [write]
  - id: write
    needs: [recall-cols]
    produces: recall-writeup
    produce_path: out/recall-list.md
    tool: docs/tools/recall-csv.md
    check: python docs/tools/checks/file-exists.py out/recall-list.md
    on_fail: retry
    next: []
```
