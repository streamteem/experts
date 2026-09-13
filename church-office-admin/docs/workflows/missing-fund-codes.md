# Missing fund codes

From the giving export they dropped, list rows with a blank fund or a code not on their chart if they also stored a chart. Do not default a blank to general. Do not invent a fund from a pew note. Quote note versus dropdown when both exist. Write-up is a missing-code list, not a recode and not a tax opinion. They recode. You flag holes.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: missing-fund-codes
steps:
  - id: export
    needs: []
    produces: gifts
    produce_path: work/giving-export.csv
    tool: docs/tools/giving-export.md
    check: python docs/tools/checks/csv-has-columns.py work/giving-export.csv amount fund
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [gifts]
    produces: fund-pack
    produce_path: out/missing-fund-codes.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/missing-fund-codes.md
    on_fail: retry
    next: []
```
