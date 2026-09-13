# Fuel outliers as questions

Compare the fuel CSV to units on the roster. Odd gallons, wrong state versus the trip sheet, or unit/driver mismatch are questions, not accusations and not theft findings unless they defined a numeric rule. Do not invent gallons or store full card numbers. IFTA is not filed from this pack. Starter / guess until they teach this shop. Say which columns you compared. Full card numbers stay out. Humans decide what a spike means.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: fuel-outliers
steps:
  - id: fuel
    needs: []
    produces: fuel-raw
    produce_path: work/fuel.csv
    tool: docs/tools/fuel-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/fuel.csv unit gallons
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [fuel-raw]
    produces: fuel-pack
    produce_path: out/fuel-questions.md
    tool: docs/tools/fuel-csv.md
    check: python docs/tools/checks/file-exists.py out/fuel-questions.md
    on_fail: retry
    next: []
```
