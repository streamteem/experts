# Date-stamp pack

Build a date-file pack from their calendar and document-folder index: application, VOE as-of, stub period-end, LE issued, CD issued, lock expiration, and closing as they stored them. Quote the source file for each date. Do not invent a date. Do not decide TRID waits as counsel. Do not lock. Do not store a full SSN. Write-up lists dates and blanks, not a legal timeline opinion.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: date-stamps
steps:
  - id: cal
    needs: []
    produces: calendar
    produce_path: work/processor-calendar.csv
    tool: docs/tools/calendar.md
    check: python docs/tools/checks/csv-has-columns.py work/processor-calendar.csv loan date
    on_fail: retry
    next: [index]
  - id: index
    needs: [calendar]
    produces: index
    produce_path: work/document-index.csv
    tool: docs/tools/document-folder-index.md
    check: python docs/tools/checks/file-exists.py work/document-index.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [calendar, index]
    produces: dates
    produce_path: out/date-stamps.md
    tool: docs/tools/calendar.md
    check: python docs/tools/checks/file-exists.py out/date-stamps.md
    on_fail: retry
    next: []
```
