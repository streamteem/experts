# Contractor work-order list

Join open work orders that they coded contractor or outside-service to their contractor list. List firm, craft, ticket, and asset. Do not invent a vendor. Do not pay. Do not treat the contractor as holding this plant's electrical license. Missing COI dates stay dates-missing, not a legal finding. Write-up is a contractor board, not a construction sub list and not a field-trade sub dispatch.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: contractor-wo-list
steps:
  - id: firms
    needs: []
    produces: firms
    produce_path: work/contractors.csv
    tool: docs/tools/contractor-list.md
    check: python docs/tools/checks/file-exists.py work/contractors.csv
    on_fail: retry
    next: [tickets]
  - id: tickets
    needs: [firms]
    produces: tickets
    produce_path: work/wo.csv
    tool: docs/tools/wo-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/wo.csv wo asset priority
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [firms, tickets]
    produces: contractor-pack
    produce_path: out/contractor-wo-list.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/contractor-wo-list.md
    on_fail: retry
    next: []
```
