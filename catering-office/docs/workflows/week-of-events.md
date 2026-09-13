# Week-of events board

Build a week board from their event-order export and calendar: event, date, venue as address, style, guarantee or expected labeled as such, delivery window, and vehicle if the calendar has one. Flag missing guarantees that are past cutoff, missing windows, and van overlaps. Do not invent a date or a room. Do not treat a saved venue BEO as the hall's hold board. Write-up names which columns came from the order versus a guess you labeled. They run the week; you do not bump jobs.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: week-of-events
steps:
  - id: orders
    needs: []
    produces: orders
    produce_path: work/event-orders.csv
    tool: docs/tools/event-order-pdf.md
    check: python docs/tools/checks/csv-has-columns.py work/event-orders.csv event date venue
    on_fail: retry
    next: [cal]
  - id: cal
    needs: [orders]
    produces: calendar
    produce_path: work/week-calendar.csv
    tool: docs/tools/calendar.md
    check: python docs/tools/checks/csv-has-columns.py work/week-calendar.csv event date
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [orders, calendar]
    produces: week-board
    produce_path: out/week-of-events.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/week-of-events.md
    on_fail: retry
    next: []
```
