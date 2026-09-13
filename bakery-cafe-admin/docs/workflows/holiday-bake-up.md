# Holiday bake-up

Pull the holiday tab on their calendar and the matching bake-list rows: pies, cookies, laminated locks, preorder cutoffs. Do not invent holiday qty from last year. Do not invent a seasonal formula. Do not leave holiday qty on the next daily list unless they said so. Flag ingredient and oven-window holes. Write-up is the dated plan plus asks. They own the holiday.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: holiday-bake-up
steps:
  - id: cal
    needs: []
    produces: cal
    produce_path: work/production-calendar.csv
    tool: docs/tools/calendar.md
    check: python docs/tools/checks/file-exists.py work/production-calendar.csv
    on_fail: retry
    next: [list]
  - id: list
    needs: [cal]
    produces: bake-list
    produce_path: work/bake-list.csv
    tool: docs/tools/bake-list-sheet.md
    check: python docs/tools/checks/file-exists.py work/bake-list.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [cal, bake-list]
    produces: holiday-pack
    produce_path: out/holiday-bake-up.md
    tool: docs/tools/calendar.md
    check: python docs/tools/checks/file-exists.py out/holiday-bake-up.md
    on_fail: retry
    next: []
```
