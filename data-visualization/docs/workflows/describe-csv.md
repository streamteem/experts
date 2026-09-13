# Describe a CSV they dropped

Load the CSV they named with pandas. Write a summary CSV of count, missing, min, max, and mean for numeric columns they named. The write-up states the question, the source file name, the columns, any filters, and that no cause was claimed. Do not invent a column. Do not impute. If pandas is missing, ask and stop; do not fake a summary. They read the pack; you do not call it a census of the shop.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: describe-csv
steps:
  - id: load
    needs: []
    produces: source
    produce_path: work/describe-source.csv
    tool: docs/tools/csv-folder.md
    check: python docs/tools/checks/file-exists.py work/describe-source.csv
    on_fail: retry
    next: [summary]
  - id: summary
    needs: [source]
    produces: summary
    produce_path: work/describe-summary.csv
    tool: docs/tools/pandas.md
    check: python docs/tools/checks/csv-has-columns.py work/describe-summary.csv column count missing min max mean
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [summary]
    produces: writeup
    produce_path: out/describe-csv.md
    tool: docs/tools/python.md
    check: python docs/tools/checks/file-exists.py out/describe-csv.md
    on_fail: retry
    next: []
```
