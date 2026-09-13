# Daily log pack

Fill or extract today's log for one job number into work/, then a write-up that quotes their rows. Their template wins over starter columns. Keep weather, manpower, equipment, and notes as they wrote them; blank stays blank with an ask. Do not reconstruct a missing day from photos or last week. One job per pack unless they asked for a job column. Incidents on the log are flagged and leave this workflow. The pack should name the source sheet and the job number the check can see.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: daily-log
steps:
  - id: collect
    needs: []
    produces: log-raw
    produce_path: work/daily-log.csv
    tool: docs/tools/log-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/daily-log.csv date job
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [log-raw]
    produces: log-pack
    produce_path: out/daily-log.md
    tool: docs/tools/log-sheet.md
    check: python docs/tools/checks/file-exists.py out/daily-log.md
    on_fail: retry
    next: []
```
