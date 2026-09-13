# Missing-docs list

Compare their document-folder index to the conditions sheet and list named items that are missing, cut off, or undated. Do not invent a document type. Do not copy a full SSN or a credit score into the list. Do not treat missing as a denial. Income, VOE, contract, and title rows stay typed as they typed them. Write-up is a missing list plus asks, not an underwrite.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: missing-docs
steps:
  - id: index
    needs: []
    produces: index
    produce_path: work/document-index.csv
    tool: docs/tools/document-folder-index.md
    check: python docs/tools/checks/csv-has-columns.py work/document-index.csv loan document
    on_fail: retry
    next: [conds]
  - id: conds
    needs: [index]
    produces: conditions
    produce_path: work/conditions.csv
    tool: docs/tools/conditions-sheet.md
    check: python docs/tools/checks/file-exists.py work/conditions.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [index, conditions]
    produces: missing
    produce_path: out/missing-docs.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/missing-docs.md
    on_fail: retry
    next: []
```
