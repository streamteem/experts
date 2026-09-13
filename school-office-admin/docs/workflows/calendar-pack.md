# Calendar pack

Copy instructional days, holidays, and early dismissals from their calendar file. Attach bell-schedule versions if they stored them. Do not invent a snow-day makeup or a state hour rule. If two calendars disagree, quote both. Handbook dates that conflict with the calendar stay flagged. They publish. You pack the dated list and a write-up. Exam windows and conference days belong on the pack if the file has them. Do not promise a closure from a nearby district rumor. They publish revisions. You quote the dated file.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: calendar-pack
steps:
  - id: cal
    needs: []
    produces: calendar
    produce_path: work/calendar.csv
    tool: docs/tools/calendar-file.md
    check: python docs/tools/checks/file-exists.py work/calendar.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [calendar]
    produces: calendar-pack
    produce_path: out/calendar-pack.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/calendar-pack.md
    on_fail: retry
    next: []
```
