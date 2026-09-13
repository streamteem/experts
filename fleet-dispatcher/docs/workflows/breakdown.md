# Breakdown write-up

Unit down from their exception or GPS export. Location only if the file has it — no invented mile marker. Who they called only if they logged it. No out-of-service ruling and no tow ETA you invent. Put this write-up ahead of routine lates when you also touch the exception pack. Starter / guess until they teach this shop. If GPS and the exception log disagree on place or time, list both. No OOS language you chose.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: breakdown
steps:
  - id: pull
    needs: []
    produces: brk-raw
    produce_path: work/breakdown.csv
    tool: docs/tools/exception-log.md
    check: python docs/tools/checks/csv-has-columns.py work/breakdown.csv unit time
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [brk-raw]
    produces: brk-pack
    produce_path: out/breakdown.md
    tool: docs/tools/gps-export.md
    check: python docs/tools/checks/file-exists.py out/breakdown.md
    on_fail: retry
    next: []
```
