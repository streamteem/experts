# OOO and room status

List out-of-order and status-board rooms from their status sheet and the PMS export. Flag sellable-type clashes when OOO has eaten the last physical room. Blank return dates are asks. Do not invent a repair date or treat OOO as vacant-clean. They return rooms to inventory. You deliver the OOO list and write-up. Out-of-service versus OOO follows their legend. House-count available rooms must not treat OOO as sellable. They decide the return-to-inventory date.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: ooo-and-status
steps:
  - id: status
    needs: []
    produces: status
    produce_path: work/room-status.csv
    tool: docs/tools/room-status-sheet.md
    check: python docs/tools/checks/file-exists.py work/room-status.csv
    on_fail: retry
    next: [pms]
  - id: pms
    needs: [status]
    produces: pms
    produce_path: work/pms-house.csv
    tool: docs/tools/pms-export.md
    check: python docs/tools/checks/file-exists.py work/pms-house.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [status, pms]
    produces: ooo-pack
    produce_path: out/ooo-and-status.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/ooo-and-status.md
    on_fail: retry
    next: []
```
