# Reminder list file

Produce a list from their export for them to send. You do not message clients. Include due date, patient, client, and the reminder name they stored. Drop deceased or inactivated patients when the export already marks them. Preferred contact is a column to copy, not a send. Duplicate rows are questions, not merges. This is a file for their mail, text, or phone process. Starter / guess until they teach which reminder types they actually send.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: reminder-list
steps:
  - id: pull
    needs: []
    produces: reminders
    produce_path: work/reminders.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py work/reminders.csv
    on_fail: retry
    next: [columns]
  - id: columns
    needs: [reminders]
    produces: rem-cols
    produce_path: work/reminders.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/csv-has-columns.py work/reminders.csv due
    on_fail: retry
    next: [write]
  - id: write
    needs: [rem-cols]
    produces: rem-writeup
    produce_path: out/reminders.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/reminders.md
    on_fail: retry
    next: []
```
