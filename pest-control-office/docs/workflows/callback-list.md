# Callback list

List open callbacks from their callback file and matching tickets. Attach named photos if present. Do not diagnose a structure or a species. Do not promise eradication. Warranty versus courtesy versus billable follows their warranty file. Hours come from their sheet, not invented time. Skip and pet flags still apply. They schedule the return. You write the list and questions.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: callback-list
steps:
  - id: callbacks
    needs: []
    produces: callbacks
    produce_path: work/callbacks.csv
    tool: docs/tools/callback-list.md
    check: python docs/tools/checks/csv-has-columns.py work/callbacks.csv ticket account
    on_fail: retry
    next: [tickets]
  - id: tickets
    needs: [callbacks]
    produces: tickets
    produce_path: work/callback-tickets.csv
    tool: docs/tools/ticket-sheet.md
    check: python docs/tools/checks/file-exists.py work/callback-tickets.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [callbacks, tickets]
    produces: callback-pack
    produce_path: out/callbacks.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/callbacks.md
    on_fail: retry
    next: []
```
