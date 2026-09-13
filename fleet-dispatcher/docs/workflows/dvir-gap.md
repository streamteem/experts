# DVIR presence

Which units on today’s roster have a DVIR file. Missing is missing. No invented clean reports and no copy-forward from yesterday or from the tractor onto a trailer. Join roster units to the inspection export, then write gaps the checks can see. Defect text is copied, not closed by you. Not an out-of-service ruling. Starter / guess until they teach this shop.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: dvir-gap
steps:
  - id: units
    needs: []
    produces: units-raw
    produce_path: work/units.csv
    tool: docs/tools/roster.md
    check: python docs/tools/checks/csv-has-columns.py work/units.csv unit driver
    on_fail: retry
    next: [dvirs]
  - id: dvirs
    needs: [units-raw]
    produces: dvir-raw
    produce_path: work/dvir.csv
    tool: docs/tools/dvir.md
    check: python docs/tools/checks/csv-has-columns.py work/dvir.csv unit date defect
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [dvir-raw]
    produces: dvir-pack
    produce_path: out/dvir-gaps.md
    tool: docs/tools/dvir.md
    check: python docs/tools/checks/file-exists.py out/dvir-gaps.md
    on_fail: retry
    next: []
```
