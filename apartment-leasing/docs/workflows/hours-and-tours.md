# Hours file plus tour calendar

Read the hours or holiday PDF they dropped and the showing calendar, then list tours that fit posted hours and flag any booked outside those hours. Do not invent Sunday or holiday open. After-hours leads are not same-night tours unless their after-hours note says so. If the PDF and a website screenshot disagree, quote both and ask. They change posted hours. You do not open the door.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: hours-and-tours
steps:
  - id: hours
    needs: []
    produces: hours
    produce_path: work/hours.pdf
    tool: docs/tools/community-policy-pdf.md
    check: python docs/tools/checks/file-exists.py work/hours.pdf
    on_fail: retry
    next: [calendar]
  - id: calendar
    needs: [hours]
    produces: calendar
    produce_path: work/tour-calendar.csv
    tool: docs/tools/showing-calendar.md
    check: python docs/tools/checks/csv-has-columns.py work/tour-calendar.csv date unit
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [hours, calendar]
    produces: hours-pack
    produce_path: out/hours-and-tours.md
    tool: docs/tools/showing-calendar.md
    check: python docs/tools/checks/file-exists.py out/hours-and-tours.md
    on_fail: retry
    next: []
```
