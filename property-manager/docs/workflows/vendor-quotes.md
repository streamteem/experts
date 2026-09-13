# Vendor quote compare

Collect the quote PDFs for one work order or capex item they name. Build a table of vendor, amount copied from each PDF, and scope as printed. Ask their two-quote threshold; skip shopping on true emergencies. They pick and they approve. Do not round, do not pick a winner, and do not pay a vendor deposit from this folder. Missing pages are questions. License and COI claims come only from files they provided.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: vendor-quotes
steps:
  - id: collect
    needs: []
    produces: quotes-raw
    produce_path: work/quotes-raw.csv
    tool: docs/tools/vendor-portal.md
    check: python docs/tools/checks/file-exists.py work/quotes-raw.csv
    on_fail: retry
    next: [compare]
  - id: compare
    needs: [quotes-raw]
    produces: quotes-table
    produce_path: work/quotes-table.csv
    tool: docs/tools/vendor-portal.md
    check: python docs/tools/checks/csv-has-columns.py work/quotes-table.csv vendor amount scope
    on_fail: retry
    next: [owner-ask]
  - id: owner-ask
    needs: [quotes-table]
    produces: quotes-pack
    produce_path: out/vendor-quotes.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/vendor-quotes.md
    on_fail: retry
    next: []
```
