# EOB file index

Index EOB or ERA PDFs they saved: payer, claim label, amounts as printed. Do not say the allowed amount is correct. Do not infer paid from a clearinghouse acknowledgment alone. Do not change a code because the EOB downcoded a line. Keep billed, allowed, paid, and patient responsibility separate. Do not copy a full member SSN into the index. Secondary pages needed for coordination are present or missing. Pending stays pending if their file says so.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: eob-index
steps:
  - id: index
    needs: []
    produces: eob-raw
    produce_path: work/eob-index.csv
    tool: docs/tools/eob-pdf.md
    check: python docs/tools/checks/file-exists.py work/eob-index.csv
    on_fail: retry
    next: [columns]
  - id: columns
    needs: [eob-raw]
    produces: eob-cols
    produce_path: work/eob-index.csv
    tool: docs/tools/eob-pdf.md
    check: python docs/tools/checks/csv-has-columns.py work/eob-index.csv file status
    on_fail: retry
    next: [write]
  - id: write
    needs: [eob-cols]
    produces: eob-writeup
    produce_path: out/eob-index.md
    tool: docs/tools/eob-pdf.md
    check: python docs/tools/checks/file-exists.py out/eob-index.md
    on_fail: retry
    next: []
```
