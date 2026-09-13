# Skip list pack

Apply their skip rows to the route CSV. Skips win. Do not invent a skip to hide a miss. Do not send a skipped account to fill the day. Lift dates come from their note. Wind holds stay a separate label unless they merged lists. One account per row. They add or lift skips. You write the leftover live stops and the skipped set plus a write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: skip-list
steps:
  - id: route
    needs: []
    produces: route
    produce_path: work/route.csv
    tool: docs/tools/route-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/route.csv route account
    on_fail: retry
    next: [tickets]
  - id: tickets
    needs: [route]
    produces: tickets
    produce_path: work/skip-tickets.csv
    tool: docs/tools/ticket-sheet.md
    check: python docs/tools/checks/file-exists.py work/skip-tickets.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [route, tickets]
    produces: skip-pack
    produce_path: out/skip-list.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/skip-list.md
    on_fail: retry
    next: []
```
