# Access-flag exceptions

Join check-ins to the access-flag export. List denies that walked, allows that the freeze log would question, and overrides they recorded. Do not rewrite the live flag. Do not invent a collections hold. Produce the exception list plus a write-up. They change access. Guests scanned as members stay on the exception list. Starter until they teach this club’s flag vocabulary.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: access-flag-exceptions
steps:
  - id: flags
    needs: []
    produces: flags
    produce_path: work/access-flags.csv
    tool: docs/tools/access-flag-export.md
    check: python docs/tools/checks/csv-has-columns.py work/access-flags.csv member_id status
    on_fail: retry
    next: [checkins]
  - id: checkins
    needs: [flags]
    produces: checkins
    produce_path: work/check-in.csv
    tool: docs/tools/check-in-csv.md
    check: python docs/tools/checks/file-exists.py work/check-in.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [flags, checkins]
    produces: access-pack
    produce_path: out/access-flag-exceptions.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/access-flag-exceptions.md
    on_fail: retry
    next: []
```
