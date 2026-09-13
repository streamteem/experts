# High-value list check

Check whether their high-value form is present when their rule or estimate PDF says it is required. List blank description or value fields they left open. Do not invent an article or a dollar. Valuation on the main form is not a substitute if they split the papers. They collect the list. You write present-or-missing plus the write-up. Claims still route; you do not decide coverage.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: high-value-list-check
steps:
  - id: inv
    needs: []
    produces: inv
    produce_path: work/inventory.csv
    tool: docs/tools/inventory-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/inventory.csv job item qty
    on_fail: retry
    next: [est]
  - id: est
    needs: [inv]
    produces: est
    produce_path: work/estimate.pdf
    tool: docs/tools/estimate-pdf.md
    check: python docs/tools/checks/file-exists.py work/estimate.pdf
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [inv, est]
    produces: hvl-pack
    produce_path: out/high-value-check.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/high-value-check.md
    on_fail: retry
    next: []
```
