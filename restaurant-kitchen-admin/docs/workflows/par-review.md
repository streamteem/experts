# Par review questions

Compare their pars to the recent sales-mix export and to waste rows if those files exist. Do not change pars. List questions only: stale high pars on dead items, low pars that 86 often, weekend versus weekday mismatch. Do not 86 from mix alone. Do not invent a food-cost target. Theoretical usage is not a count. Menu changes stay the chef's. Say the date range on the mix. Starter par talk is not this shop's target until they teach.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: par-review
steps:
  - id: mix
    needs: []
    produces: mix-raw
    produce_path: work/menu-mix.csv
    tool: docs/tools/pos-export.md
    check: python docs/tools/checks/csv-has-columns.py work/menu-mix.csv item qty
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [mix-raw]
    produces: par-pack
    produce_path: out/par-questions.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/par-questions.md
    on_fail: retry
    next: []
```
