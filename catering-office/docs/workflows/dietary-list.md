# Dietary list

Build a per-event dietary list from their dietary sheet, the event order, and the allergen file: counts as they labeled them and flags routed to sheet rows. Do not invent a substitute dish. Do not treat a guest. Do not stamp a plate safe. Math that exceeds the guarantee stays flagged. Missing allergen-sheet rows for a flagged dish are asks. Write-up uses their words. They decide the plate. You route.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: dietary-list
steps:
  - id: diet
    needs: []
    produces: dietary
    produce_path: work/dietary.csv
    tool: docs/tools/dietary-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/dietary.csv event note
    on_fail: retry
    next: [allergen]
  - id: allergen
    needs: [dietary]
    produces: allergens
    produce_path: work/allergen-rows.csv
    tool: docs/tools/allergen-file.md
    check: python docs/tools/checks/file-exists.py work/allergen-rows.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [dietary, allergens]
    produces: dietary-pack
    produce_path: out/dietary-list.md
    tool: docs/tools/event-order-pdf.md
    check: python docs/tools/checks/file-exists.py out/dietary-list.md
    on_fail: retry
    next: []
```
