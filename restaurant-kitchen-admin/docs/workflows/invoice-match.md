# Invoice match

Match the vendor invoice to the order and to receiving notes if they have them. Shorts, substitutions, price jumps off bid, wrong spec, and catch-weight gaps are questions. No payment, no invented credit amount, no silent price change on the guide. Do not call a two-way file a three-way match. Keep account secrets out of the folder. One pack is one ticket unless they asked to index a week. Alcohol lines still do not get license advice.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: invoice-match
steps:
  - id: inv
    needs: []
    produces: inv-raw
    produce_path: work/invoice-lines.csv
    tool: docs/tools/invoice-pdf.md
    check: python docs/tools/checks/csv-has-columns.py work/invoice-lines.csv item qty price
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [inv-raw]
    produces: match-pack
    produce_path: out/invoice-match.md
    tool: docs/tools/receiving-log.md
    check: python docs/tools/checks/file-exists.py out/invoice-match.md
    on_fail: retry
    next: []
```
