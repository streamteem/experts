# Attendance day list

Build the day's attendance list from their export. Keep their codes. Flag blank marks and dates that do not match the calendar file if they also dropped one. Do not invent excuses or truancy findings. Do not recode a teacher mark. One school date unless they asked for a range. Closed or late-start days stay labeled. They post the official count. You write the list and exceptions.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: attendance-day
steps:
  - id: pull
    needs: []
    produces: attendance
    produce_path: work/attendance.csv
    tool: docs/tools/attendance-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/attendance.csv student date
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [attendance]
    produces: attendance-pack
    produce_path: out/attendance-day.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/attendance-day.md
    on_fail: retry
    next: []
```
