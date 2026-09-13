# Assignment board

Build a board from their assignment sheet, employee list, and calendar: person, client, shift, start, expected end, status, and DNS/unavailable filters they already coded. Do not invent a placement. Do not invent a start. Do not fire anyone. Rates stay pointers to the rate file, not guessed markups. Write the board CSV and a short write-up. They dispatch. You list holes. SSNs stay out of the board.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: assignment-board
steps:
  - id: assign
    needs: []
    produces: assign
    produce_path: work/assignments.csv
    tool: docs/tools/assignment-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/assignments.csv employee client start
    on_fail: retry
    next: [people]
  - id: people
    needs: [assign]
    produces: people
    produce_path: work/employee-list.csv
    tool: docs/tools/employee-list.md
    check: python docs/tools/checks/csv-has-columns.py work/employee-list.csv name
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [assign, people]
    produces: board
    produce_path: out/assignment-board.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/assignment-board.md
    on_fail: retry
    next: []
```
