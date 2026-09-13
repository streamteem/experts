# Open POs

List open purchase orders and need-by dates from their sheet or export. Flag lines past need-by. Prices on the list must already be on the PO or the quote file they saved — do not fill blanks and do not guess freight. Keep draft versus issued as they coded it. Promise dates, if shown, come only from a vendor PDF already in the folder. Remaining qty after partials follows their receiving file, not hope. They use the list; you do not send it to vendors as a live order.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: open-pos
steps:
  - id: pull
    needs: []
    produces: pos
    produce_path: work/pos.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/csv-has-columns.py work/pos.csv po sku qty
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [pos]
    produces: po-pack
    produce_path: out/open-pos.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/open-pos.md
    on_fail: retry
    next: []
```
