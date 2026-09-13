# Specials against availability

Read the dated specials sheet and the availability export, then list which open floorplans still match a live offer. Do not invent a concession. Expired specials stay expired. Do not attach a special to a held or down unit unless their sheet says it applies. Posted rent on availability is not a new special. They change promotions; you match files.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: specials-from-file
steps:
  - id: specials
    needs: []
    produces: specials
    produce_path: work/specials.csv
    tool: docs/tools/specials-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/specials.csv floorplan offer
    on_fail: retry
    next: [avail]
  - id: avail
    needs: [specials]
    produces: avail
    produce_path: work/availability.csv
    tool: docs/tools/availability-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/availability.csv unit status
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [specials, avail]
    produces: specials-pack
    produce_path: out/specials.md
    tool: docs/tools/specials-sheet.md
    check: python docs/tools/checks/file-exists.py out/specials.md
    on_fail: retry
    next: []
```
