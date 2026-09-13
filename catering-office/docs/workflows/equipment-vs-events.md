# Equipment versus events

Compare house equipment on-hand to the same-day event pack-outs: chafers, cambros, urns, china. Flag double-books and shortages. Rentals on a PO are not house on-hand until the PO says they land. Do not invent a piece count. Do not silently assign venue kit. Write-up names the Saturday (or day) and which events collide. They rent or they move a job. You keep the shortage visible.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: equipment-vs-events
steps:
  - id: equip
    needs: []
    produces: equipment
    produce_path: work/house-equipment.csv
    tool: docs/tools/equipment-list.md
    check: python docs/tools/checks/csv-has-columns.py work/house-equipment.csv item qty
    on_fail: retry
    next: [events]
  - id: events
    needs: [equipment]
    produces: events
    produce_path: work/equipment-events.csv
    tool: docs/tools/event-order-pdf.md
    check: python docs/tools/checks/csv-has-columns.py work/equipment-events.csv event date
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [equipment, events]
    produces: equip-pack
    produce_path: out/equipment-vs-events.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/equipment-vs-events.md
    on_fail: retry
    next: []
```
