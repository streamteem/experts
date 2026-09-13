# Pick list pack

From their order export and on-hand or available file. Write shorts. No silent substitute. Quantity cannot exceed the stock file they provided. Holds, damage, and consignment-to-someone-else are not house pick faces. Drop-ship lines stay off the warehouse pick. Do not promise a date or change a price. Lot and serial if required, following their pick rule only if they stored one. Missing stock file: say the pick is unconfirmed.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: pick-pack
steps:
  - id: orders
    needs: []
    produces: picks
    produce_path: work/picks.csv
    tool: docs/tools/pick-ticket.md
    check: python docs/tools/checks/csv-has-columns.py work/picks.csv sku qty
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [picks]
    produces: pick-out
    produce_path: out/picks.md
    tool: docs/tools/pick-ticket.md
    check: python docs/tools/checks/file-exists.py out/picks.md
    on_fail: retry
    next: []
```
