# Exceptions list

Late, breakdown, failed, and missing-POD rows from the day’s files. Breakdown and safety defects first, then other codes they use. Every row needs a timestamp or saved note; do not create exceptions from memory. Use their codes. The pack lists source (log, TMS, driver note) so dispatcher commentary stays separate from driver facts. Starter / guess until they teach this shop.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: exceptions
steps:
  - id: list
    needs: []
    produces: exc
    produce_path: work/exceptions.csv
    tool: docs/tools/exception-log.md
    check: python docs/tools/checks/csv-has-columns.py work/exceptions.csv stop code time
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [exc]
    produces: exc-pack
    produce_path: out/exceptions.md
    tool: docs/tools/exception-log.md
    check: python docs/tools/checks/file-exists.py out/exceptions.md
    on_fail: retry
    next: []
```
