# Outside-process due list

List send-out operations from the work-order export against the outside-PO list. Promise dates come only from that PO file. Do not invent a subcontract lead. Do not pay the vendor. Missing PO on an outside op stays a gap. Late promises versus job due stay flagged infeasible. Certs expected back stay present-or-missing. They expedite; you list. Return-to-dock shorts stay visible. You do not invent transit days. Certs expected with the lot stay present-or-missing on the same pack.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: outside-process-due
steps:
  - id: wo
    needs: []
    produces: wos
    produce_path: work/work-orders.csv
    tool: docs/tools/wo-export.md
    check: python docs/tools/checks/csv-has-columns.py work/work-orders.csv wo item qty
    on_fail: retry
    next: [pos]
  - id: pos
    needs: [wos]
    produces: pos
    produce_path: work/outside-pos.csv
    tool: docs/tools/outside-po-list.md
    check: python docs/tools/checks/file-exists.py work/outside-pos.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [wos, pos]
    produces: outside-pack
    produce_path: out/outside-due.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/outside-due.md
    on_fail: retry
    next: []
```
