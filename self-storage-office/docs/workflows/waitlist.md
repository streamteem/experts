# Waitlist pack

List waitlist rows in their existing order with size wanted and date added. Do not jump a referral. Do not invent a phone. A seat is not a hold unless occupancy shows a reservation they coded. You may flag a matching vacant from the occupancy export as a question; you do not assign the unit. Stale rows stay until their purge rule. They call the next person. You write the list.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: waitlist
steps:
  - id: list
    needs: []
    produces: wait
    produce_path: work/waitlist.csv
    tool: docs/tools/waitlist.md
    check: python docs/tools/checks/csv-has-columns.py work/waitlist.csv size_wanted
    on_fail: retry
    next: [occ]
  - id: occ
    needs: [wait]
    produces: occ
    produce_path: work/occupancy.csv
    tool: docs/tools/occupancy-export.md
    check: python docs/tools/checks/file-exists.py work/occupancy.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [wait, occ]
    produces: wait-pack
    produce_path: out/waitlist.md
    tool: docs/tools/waitlist.md
    check: python docs/tools/checks/file-exists.py out/waitlist.md
    on_fail: retry
    next: []
```
