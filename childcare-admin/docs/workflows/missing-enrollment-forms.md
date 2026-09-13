# Missing enrollment forms

From the enrollment PDF folder, list each named packet page as present, dated, signed, or missing for the children they asked. Do not fill blanks. Do not copy full SSN or extra medical notes into docs/. Guardian signatures are present or missing, not a custody decision. A packet that is almost done is still incomplete. Sibling children are separate rows. Start without a complete packet is their written exception, not your mark.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: missing-enrollment-forms
steps:
  - id: folder
    needs: []
    produces: packets
    produce_path: work/packet-index.csv
    tool: docs/tools/enrollment-pdf-folder.md
    check: python docs/tools/checks/file-exists.py work/packet-index.csv
    on_fail: retry
    next: [grid]
  - id: grid
    needs: [packets]
    produces: grid
    produce_path: work/missing-forms.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/csv-has-columns.py work/missing-forms.csv child form complete
    on_fail: retry
    next: [write]
  - id: write
    needs: [packets, grid]
    produces: forms-pack
    produce_path: out/missing-enrollment-forms.md
    tool: docs/tools/enrollment-pdf-folder.md
    check: python docs/tools/checks/file-exists.py out/missing-enrollment-forms.md
    on_fail: retry
    next: []
```
