# Vendor bills pack

Collect vendor bill files for the period they name, index them, and code each row to an account on their chart or to a labeled guess. Produce the raw index, the coded CSV with date, amount, and category, and a pack the owner can review before they pay. They or their bank pay; this desk never originates payment. Do not invent missing amounts, vendors, or due dates. If a PDF is missing, park the line as a question. Ask cash versus accrual so you do not enter AP they do not use. Recurring rent or software is a question if this month's invoice is not in the folder. Starter coding is a guess until they teach the vendor map.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: vendor-bills
steps:
  - id: collect
    needs: []
    produces: bills-raw
    produce_path: work/bills-raw.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py work/bills-raw.csv
    on_fail: retry
    next: [code]
  - id: code
    needs: [bills-raw]
    produces: bills-coded
    produce_path: work/bills-coded.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/csv-has-columns.py work/bills-coded.csv date amount category
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [bills-coded]
    produces: bills-pack
    produce_path: out/vendor-bills.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/vendor-bills.md
    on_fail: retry
    next: []
```
