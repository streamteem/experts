# Walk-in count pack

Transcribe or check their count sheet, including the shelf map if they filed one. Missing rows stay missing. Units stay as printed. Do not fill blanks from sales, last week, or a POS theoretical. Partial counts stay labeled partial. Use the open or close timestamp they wrote and ask which count feeds the order. Do not average two counts. You do not rearrange the box in the write-up. This pack is their clipboard, not a guessed walk-in.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: count-walk-in
steps:
  - id: pull
    needs: []
    produces: count-raw
    produce_path: work/walkin-count.csv
    tool: docs/tools/count-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/walkin-count.csv item qty
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [count-raw]
    produces: count-pack
    produce_path: out/count.md
    tool: docs/tools/count-sheet.md
    check: python docs/tools/checks/file-exists.py out/count.md
    on_fail: retry
    next: []
```
