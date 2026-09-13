# Bait-map index

Index bait-station maps they stored to account and ticket. List station ids as written. Do not invent a device or redraw the building as a structural diagnosis. Device-scan exports, if present, stay a later reconcile. Photos named to the map help; they are not a diagnosis. Gate codes stay out of the index. They place stations. You write the index and write-up the check can see.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: bait-map-index
steps:
  - id: maps
    needs: []
    produces: maps
    produce_path: work/bait-map-index.csv
    tool: docs/tools/bait-map-pdf.md
    check: python docs/tools/checks/file-exists.py work/bait-map-index.csv
    on_fail: retry
    next: [tickets]
  - id: tickets
    needs: [maps]
    produces: tickets
    produce_path: work/bait-tickets.csv
    tool: docs/tools/ticket-sheet.md
    check: python docs/tools/checks/file-exists.py work/bait-tickets.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [maps, tickets]
    produces: map-pack
    produce_path: out/bait-map-index.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/bait-map-index.md
    on_fail: retry
    next: []
```
