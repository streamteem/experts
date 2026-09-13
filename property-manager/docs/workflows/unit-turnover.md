# Unit turnover pack

For one unit, assemble the vacate file (notice dates, lease-index gaps), the make-ready punch, and the rent-ready label they use. This is an operations pack, not an inspection certificate and not a habitability ruling. Do not change locks as a lockout, do not store codes, and do not pay vendors or refund the deposit from this folder. Days-vacant math uses their status flip dates. Photos are indexed, not verdicts.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: unit-turnover
steps:
  - id: vacate
    needs: []
    produces: vacate-file
    produce_path: work/vacate-file.csv
    tool: docs/tools/lease-file-index.md
    check: python docs/tools/checks/file-exists.py work/vacate-file.csv
    on_fail: retry
    next: [ready]
  - id: ready
    needs: [vacate-file]
    produces: turnover-punch
    produce_path: work/turnover-punch.csv
    tool: docs/tools/make-ready-list.md
    check: python docs/tools/checks/csv-has-columns.py work/turnover-punch.csv unit item status
    on_fail: retry
    next: [turn-pack]
  - id: turn-pack
    needs: [turnover-punch]
    produces: turnover-writeup
    produce_path: out/unit-turnover.md
    tool: docs/tools/make-ready-list.md
    check: python docs/tools/checks/file-exists.py out/unit-turnover.md
    on_fail: retry
    next: []
```
