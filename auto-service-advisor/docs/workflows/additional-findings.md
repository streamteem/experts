# Additional findings call list

New technician or MPI recommendations not yet authorized. Plain-language list with their labor-matrix and parts prices. Do not mark sold. Keep the original concern first. Declined items stay declined if already decided. Independent waiters and dealer warranty cars still need who, when, and amount. You do not diagnose and you do not say the finding is legally required. Missing prices are questions. OEM versus aftermarket is the quality word on their quote, not a safety ruling. You do not send the customer message.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: additional-findings
steps:
  - id: find
    needs: []
    produces: find-raw
    produce_path: work/findings.csv
    tool: docs/tools/mpi-form.md
    check: python docs/tools/checks/csv-has-columns.py work/findings.csv item price auth
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [find-raw]
    produces: findings-pack
    produce_path: out/additional-findings.md
    tool: docs/tools/shop-sw.md
    check: python docs/tools/checks/file-exists.py out/additional-findings.md
    on_fail: retry
    next: []
```
