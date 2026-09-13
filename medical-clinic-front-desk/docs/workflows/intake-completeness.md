# Intake completeness

From PDFs they share, list missing pages and signatures as questions. No clinical reading of history answers, allergies, or medications. Registration, history, consents, and privacy-notice acknowledgment are yes or no on named pages. Do not copy a full SSN or the full history into docs/ when a completeness row will do. Guardian signatures for minors are present or missing, not a custody decision. If a required form is not in the folder they named, ask; do not mark complete.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: intake-completeness
steps:
  - id: list
    needs: []
    produces: forms
    produce_path: work/intake-index.csv
    tool: docs/tools/intake-pdf-folder.md
    check: python docs/tools/checks/file-exists.py work/intake-index.csv
    on_fail: retry
    next: [columns]
  - id: columns
    needs: [forms]
    produces: forms-cols
    produce_path: work/intake-index.csv
    tool: docs/tools/intake-pdf-folder.md
    check: python docs/tools/checks/csv-has-columns.py work/intake-index.csv form complete
    on_fail: retry
    next: [write]
  - id: write
    needs: [forms-cols]
    produces: forms-writeup
    produce_path: out/intake-missing.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/intake-missing.md
    on_fail: retry
    next: []
```
