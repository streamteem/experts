# Change-after-cutoff log

List revisions from the change-log sheet against each event's cutoff from the order: old value, new value, date of change, and whether it is after cutoff. Do not hide a late count. Do not invent a late fee. Guarantee still wins until they file a new guarantee. Write-up flags late adds that lack a pack-out or prep revision. They accept or refuse. You keep lateness visible.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: change-after-cutoff-log
steps:
  - id: log
    needs: []
    produces: log
    produce_path: work/change-log.csv
    tool: docs/tools/change-log-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/change-log.csv event changed
    on_fail: retry
    next: [orders]
  - id: orders
    needs: [log]
    produces: orders
    produce_path: work/cutoff-orders.csv
    tool: docs/tools/event-order-pdf.md
    check: python docs/tools/checks/csv-has-columns.py work/cutoff-orders.csv event cutoff
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [log, orders]
    produces: cutoff-pack
    produce_path: out/change-after-cutoff.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/change-after-cutoff.md
    on_fail: retry
    next: []
```
