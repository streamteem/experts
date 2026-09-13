# Three-way receiving match

Match PO lines to receiving and to the invoice PDF if present. Name any missing leg instead of calling the pack three-way. List price, quantity, UOM, and freight exceptions using their written tolerance if they have one. Do not mark paid and do not schedule payment. Partials match on received qty, not full PO qty, unless their rule allows billed-not-received. Hand the completed or exceptioned file to AP. They pay.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: match
steps:
  - id: pos
    needs: []
    produces: pos
    produce_path: work/pos.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/csv-has-columns.py work/pos.csv po sku qty
    on_fail: retry
    next: [recv]
  - id: recv
    needs: [pos]
    produces: recv
    produce_path: work/receiving.csv
    tool: docs/tools/receiving.md
    check: python docs/tools/checks/file-exists.py work/receiving.csv
    on_fail: retry
    next: [inv]
  - id: inv
    needs: [recv]
    produces: inv
    produce_path: work/invoice.pdf
    tool: docs/tools/invoice-pdf.md
    check: python docs/tools/checks/file-exists.py work/invoice.pdf
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [pos, recv, inv]
    produces: match-pack
    produce_path: out/match.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/match.md
    on_fail: retry
    next: []
```
