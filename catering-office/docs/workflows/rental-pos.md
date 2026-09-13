# Rental PO pack

List open rental POs against events: item, qty, deliver window, return window. Flag missing return times, address holes, and POs that fight house equipment already covering the same count. Do not invent a SKU or a price. Do not pay the vendor. Venue vendors on a saved BEO stay labeled venue. Write-up is a completeness pack, not a catalog. They order. You list fights.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: rental-pos
steps:
  - id: pos
    needs: []
    produces: pos
    produce_path: work/rental-pos.csv
    tool: docs/tools/rental-po.md
    check: python docs/tools/checks/csv-has-columns.py work/rental-pos.csv event item
    on_fail: retry
    next: [events]
  - id: events
    needs: [pos]
    produces: events
    produce_path: work/rental-events.csv
    tool: docs/tools/event-order-pdf.md
    check: python docs/tools/checks/csv-has-columns.py work/rental-events.csv event date
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [pos, events]
    produces: rental-pack
    produce_path: out/rental-pos.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/rental-pos.md
    on_fail: retry
    next: []
```
