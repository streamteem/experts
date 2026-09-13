# Missing report and outlier list

Write a missing-count CSV for the columns they named and an outlier-list CSV using the fence or threshold they named. The write-up lists source file, n, the rule, and that listed points were not deleted unless they asked. Do not impute. Do not call a point an error without their file. If numpy is missing and they wanted a numeric fence, ask; do not invent rows.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: missing-and-outliers
steps:
  - id: missing
    needs: []
    produces: missing
    produce_path: work/missing-report.csv
    tool: docs/tools/pandas.md
    check: python docs/tools/checks/csv-has-columns.py work/missing-report.csv column count missing
    on_fail: retry
    next: [outliers]
  - id: outliers
    needs: [missing]
    produces: outliers
    produce_path: work/outlier-list.csv
    tool: docs/tools/numpy.md
    check: python docs/tools/checks/file-exists.py work/outlier-list.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [missing, outliers]
    produces: writeup
    produce_path: out/missing-and-outliers.md
    tool: docs/tools/python.md
    check: python docs/tools/checks/file-exists.py out/missing-and-outliers.md
    on_fail: retry
    next: []
```
