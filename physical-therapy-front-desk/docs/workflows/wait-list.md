# Wait-list pack

From their wait-list file, keep their order and requested type and therapist. Match open or cancelled slots from the day list only as listed options. They choose who is offered. You do not message patients and you do not invent that someone was reached. Emergency wording flags staff and is not a diagnosis. Extra phones the send-list does not need stay out of the write-up. Prefer chart number. Cancel wait-fill still follows their order, not a jump you invent.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: wait-list
steps:
  - id: wait
    needs: []
    produces: wait
    produce_path: work/wait-list.csv
    tool: docs/tools/wait-list.md
    check: python docs/tools/checks/csv-has-columns.py work/wait-list.csv chart type
    on_fail: retry
    next: [slots]
  - id: slots
    needs: [wait]
    produces: slots
    produce_path: work/day-list.csv
    tool: docs/tools/schedule-csv.md
    check: python docs/tools/checks/file-exists.py work/day-list.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [wait, slots]
    produces: wait-writeup
    produce_path: out/wait-list.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/wait-list.md
    on_fail: retry
    next: []
```
