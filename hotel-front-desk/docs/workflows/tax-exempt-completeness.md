# Tax-exempt completeness

Compare folios coded tax-exempt to certificates in the tax-file folder. List present, missing, expired, and name-mismatch. Do not decide exemption as law and do not invent a zero tax. Tax-off without a cert stays an exception. They apply or reverse tax. You deliver the completeness list and write-up. Name-mismatch and expired letters count as missing. You do not accept a verbal exemption. Occupancy tax stays their file, not a legal opinion.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: tax-exempt-completeness
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
    produces: exempt-pack
    produce_path: out/tax-exempt-completeness.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/tax-exempt-completeness.md
    on_fail: retry
    next: []
```
