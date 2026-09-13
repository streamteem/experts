# Suspense list as their codes

List suspense and rereq items from their conditions sheet using their codes and comments only. Do not translate a code into a denial or an easy fix. Do not unsuspend. Do not invent a reason. Do not approve. Do not invent a rate to “fix” suspense. Write-up is their status plus dated evidence rows, not a prognosis and not a fair-lending opinion.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: suspense-list-as-their-codes
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
    produces: suspense-pack
    produce_path: out/suspense-list.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/suspense-list.md
    on_fail: retry
    next: []
```
