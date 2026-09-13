# Group-compare bars

Group the measure they named by the category they named. Write the aggregated work CSV, a PNG bar chart, and a write-up. Sort by the rule they named. Zero baseline for counts and dollars. Colorblind palette. Do not invent a category or a winner stamp. Say n per bar when slices are small. If seaborn is missing, matplotlib bars are fine; ask rather than fake a file.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: group-compare-bars
steps:
  - id: agg
    needs: []
    produces: agg
    produce_path: work/group-compare.csv
    tool: docs/tools/pandas.md
    check: python docs/tools/checks/csv-has-columns.py work/group-compare.csv group value
    on_fail: retry
    next: [chart]
  - id: chart
    needs: [agg]
    produces: png
    produce_path: out/group-compare-bars.png
    tool: docs/tools/seaborn.md
    check: python docs/tools/checks/file-exists.py out/group-compare-bars.png
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [png]
    produces: writeup
    produce_path: out/group-compare-bars.md
    tool: docs/tools/chart-output-folder.md
    check: python docs/tools/checks/file-exists.py out/group-compare-bars.md
    on_fail: retry
    next: []
```
