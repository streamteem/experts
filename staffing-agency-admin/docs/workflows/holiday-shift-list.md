# Holiday shift list

Join the holiday calendar to open assignments and the rate file. List who is scheduled on a holiday or shutdown date they wrote, and quote holiday bill or pay premiums only from the rate file. Do not invent a federal-holiday list. Do not assume the client is closed. If agency and client calendars disagree, quote both and ask who works. Write the list and a write-up. They decide who is sent. You do not invent a premium.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: holiday-shift-list
steps:
  - id: hols
    needs: []
    produces: holidays
    produce_path: work/holidays.csv
    tool: docs/tools/calendar-holidays.md
    check: python docs/tools/checks/csv-has-columns.py work/holidays.csv date
    on_fail: retry
    next: [assign]
  - id: assign
    needs: [holidays]
    produces: assign
    produce_path: work/assignments.csv
    tool: docs/tools/assignment-sheet.md
    check: python docs/tools/checks/file-exists.py work/assignments.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [holidays, assign]
    produces: hol-pack
    produce_path: out/holiday-shifts.md
    tool: docs/tools/rate-file.md
    check: python docs/tools/checks/file-exists.py out/holiday-shifts.md
    on_fail: retry
    next: []
```
