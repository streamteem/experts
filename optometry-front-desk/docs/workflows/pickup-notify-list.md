# Pickup notify list

From the lab-status or tray export, list jobs their status word says are ready and not yet marked notified. Chart label, job or tray number, preferred contact as stored. They call or text. You do not send the notice and you do not invent that someone was reached. Ready must come from their status file, not a guessed ship date. Do not include Rx powers on the notify list. Extra phones the list does not need stay out. Minors follow their guardian contact fields. Produce the list plus a write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: pickup-notify-list
steps:
  - id: status
    needs: []
    produces: status
    produce_path: work/lab-status.csv
    tool: docs/tools/lab-status.md
    check: python docs/tools/checks/csv-has-columns.py work/lab-status.csv job status
    on_fail: retry
    next: [day]
  - id: day
    needs: [status]
    produces: day
    produce_path: work/day-list.csv
    tool: docs/tools/day-list-csv.md
    check: python docs/tools/checks/file-exists.py work/day-list.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [status, day]
    produces: notify-writeup
    produce_path: out/pickup-notify.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/pickup-notify.md
    on_fail: retry
    next: []
```
