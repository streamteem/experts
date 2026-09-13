# Appraisal in file (not a value)

Index the appraisal PDF folder: report present, report date, invoice, AOA, and printed appraisal conditions as text. Do not give a value opinion. Do not invent a value. Do not compare to a CMA. Do not pay the AMC. Ordered-but-missing stays missing, not a denial. Do not treat a completion photo as a value you certify. Write-up is a file pack, not an underwrite of collateral.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: appraisal-in-file-not-value
steps:
  - id: appr
    needs: []
    produces: appraisal
    produce_path: work/appraisal-index.csv
    tool: docs/tools/appraisal-pdf-folder.md
    check: python docs/tools/checks/csv-has-columns.py work/appraisal-index.csv loan document
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [appraisal]
    produces: appraisal-pack
    produce_path: out/appraisal-in-file.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/appraisal-in-file.md
    on_fail: retry
    next: []
```
