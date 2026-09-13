# Submittal log pack

Status and aging from their submittal export. You do not approve, reject, or change for review to approved. Keep specification sections and resubmittal suffixes they used. Missing sections are asks, not guessed numbers. Shop-drawing stamps stay on the files they stored; this pack is the register, not a review. Aging uses their sent and returned dates. The write-up names the export and lists open versus returned in their words so the field and office share one list.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: submittal-aging
steps:
  - id: list
    needs: []
    produces: sub-raw
    produce_path: work/submittals.csv
    tool: docs/tools/submittal-log.md
    check: python docs/tools/checks/csv-has-columns.py work/submittals.csv number status
    on_fail: retry
    next: [age]
  - id: age
    needs: [sub-raw]
    produces: sub-aged
    produce_path: work/submittals-aged.csv
    tool: docs/tools/submittal-log.md
    check: python docs/tools/checks/csv-has-columns.py work/submittals-aged.csv number status
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [sub-aged]
    produces: sub-pack
    produce_path: out/submittals.md
    tool: docs/tools/submittal-log.md
    check: python docs/tools/checks/file-exists.py out/submittals.md
    on_fail: retry
    next: []
```
