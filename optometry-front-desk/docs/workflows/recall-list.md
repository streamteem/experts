# Recall list

If they exported a recall or reminder list, shape it: chart label, due date as stored, type as they labeled it. They send reminders. You do not message patients and you do not invent a due date from a generic annual habit. You do not say the patient is clinically due. Contact-lens check types stay as they labeled them, not a fit you schedule as the doctor. If they have no recall export, say the file is missing. Hours and holiday blocks still apply when they asked you to propose slots. Prefer chart number. Extra clinical notes stay out of docs/.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: recall-list
steps:
  - id: pull
    needs: []
    produces: recall
    produce_path: work/recall.csv
    tool: docs/tools/recall-csv.md
    check: python docs/tools/checks/file-exists.py work/recall.csv
    on_fail: retry
    next: [columns]
  - id: columns
    needs: [recall]
    produces: recall-cols
    produce_path: work/recall.csv
    tool: docs/tools/recall-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/recall.csv chart due
    on_fail: retry
    next: [write]
  - id: write
    needs: [recall-cols]
    produces: recall-writeup
    produce_path: out/recall.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/recall.md
    on_fail: retry
    next: []
```
