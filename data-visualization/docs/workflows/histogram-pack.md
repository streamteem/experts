# Histogram pack

From the numeric column they named, write a work CSV of the plotted values, a PNG histogram, and a write-up. Bin width is an ask or a stated default — do not hunt bins for a story. Say n, units, missing count, and what was not claimed. If matplotlib or seaborn is missing, ask and install; do not fake a PNG. Outliers stay unless they asked to list them aside.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: histogram-pack
steps:
  - id: values
    needs: []
    produces: values
    produce_path: work/histogram-values.csv
    tool: docs/tools/pandas.md
    check: python docs/tools/checks/csv-has-columns.py work/histogram-values.csv value
    on_fail: retry
    next: [chart]
  - id: chart
    needs: [values]
    produces: png
    produce_path: out/histogram.png
    tool: docs/tools/matplotlib.md
    check: python docs/tools/checks/file-exists.py out/histogram.png
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [png]
    produces: writeup
    produce_path: out/histogram-pack.md
    tool: docs/tools/chart-output-folder.md
    check: python docs/tools/checks/file-exists.py out/histogram-pack.md
    on_fail: retry
    next: []
```
