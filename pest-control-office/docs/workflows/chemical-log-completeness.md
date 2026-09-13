# Chemical log completeness

List application-log rows and flag blanks they use: product, EPA-from-their-file, rate-as-logged, tech, interior versus exterior. Do not invent a mix, rate, or EPA number. Tickets that say treated with no log row stay holes. License-on-file is present-or-missing, not a stamp. Held wind stops do not get a fake row. They complete the log. You write the hole list and a write-up the check can see.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: chemical-log-completeness
steps:
  - id: log
    needs: []
    produces: log
    produce_path: work/chemical-log.csv
    tool: docs/tools/chemical-log.md
    check: python docs/tools/checks/csv-has-columns.py work/chemical-log.csv date account
    on_fail: retry
    next: [tickets]
  - id: tickets
    needs: [log]
    produces: tickets
    produce_path: work/log-tickets.csv
    tool: docs/tools/ticket-sheet.md
    check: python docs/tools/checks/file-exists.py work/log-tickets.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [log, tickets]
    produces: log-pack
    produce_path: out/chemical-log-completeness.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/chemical-log-completeness.md
    on_fail: retry
    next: []
```
