# Device count pack

Count devices from their bait-station map and match tickets or scan notes they stored. Quote map versus scan when they disagree; do not invent a station. Missing or damaged devices they coded stay visible. Photos are not a count. Interior versus exterior stays split if they split it. They replace devices. You write the count table and a write-up. Gate codes stay out.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: device-count
steps:
  - id: maps
    needs: []
    produces: maps
    produce_path: work/device-map-index.csv
    tool: docs/tools/bait-map-pdf.md
    check: python docs/tools/checks/file-exists.py work/device-map-index.csv
    on_fail: retry
    next: [tickets]
  - id: tickets
    needs: [maps]
    produces: tickets
    produce_path: work/device-tickets.csv
    tool: docs/tools/ticket-sheet.md
    check: python docs/tools/checks/file-exists.py work/device-tickets.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [maps, tickets]
    produces: device-pack
    produce_path: out/device-count.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/device-count.md
    on_fail: retry
    next: []
```
