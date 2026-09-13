# Supply reorder flags from their min

Compare on-hand to their par or min on the supply par sheet. Flag at or below their min. Do not invent a min, a brand, or a case count. Do not place an order. Chemical rows stay names from their sheet; mixes stay out. One SKU and closet per row. Write-up is the below-par list plus blank-min asks. They buy. You pack the flags the check can see.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: supply-below-par
steps:
  - id: pars
    needs: []
    produces: pars
    produce_path: work/supply-par.csv
    tool: docs/tools/supply-par-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/supply-par.csv sku min
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [pars]
    produces: below-par-pack
    produce_path: out/supply-below-par.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/supply-below-par.md
    on_fail: retry
    next: []
```
