# Staffing from their file

Build a staffing board from the roster and the event-order labor grid: chef, captain, servers, bartender-as-count, driver. Flag missing rosters, invented-looking blanks, and people booked on overlapping windows. Do not invent a ratio. Do not stamp a bartender licensed. Overtime stays off unless their file has a rule. Write-up quotes the roster. They call staff. You do not fire anyone.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: staffing-from-file
steps:
  - id: roster
    needs: []
    produces: roster
    produce_path: work/staff-roster.csv
    tool: docs/tools/staff-roster.md
    check: python docs/tools/checks/csv-has-columns.py work/staff-roster.csv event role
    on_fail: retry
    next: [orders]
  - id: orders
    needs: [roster]
    produces: orders
    produce_path: work/staff-orders.csv
    tool: docs/tools/event-order-pdf.md
    check: python docs/tools/checks/csv-has-columns.py work/staff-orders.csv event date
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [roster, orders]
    produces: staff-pack
    produce_path: out/staffing-from-file.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/staffing-from-file.md
    on_fail: retry
    next: []
```
