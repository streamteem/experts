# Deliveries list

List expected and received deliveries for one job. Missing tickets stay missing; a calendar hold is not received. Match each line to a packing slip or photo they filed, and say when the page is absent. Short counts stay on their receiving words. Use their job number on every row. Do not move a truck to a neighboring job. The notes file names ticket numbers as printed. The pack quotes present versus missing backup so later pay or shortage talks have a dated list, not a smoothed story.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: deliveries
steps:
  - id: list
    needs: []
    produces: deliveries
    produce_path: work/deliveries.csv
    tool: docs/tools/delivery-ticket.md
    check: python docs/tools/checks/csv-has-columns.py work/deliveries.csv date item
    on_fail: retry
    next: [match]
  - id: match
    needs: [deliveries]
    produces: ticket-notes
    produce_path: work/delivery-tickets.md
    tool: docs/tools/delivery-ticket.md
    check: python docs/tools/checks/file-exists.py work/delivery-tickets.md
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [ticket-notes]
    produces: del-pack
    produce_path: out/deliveries.md
    tool: docs/tools/log-sheet.md
    check: python docs/tools/checks/file-exists.py out/deliveries.md
    on_fail: retry
    next: []
```
