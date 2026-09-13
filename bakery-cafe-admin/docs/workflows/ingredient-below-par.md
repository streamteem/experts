# Ingredients below par

Compare ingredient par-min to counted on-hand or receiving on-hand for flour, butter, dairy, and other lines they named. Suggested order qty only when par and count both exist. Do not invent a par, a bag count, or a vendor minimum filler. Receiving shorts stay visible. Do not pay. Write-up is the below-par list. They order. No filler SKUs for a vendor minimum. They order; you list the hole.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: ingredient-below-par
steps:
  - id: pars
    needs: []
    produces: ing-par
    produce_path: work/ingredient-par.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/csv-has-columns.py work/ingredient-par.csv item par
    on_fail: retry
    next: [recv]
  - id: recv
    needs: [ing-par]
    produces: recv
    produce_path: work/receiving.csv
    tool: docs/tools/receiving-csv.md
    check: python docs/tools/checks/file-exists.py work/receiving.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [ing-par, recv]
    produces: ing-pack
    produce_path: out/ingredient-below-par.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/ingredient-below-par.md
    on_fail: retry
    next: []
```
