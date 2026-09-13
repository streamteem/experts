# Punch list pack

One job. Room, item, owner, and done come from their sheet only. Do not close an item from a photo caption or invent rooms. Keep owner punch and contractor pre-punch on the lists they named if both exist. Reopened items stay open until they mark them. Their columns win, including informal cards they asked you to type. The pack quotes status words from the sheet the check can see and leaves missing owners as questions rather than assignments you make.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: punch-list
steps:
  - id: items
    needs: []
    produces: punch-raw
    produce_path: work/punch.csv
    tool: docs/tools/punch-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/punch.csv room item
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [punch-raw]
    produces: punch-pack
    produce_path: out/punch.md
    tool: docs/tools/punch-sheet.md
    check: python docs/tools/checks/file-exists.py out/punch.md
    on_fail: retry
    next: []
```
