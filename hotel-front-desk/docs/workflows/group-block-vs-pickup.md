# Group block versus pickup

Compare contracted block rooms to pickup on their group sheet and the arrivals export. List remaining, cutoff, and wash only as written. Blank cutoff is an ask. Do not invent a group rate or release rooms. Rooming-list names must already be on their file. Attach a BEO note only if they dropped one. They cut or wash. You deliver the comparison and write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: group-block-vs-pickup
steps:
  - id: block
    needs: []
    produces: block
    produce_path: work/group-block.csv
    tool: docs/tools/group-block-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/group-block.csv group pickup
    on_fail: retry
    next: [arr]
  - id: arr
    needs: [block]
    produces: arrivals
    produce_path: work/arrivals.csv
    tool: docs/tools/arrivals-csv.md
    check: python docs/tools/checks/file-exists.py work/arrivals.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [block, arrivals]
    produces: group-pack
    produce_path: out/group-block-vs-pickup.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/group-block-vs-pickup.md
    on_fail: retry
    next: []
```
