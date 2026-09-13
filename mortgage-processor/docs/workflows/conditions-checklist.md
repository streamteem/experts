# Conditions checklist

Build a conditions checklist from their conditions sheet: loan number, condition text, PTD/PTF/suspense as they coded it, and status. Attach present-missing only when the matching document is in the pack. Do not invent a condition. Do not mark cleared without their code. Do not declare CTC. Do not underwrite. Write-up names which rows came from their export versus a guess you labeled.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: conditions-checklist
steps:
  - id: sheet
    needs: []
    produces: conditions
    produce_path: work/conditions.csv
    tool: docs/tools/conditions-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/conditions.csv loan condition
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [conditions]
    produces: checklist
    produce_path: out/conditions-checklist.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/conditions-checklist.md
    on_fail: retry
    next: []
```
