# House count pack

Restate tonight’s house count from their PMS export and in-house list: occupied, vacant-sellable, OOO, arrivals not in, and due-outs, by type if their report splits them. Occupancy percent and ADR only if their flash already printed them or they wrote the math. If the three files disagree, quote all three. Do not invent a percent. They decide what to sell. You deliver the count and write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: house-count
steps:
  - id: pms
    needs: []
    produces: pms
    produce_path: work/pms-house.csv
    tool: docs/tools/pms-export.md
    check: python docs/tools/checks/file-exists.py work/pms-house.csv
    on_fail: retry
    next: [inh]
  - id: inh
    needs: [pms]
    produces: inhouse
    produce_path: work/in-house.csv
    tool: docs/tools/in-house-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/in-house.csv room status
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [pms, inhouse]
    produces: count-pack
    produce_path: out/house-count.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/house-count.md
    on_fail: retry
    next: []
```
