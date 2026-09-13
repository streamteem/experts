# Asset warranty due

List assets whose warranty-end date on the asset list falls before the pack date they named, or is already past. Do not invent a warranty year. Do not file a claim. If install date and warranty start disagree, quote both on the write-up. Missing warranty-end stays a question. This is in-house OEM or installer coverage on assets they operate, not field-trade customer warranty labor and not a construction closeout warranty log.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: asset-warranty-due
steps:
  - id: assets
    needs: []
    produces: assets
    produce_path: work/asset-list.csv
    tool: docs/tools/asset-list.md
    check: python docs/tools/checks/csv-has-columns.py work/asset-list.csv asset warranty-end
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [assets]
    produces: warranty-pack
    produce_path: out/asset-warranty-due.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/asset-warranty-due.md
    on_fail: retry
    next: []
```
