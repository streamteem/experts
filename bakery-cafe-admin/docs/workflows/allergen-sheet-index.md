# Allergen sheet index

Index their allergen sheet against formula or bake-list names: missing rows, two-sheet fights, blank sesame or nut cells. Quote contains and may-contain exactly. Do not invent status. Do not write gluten-free as a legal claim. Do not advise a guest. FDA pages stay orientation. Write-up is the hole list. They own the live matrix. Blank cells stay blank. They own the live matrix; you index holes.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: allergen-sheet-index
steps:
  - id: sheet
    needs: []
    produces: allergens
    produce_path: work/allergen-sheet.csv
    tool: docs/tools/allergen-sheet.md
    check: python docs/tools/checks/file-exists.py work/allergen-sheet.csv
    on_fail: retry
    next: [formulas]
  - id: formulas
    needs: [allergens]
    produces: formulas
    produce_path: work/formula-index.csv
    tool: docs/tools/formula-file.md
    check: python docs/tools/checks/file-exists.py work/formula-index.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [allergens, formulas]
    produces: allergen-pack
    produce_path: out/allergen-sheet-index.md
    tool: docs/tools/allergen-sheet.md
    check: python docs/tools/checks/file-exists.py out/allergen-sheet-index.md
    on_fail: retry
    next: []
```
