# ACORD completeness

Index the ACORD and application PDFs they dropped. List form number, named insured as written, and blank required boxes. Do not fill class codes, FEIN, payroll, or VINs from memory. Do not call the packet ready to bind. Unsigned producer blocks stay unsigned. Attach a missing-forms CSV the producer can work. They obtain answers and they submit. You keep present-versus-missing visible.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: acord-completeness
steps:
  - id: folder
    needs: []
    produces: acord
    produce_path: work/acord-index.csv
    tool: docs/tools/acord-pdf-folder.md
    check: python docs/tools/checks/file-exists.py work/acord-index.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [acord]
    produces: acord-pack
    produce_path: out/acord-missing.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/acord-missing.md
    on_fail: retry
    next: []
```
