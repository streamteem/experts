# Day list

From the schedule export, list the day by time, provider, type, and their patient label. Keep closed blocks, lunch, and huddle rows. Flag emergency wording for staff. No clinical notes and no diagnosis from the reason field. One clinic date and one location unless they asked for a multi-day book and the file has a date column. Flag overlaps that their double-book rule does not allow; do not move providers to hide them. Prefer chart or MRN. Confirm the export date before you treat it as tomorrow.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: day-list
steps:
  - id: pull
    needs: []
    produces: sched
    produce_path: work/day-list.csv
    tool: docs/tools/day-list-csv.md
    check: python docs/tools/checks/file-exists.py work/day-list.csv
    on_fail: retry
    next: [blocks]
  - id: blocks
    needs: [sched]
    produces: blocks
    produce_path: work/blocks.csv
    tool: docs/tools/calendar-blocks.md
    check: python docs/tools/checks/file-exists.py work/blocks.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [sched, blocks]
    produces: day-writeup
    produce_path: out/day-list.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/day-list.md
    on_fail: retry
    next: []
```
