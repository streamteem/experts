# Estimate draft from the price file

Draft estimate lines from their price file and the lead or ticket they stored. Quantity they listed times unit price they listed. Blank price or blank qty: ask. Do not invent a mix, an EPA number, or a monthly rate. Do not promise eradication. Label the pack draft until they accept. They send the proposal. You do not treat the draft as sold work on a route day.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: estimate-from-price
steps:
  - id: price
    needs: []
    produces: price
    produce_path: work/price-file.csv
    tool: docs/tools/price-file.md
    check: python docs/tools/checks/csv-has-columns.py work/price-file.csv item price
    on_fail: retry
    next: [tickets]
  - id: tickets
    needs: [price]
    produces: tickets
    produce_path: work/estimate-tickets.csv
    tool: docs/tools/ticket-sheet.md
    check: python docs/tools/checks/file-exists.py work/estimate-tickets.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [price, tickets]
    produces: estimate-pack
    produce_path: out/estimate.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/estimate.md
    on_fail: retry
    next: []
```
