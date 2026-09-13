# Contract completeness pack

Read contract PDFs against their required fields: renter, unit or serial, dates, rate lines from the rate file, waiver or RPP box, tax or exempt cert pointer, PO if the account needs one, and COI if required. Do not invent a rate, tax, or deposit. Draft is not signed out. Blank required fields become asks. No PAN copied from a scan. Produce the missing-fields list and write-up. They sign and they collect.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: contract-completeness
steps:
  - id: pdf
    needs: []
    produces: contracts
    produce_path: work/contracts.csv
    tool: docs/tools/contract-pdf-folder.md
    check: python docs/tools/checks/file-exists.py work/contracts.csv
    on_fail: retry
    next: [rates]
  - id: rates
    needs: [contracts]
    produces: rates
    produce_path: work/rate-file.csv
    tool: docs/tools/rate-file.md
    check: python docs/tools/checks/file-exists.py work/rate-file.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [contracts, rates]
    produces: contract-pack
    produce_path: out/contract-completeness.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/contract-completeness.md
    on_fail: retry
    next: []
```
