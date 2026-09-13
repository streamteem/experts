# Time-series line

Parse the date column they named, apply the date range they named, aggregate to the grain they named, and write a work series CSV plus a PNG line. Gaps stay gaps unless they said how to treat closed days. Do not extend the line as a forecast. Rolling mean only if they asked, labeled as history. Timezone and week-start: ask if missing. Name the source file in the write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: time-series-line
steps:
  - id: series
    needs: []
    produces: series
    produce_path: work/timeseries.csv
    tool: docs/tools/pandas.md
    check: python docs/tools/checks/csv-has-columns.py work/timeseries.csv date value
    on_fail: retry
    next: [chart]
  - id: chart
    needs: [series]
    produces: png
    produce_path: out/timeseries-line.png
    tool: docs/tools/matplotlib.md
    check: python docs/tools/checks/file-exists.py out/timeseries-line.png
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [png]
    produces: writeup
    produce_path: out/timeseries-line.md
    tool: docs/tools/python.md
    check: python docs/tools/checks/file-exists.py out/timeseries-line.md
    on_fail: retry
    next: []
```
