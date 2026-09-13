# Incoming records routing log

Log received PDFs. Do not interpret labs or films. Assign only as their routing sheet says. Record received date, source, patient label, filename, and page count if they care. Missing identity is a question before attach. Do not paste result tables into the write-up. Critical-call flags interrupt only when their protocol says so. Starter / guess until they teach default doctors and folder names.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: records-in
steps:
  - id: index
    needs: []
    produces: rec-in
    produce_path: work/records-in.csv
    tool: docs/tools/records-pdf.md
    check: python docs/tools/checks/file-exists.py work/records-in.csv
    on_fail: retry
    next: [columns]
  - id: columns
    needs: [rec-in]
    produces: rec-cols
    produce_path: work/records-in.csv
    tool: docs/tools/records-pdf.md
    check: python docs/tools/checks/csv-has-columns.py work/records-in.csv file received
    on_fail: retry
    next: [write]
  - id: write
    needs: [rec-cols]
    produces: rec-writeup
    produce_path: out/records-in.md
    tool: docs/tools/records-pdf.md
    check: python docs/tools/checks/file-exists.py out/records-in.md
    on_fail: retry
    next: []
```
