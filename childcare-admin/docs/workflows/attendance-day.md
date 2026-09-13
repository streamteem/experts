# Day attendance list

From the attendance export, list the program date by room, child label they allow, and present/absent or in/out as they coded it. Confirm the file date before you treat it as today. Do not mark anyone present to tidy ratio. Flag sign-in gaps and illness wording as their words, not a diagnosis. Prefer child ID. Never release a child from this list. If roster and attendance disagree on who is enrolled versus present, quote both in the write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: attendance-day
steps:
  - id: pull
    needs: []
    produces: att
    produce_path: work/attendance.csv
    tool: docs/tools/attendance-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/attendance.csv child status
    on_fail: retry
    next: [roster]
  - id: roster
    needs: [att]
    produces: roster
    produce_path: work/roster.csv
    tool: docs/tools/roster-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/roster.csv child room
    on_fail: retry
    next: [write]
  - id: write
    needs: [att, roster]
    produces: att-pack
    produce_path: out/attendance-day.md
    tool: docs/tools/attendance-csv.md
    check: python docs/tools/checks/file-exists.py out/attendance-day.md
    on_fail: retry
    next: []
```
