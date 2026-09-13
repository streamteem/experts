# Folio exception pack

Read folio PDFs against the tax file and any package or routing notes they stored. List missing posts, duplicates, tax-off without a cert, comps without a code, and POS mismatches. Never invent a correcting amount or a tax. Stop and ask if PAN is visible. They adjust folios. You deliver the exception list and write-up. Package-split misses and city-ledger routing errors belong on the same list when the files show them. Do not hide a miss to tidy night audit. Min-necessary guest labels only.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: folio-exceptions
steps:
  - id: folios
    needs: []
    produces: folios
    produce_path: work/folio-index.csv
    tool: docs/tools/folio-pdf.md
    check: python docs/tools/checks/file-exists.py work/folio-index.csv
    on_fail: retry
    next: [tax]
  - id: tax
    needs: [folios]
    produces: tax
    produce_path: work/tax-file.csv
    tool: docs/tools/tax-file.md
    check: python docs/tools/checks/file-exists.py work/tax-file.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [folios, tax]
    produces: folio-pack
    produce_path: out/folio-exceptions.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/folio-exceptions.md
    on_fail: retry
    next: []
```
