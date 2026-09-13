# Route day list

Build a day list from their route CSV and tickets: tech, account, service, window, pet, child, dog, and skip flags. Apply the skip list first. Do not invent a ticket, a target pest, a mix, or a license stamp. Wind stays on the board until they write a hold. One account per row. They dispatch. You write the list and a short write-up. Gate codes stay out of the pack.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: route-day
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
    produce_path: work/tickets.csv
    tool: docs/tools/ticket-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/tickets.csv ticket account
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [route, tickets]
    produces: route-day-pack
    produce_path: out/route-day.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/route-day.md
    on_fail: retry
    next: []
```
