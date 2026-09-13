# Inventory versus chemical log

Compare their chemical inventory sheet to application-log product names they already wrote. Flag products logged that are not on the inventory key, and inventory rows with no matching log name if they asked. Do not invent on-hand qty. Do not invent an EPA number or a mix. Short counts stay visible. They buy and they count. You write the mismatch list and a write-up the check can see.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: inventory-chem-vs-log
steps:
  - id: inv
    needs: []
    produces: inv
    produce_path: work/inventory-chem.csv
    tool: docs/tools/inventory-chem.md
    check: python docs/tools/checks/csv-has-columns.py work/inventory-chem.csv product qty
    on_fail: retry
    next: [log]
  - id: log
    needs: [inv]
    produces: log
    produce_path: work/chemical-log.csv
    tool: docs/tools/chemical-log.md
    check: python docs/tools/checks/file-exists.py work/chemical-log.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [inv, log]
    produces: inv-log-pack
    produce_path: out/inventory-vs-log.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/inventory-vs-log.md
    on_fail: retry
    next: []
```
