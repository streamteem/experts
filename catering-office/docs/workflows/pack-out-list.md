# Pack-out list

Build a pack-out from the event order, house equipment list, and their pack-out sheet: food lines from the menu file and guarantee, chafers, linens, china, coolers, ice, and labels. Drop-off versus full-service must match the order. Shortages versus house on-hand stay visible. Do not invent a piece or a yield. Do not borrow venue kit unless a saved BEO they filed says the hall provides it. Write-up lists holes and asks. They load the van.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: pack-out-list
steps:
  - id: order
    needs: []
    produces: order
    produce_path: work/pack-event.csv
    tool: docs/tools/event-order-pdf.md
    check: python docs/tools/checks/csv-has-columns.py work/pack-event.csv event date
    on_fail: retry
    next: [equip]
  - id: equip
    needs: [order]
    produces: equipment
    produce_path: work/pack-equipment.csv
    tool: docs/tools/equipment-list.md
    check: python docs/tools/checks/csv-has-columns.py work/pack-equipment.csv item qty
    on_fail: retry
    next: [sheet]
  - id: sheet
    needs: [order, equipment]
    produces: packout
    produce_path: work/pack-out.csv
    tool: docs/tools/pack-out-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/pack-out.csv event item
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [order, equipment, packout]
    produces: pack-out-pack
    produce_path: out/pack-out-list.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/pack-out-list.md
    on_fail: retry
    next: []
```
