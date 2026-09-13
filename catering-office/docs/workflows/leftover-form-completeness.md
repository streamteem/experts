# Leftover-form completeness

For events whose leftover policy requires a signed release, list form present or missing from the leftover-form folder against the event-order list. Do not invent legal text. Do not stamp leftovers safe. Drop-off jobs follow their policy file, which may not require a form. Write-up is a completeness list, not a donation finding. They collect signatures. You keep missing forms visible.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: leftover-form-completeness
steps:
  - id: orders
    needs: []
    produces: orders
    produce_path: work/leftover-events.csv
    tool: docs/tools/event-order-pdf.md
    check: python docs/tools/checks/csv-has-columns.py work/leftover-events.csv event date
    on_fail: retry
    next: [forms]
  - id: forms
    needs: [orders]
    produces: forms
    produce_path: work/leftover-forms.csv
    tool: docs/tools/leftover-form-folder.md
    check: python docs/tools/checks/file-exists.py work/leftover-forms.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [orders, forms]
    produces: leftover-pack
    produce_path: out/leftover-form-completeness.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/leftover-form-completeness.md
    on_fail: retry
    next: []
```
