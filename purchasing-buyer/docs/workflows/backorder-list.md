# Backorder and late-line list

Build a list of open lines past need-by, plus vendor backorder notes from the latest PDF or acknowledgment. Promise dates only from that file — not from hope or a remembered lead time. They contact the vendor unless they asked you only to list. Do not overwrite need-by with a late promise. Do not zero remaining qty. Infeasible original need-by stays flagged if the PDF never supported it. Cancel or close-short is their decision.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: backorder-list
steps:
  - id: pos
    needs: []
    produces: pos
    produce_path: work/pos.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/csv-has-columns.py work/pos.csv po sku qty
    on_fail: retry
    next: [pdf]
  - id: pdf
    needs: [pos]
    produces: notes
    produce_path: work/vendor-notes.csv
    tool: docs/tools/vendor-pdf.md
    check: python docs/tools/checks/file-exists.py work/vendor-notes.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [pos, notes]
    produces: late-pack
    produce_path: out/backorders.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/backorders.md
    on_fail: retry
    next: []
```
