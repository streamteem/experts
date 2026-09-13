# Estimate from their rate file

Draft the estimate from their rate file plus the inventory they stored. Copy extras only when the survey already names them. Leave weight and cube blank unless a scale ticket or their sheet already has a number — never invent either. Binding type stays as their file or an ask. Fuel comes only from their memo. They send the estimate. You write the draft and the questions the check can see.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: estimate-from-rate-file
steps:
  - id: rate
    needs: []
    produces: rate
    produce_path: work/rate-file.csv
    tool: docs/tools/rate-file.md
    check: python docs/tools/checks/file-exists.py work/rate-file.csv
    on_fail: retry
    next: [inv]
  - id: inv
    needs: [rate]
    produces: inv
    produce_path: work/inventory.csv
    tool: docs/tools/inventory-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/inventory.csv job item qty
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [rate, inv]
    produces: estimate-pack
    produce_path: out/estimate-draft.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/estimate-draft.md
    on_fail: retry
    next: []
```
