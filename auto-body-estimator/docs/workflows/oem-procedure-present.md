# OEM procedure present

Index procedure PDFs against estimate operations that their process says need a page. List present versus missing. Do not invent a page. Do not stamp weld, ADAS, or scan complete. I-CAR and OEM sites are orientation; their saved PDF is the evidence. Write-up is the completeness list plus asks, not a repair-procedure you invent. Wrong-VIN pages stay mismatch. You do not invent a sectioning method. Write-up is present versus missing plus asks. Weld and ADAS lines without pages stay asks, not stamps.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: oem-procedure-present
steps:
  - id: proc
    needs: []
    produces: proc
    produce_path: work/procedure-index.csv
    tool: docs/tools/procedure-pdf-folder.md
    check: python docs/tools/checks/file-exists.py work/procedure-index.csv
    on_fail: retry
    next: [est]
  - id: est
    needs: [proc]
    produces: est
    produce_path: work/estimate-export.csv
    tool: docs/tools/estimate-export.md
    check: python docs/tools/checks/file-exists.py work/estimate-export.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [proc, est]
    produces: proc-pack
    produce_path: out/oem-procedure-present.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/oem-procedure-present.md
    on_fail: retry
    next: []
```
