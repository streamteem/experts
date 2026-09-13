# Broken appointments list

From their sheet, list cancellations and no-shows they already coded. Do not invent a fee policy, a three-strikes rule, or a dismissal. Keep their status words (no-show versus same-day cancel) and do not infer no-show from a blank confirmation. You do not contact the list. You do not award a wait-list slot. Prefer chart number. If they have no broken column, say so. Do not copy extra clinical reason text into docs/ beyond the status they stored.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: broken-list
steps:
  - id: pull
    needs: []
    produces: broken-raw
    produce_path: work/broken.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py work/broken.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [broken-raw]
    produces: broken-writeup
    produce_path: out/broken-list.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/broken-list.md
    on_fail: retry
    next: []
```
