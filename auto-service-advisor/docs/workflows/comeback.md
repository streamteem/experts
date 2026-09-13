# Comeback flag

Match today's concern to a prior RO in their history export. Flag at the top with the prior number from the file. No invented failure of the last repair and no warranty coverage opinion. Keep today's customer words. If the wording is only close, ask. Independent local history and dealer history screens both work when they saved the export. Do not bury the flag under an oil-change line. Policy amounts appear only if a manager already wrote them. Missing history is a question, not a story from chat.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: comeback
steps:
  - id: hist
    needs: []
    produces: hist-raw
    produce_path: work/history.csv
    tool: docs/tools/shop-sw.md
    check: python docs/tools/checks/csv-has-columns.py work/history.csv ro date concern
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [hist-raw]
    produces: comeback-pack
    produce_path: out/comeback.md
    tool: docs/tools/shop-sw.md
    check: python docs/tools/checks/file-exists.py out/comeback.md
    on_fail: retry
    next: []
```
