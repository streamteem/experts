# Title routing

Index the title folder: commitment, updates, invoices, and related PDFs. Route names and dates. Do not clear exceptions. Do not hold money. Do not republish wire instructions. Do not give a title opinion. This is loan-file routing, not the real-estate transaction coordinator’s objection calendar. Draft stamps stay draft. Missing commitment stays missing. Write-up is a routing list plus missing schedules they named.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: title-routing
steps:
  - id: title
    needs: []
    produces: title
    produce_path: work/title-index.csv
    tool: docs/tools/title-folder.md
    check: python docs/tools/checks/csv-has-columns.py work/title-index.csv loan document
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [title]
    produces: title-pack
    produce_path: out/title-routing.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/title-routing.md
    on_fail: retry
    next: []
```
