# Estimate pack from their files

Build an estimate pack from their labor matrix, parts file, and estimate export. Hours come only from the matrix or listed operations. Prices come only from the parts file. Do not invent hours or prices. Do not issue a total-loss verdict or a structural stamp. Write-up names which lines are first-write versus supplement and which fields were blank asks. Distinct from a mechanical RO estimate pack.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: estimate-from-files
steps:
  - id: matrix
    needs: []
    produces: matrix
    produce_path: work/labor-matrix.csv
    tool: docs/tools/labor-matrix.md
    check: python docs/tools/checks/csv-has-columns.py work/labor-matrix.csv op hours
    on_fail: retry
    next: [parts]
  - id: parts
    needs: [matrix]
    produces: parts
    produce_path: work/parts-file.csv
    tool: docs/tools/parts-file.md
    check: python docs/tools/checks/csv-has-columns.py work/parts-file.csv part price
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [matrix, parts]
    produces: estimate-pack
    produce_path: out/estimate-from-files.md
    tool: docs/tools/estimate-export.md
    check: python docs/tools/checks/file-exists.py out/estimate-from-files.md
    on_fail: retry
    next: []
```
