# Holiday and closure pack

Copy the year’s closures, staff-only days, and tuition-charged holidays from their calendar file and quote the handbook exhibit when the calendar is silent on whether tuition is due. Do not invent a federal-holiday rule. Camp weeks and school-district days off stay labeled if they split those calendars. Confirm the year on the file. They send parent notices unless they taught a send step. If two calendars disagree, quote both. Extra-care does not run on a closed day unless their file says so.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: holiday-calendar-pack
steps:
  - id: cal
    needs: []
    produces: cal
    produce_path: work/calendar.csv
    tool: docs/tools/calendar-file.md
    check: python docs/tools/checks/file-exists.py work/calendar.csv
    on_fail: retry
    next: [handbook]
  - id: handbook
    needs: [cal]
    produces: handbook
    produce_path: work/handbook-notes.csv
    tool: docs/tools/handbook-pdf.md
    check: python docs/tools/checks/file-exists.py work/handbook-notes.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [cal, handbook]
    produces: cal-pack
    produce_path: out/holiday-calendar.md
    tool: docs/tools/calendar-file.md
    check: python docs/tools/checks/file-exists.py out/holiday-calendar.md
    on_fail: retry
    next: []
```
