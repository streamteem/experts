# Notice process log (not legal forms)

Log notices they already use: type, unit, date, method, who approved. Flag missing fields. Do not draft statutory pay-or-quit, lockout, or eviction text, and do not invent a day count from another state. They or counsel send. The handoff is a process gap list, not a form bank and not a statement that anything was properly served. Entry-notice hours are ask-not-invent. Codes stay in their vault.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: notice-process
steps:
  - id: log
    needs: []
    produces: notice-raw
    produce_path: work/notice-log.csv
    tool: docs/tools/notice-log.md
    check: python docs/tools/checks/file-exists.py work/notice-log.csv
    on_fail: retry
    next: [gaps]
  - id: gaps
    needs: [notice-raw]
    produces: notice-gaps
    produce_path: work/notice-gaps.csv
    tool: docs/tools/notice-log.md
    check: python docs/tools/checks/csv-has-columns.py work/notice-gaps.csv unit type missing
    on_fail: retry
    next: [handoff]
  - id: handoff
    needs: [notice-gaps]
    produces: notice-handoff
    produce_path: out/notice-process.md
    tool: docs/tools/notice-log.md
    check: python docs/tools/checks/file-exists.py out/notice-process.md
    on_fail: retry
    next: []
```
