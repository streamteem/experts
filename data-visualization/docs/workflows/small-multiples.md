# Small multiples from a facet they name

Repeat the same chart for each value of the facet column they named. Write the aggregated work CSV, one faceted PNG, and a write-up that states shared versus free y-scale and n per panel. Do not drop a small panel. Do not invent a facet. A folder of files is the dashboard, not a BI site. If seaborn is missing, matplotlib subplots or an install ask — do not fake panels.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: small-multiples
steps:
  - id: facet
    needs: []
    produces: facet
    produce_path: work/small-multiples.csv
    tool: docs/tools/pandas.md
    check: python docs/tools/checks/csv-has-columns.py work/small-multiples.csv facet date value
    on_fail: retry
    next: [chart]
  - id: chart
    needs: [facet]
    produces: png
    produce_path: out/small-multiples.png
    tool: docs/tools/seaborn.md
    check: python docs/tools/checks/file-exists.py out/small-multiples.png
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [png]
    produces: writeup
    produce_path: out/small-multiples.md
    tool: docs/tools/chart-output-folder.md
    check: python docs/tools/checks/file-exists.py out/small-multiples.md
    on_fail: retry
    next: []
```
