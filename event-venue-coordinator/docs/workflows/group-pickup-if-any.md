# Group pickup (if any)

If they have a sleeping-room block file, list contracted rooms, pickup, remaining, printed rate, and room cutoff. If the file is empty, say no block — do not invent one. Do not invent pickup or a group rate. Do not wash rooms. Banquet minimum stays on banquet files. They manage the hotel system. You deliver the pickup list plus write-up when a block exists.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: group-pickup-if-any
steps:
  - id: block
    needs: []
    produces: block
    produce_path: work/group-block.csv
    tool: docs/tools/group-block-if-any.md
    check: python docs/tools/checks/file-exists.py work/group-block.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [block]
    produces: pickup-pack
    produce_path: out/group-pickup.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/group-pickup.md
    on_fail: retry
    next: []
```
