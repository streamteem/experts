# Supplement log

List estimate versions from the supplement log and join to the estimate export so first-write versus later dollars stay visible. Do not invent a supplement. Do not hide an insurer reduction. Aging days come from their dates, not a promised SLA. Write-up is the version list plus asks, not a totaling verdict and not a promise the carrier will pay.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: supplement-log
steps:
  - id: log
    needs: []
    produces: log
    produce_path: work/supplement-log.csv
    tool: docs/tools/supplement-log.md
    check: python docs/tools/checks/csv-has-columns.py work/supplement-log.csv claim date
    on_fail: retry
    next: [est]
  - id: est
    needs: [log]
    produces: est
    produce_path: work/estimate-export.csv
    tool: docs/tools/estimate-export.md
    check: python docs/tools/checks/file-exists.py work/estimate-export.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [log, est]
    produces: supp-pack
    produce_path: out/supplement-log.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/supplement-log.md
    on_fail: retry
    next: []
```
