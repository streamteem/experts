# Machine-down versus WIP

Put the machine-status file next to open work at those work centers. Down stays visible. Do not invent a repair duration or a diagnosis. Queued jobs remain on the list. Alternate-router moves wait for their file. Capacity hours on a down day are not available unless they wrote a workaround. Write-up quotes the status timestamp. They return the machine to service.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: machine-down-vs-wip
steps:
  - id: status
    needs: []
    produces: status
    produce_path: work/machine-status.csv
    tool: docs/tools/machine-status.md
    check: python docs/tools/checks/file-exists.py work/machine-status.csv
    on_fail: retry
    next: [wo]
  - id: wo
    needs: [status]
    produces: wos
    produce_path: work/work-orders.csv
    tool: docs/tools/wo-export.md
    check: python docs/tools/checks/csv-has-columns.py work/work-orders.csv wo item qty
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [status, wos]
    produces: down-pack
    produce_path: out/machine-down-wip.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/machine-down-wip.md
    on_fail: retry
    next: []
```
