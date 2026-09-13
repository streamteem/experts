# I-9 section dates

Build a date list from their I-9 index: name, start date from their hire file if present, Section 1 date, Section 2 date, and reverify date if they track one. Blank stays blank and becomes an ask. Do not invent dates from a remembered timing rule. Do not choose documents. Do not copy SSN or ID images. If start date and a section date look out of order, list both and ask. Write-up is completeness only, not an immigration opinion.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: i9-section-dates
steps:
  - id: index
    needs: []
    produces: i9idx
    produce_path: work/i9-index.csv
    tool: docs/tools/i9-folder-index.md
    check: python docs/tools/checks/csv-has-columns.py work/i9-index.csv name
    on_fail: retry
    next: [roster]
  - id: roster
    needs: [i9idx]
    produces: roster
    produce_path: work/roster.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py work/roster.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [i9idx, roster]
    produces: i9-pack
    produce_path: out/i9-section-dates.md
    tool: docs/tools/i9-folder-index.md
    check: python docs/tools/checks/file-exists.py out/i9-section-dates.md
    on_fail: retry
    next: []
```
