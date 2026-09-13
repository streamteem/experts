# Departures and due-outs

List due-outs and planned departures from the in-house export and room status. Late-checkout asks stay asks. Unsettled folios are exceptions, not skippers unless they coded skipper. Do not invent a late fee. A due-out who extended must follow their export, not hope. They check guests out. You deliver the due-out list and write-up. Express-checkout flags stay as coded. Do not email a folio that shows PAN. Bags-in-room notes they wrote stay on the row. They settle tenders.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: departures-due-out
steps:
  - id: inh
    needs: []
    produces: inhouse
    produce_path: work/in-house.csv
    tool: docs/tools/in-house-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/in-house.csv room departure
    on_fail: retry
    next: [status]
  - id: status
    needs: [inhouse]
    produces: status
    produce_path: work/room-status.csv
    tool: docs/tools/room-status-sheet.md
    check: python docs/tools/checks/file-exists.py work/room-status.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [inhouse, status]
    produces: dept-pack
    produce_path: out/departures-due-out.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/departures-due-out.md
    on_fail: retry
    next: []
```
