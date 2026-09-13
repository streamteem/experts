# Crew day list

Build a day list from their roster and tickets: crew, property, service, window, dog and skip flags. Apply the skip list first. Do not assign down equipment. Do not invent hours, wages, or a missing ticket. Weather stays on the board until they call a postpone. One property per row. They dispatch. You write the list and a short write-up. Gate codes stay out of the pack.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: crew-day
steps:
  - id: roster
    needs: []
    produces: roster
    produce_path: work/crew-roster.csv
    tool: docs/tools/crew-roster.md
    check: python docs/tools/checks/csv-has-columns.py work/crew-roster.csv crew name
    on_fail: retry
    next: [tickets]
  - id: tickets
    needs: [roster]
    produces: tickets
    produce_path: work/tickets.csv
    tool: docs/tools/job-ticket-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/tickets.csv ticket property service
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [roster, tickets]
    produces: crew-day-pack
    produce_path: out/crew-day.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/crew-day.md
    on_fail: retry
    next: []
```
