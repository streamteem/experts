# Detention / dwell questions

In and out times from their scan, route sheet, or site file. No invented dwell minutes or claim amount. Missing arrive or depart is a question. Long dwell is flagged for a human, not filed as a claim by you. Do not apply a shipper free-time table unless they gave that file. Starter / guess until they teach this shop.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: detention
steps:
  - id: times
    needs: []
    produces: dwell-raw
    produce_path: work/dwell.csv
    tool: docs/tools/route-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/dwell.csv stop arrive depart
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [dwell-raw]
    produces: dwell-pack
    produce_path: out/detention.md
    tool: docs/tools/site-file.md
    check: python docs/tools/checks/file-exists.py out/detention.md
    on_fail: retry
    next: []
```
