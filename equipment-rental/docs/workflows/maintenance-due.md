# Maintenance-due versus reservations

List units their PM file marks due or overdue and show reservation or on-rent conflicts. Do not invent an interval and do not hide a due row to protect a booking. Do not write a repair diagnosis or a parts list. Substitution is their rule if a reserved unit is locked out. They decide shop, sub, or override. You produce the due list, conflicts, and write-up. Vendor invoices stay unpaid on this desk.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: maintenance-due
steps:
  - id: pm
    needs: []
    produces: pm
    produce_path: work/maintenance-due.csv
    tool: docs/tools/maintenance-due.md
    check: python docs/tools/checks/csv-has-columns.py work/maintenance-due.csv unit
    on_fail: retry
    next: [fleet]
  - id: fleet
    needs: [pm]
    produces: fleet
    produce_path: work/fleet.csv
    tool: docs/tools/fleet-csv.md
    check: python docs/tools/checks/file-exists.py work/fleet.csv
    on_fail: retry
    next: [res]
  - id: res
    needs: [fleet]
    produces: reservations
    produce_path: work/reservations.csv
    tool: docs/tools/reservation-csv.md
    check: python docs/tools/checks/file-exists.py work/reservations.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [pm, fleet, reservations]
    produces: pm-pack
    produce_path: out/maintenance-due.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/maintenance-due.md
    on_fail: retry
    next: []
```
