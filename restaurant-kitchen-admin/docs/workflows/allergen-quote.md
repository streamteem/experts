# Allergen quote from their file

Quote contains, may-contain, and same-kitchen phrases from their matrix for the items they name. No invented legal status, no gluten-free or safe-for stamp, no guest medical advice. If the matrix is missing or two files disagree, ask which is live. Do not fill sesame or other allergens from a Food Code orientation page. Guest questions go to the manager or chef. Copy phrases exactly. This pack is a quote sheet, not an inspection and not a new procedure.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: allergen-quote
steps:
  - id: pull
    needs: []
    produces: alg-raw
    produce_path: work/allergen-items.csv
    tool: docs/tools/allergen-file.md
    check: python docs/tools/checks/csv-has-columns.py work/allergen-items.csv item status
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [alg-raw]
    produces: alg-pack
    produce_path: out/allergen-quote.md
    tool: docs/tools/allergen-file.md
    check: python docs/tools/checks/file-exists.py out/allergen-quote.md
    on_fail: retry
    next: []
```
