# Route pack

Pull the route CSV and match each stop to a ticket. Keep their sequence. Flag skips, missing tickets, missing access, and time windows. Do not invent a better order or a ghost stop. Commercial PO flags stay visible if their file requires a PO. One property per row. They may reorder. You pack the file and write-up for the trucks they already named.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: route-pack
steps:
  - id: route
    needs: []
    produces: route
    produce_path: work/route.csv
    tool: docs/tools/route-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/route.csv route property
    on_fail: retry
    next: [tickets]
  - id: tickets
    needs: [route]
    produces: tickets
    produce_path: work/route-tickets.csv
    tool: docs/tools/job-ticket-sheet.md
    check: python docs/tools/checks/file-exists.py work/route-tickets.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [route, tickets]
    produces: route-pack
    produce_path: out/route-pack.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/route-pack.md
    on_fail: retry
    next: []
```
