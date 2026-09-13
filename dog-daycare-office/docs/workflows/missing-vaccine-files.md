# Missing vaccine-file list

From their vaccine index and today’s stay list, list patient-dogs whose required pages are missing, unreadable, or the wrong dog. Present or missing only. Never decide a vaccine is due medically. Never interpret a titer. Do not paste certificate tables. Rabies pages they require are the same rule. Starter / guess until they teach which named pages this shop requires for daycare versus board.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: missing-vaccine-files
steps:
  - id: index
    needs: []
    produces: vax
    produce_path: work/vaccine-index.csv
    tool: docs/tools/vaccine-file-index.md
    check: python docs/tools/checks/csv-has-columns.py work/vaccine-index.csv patient file
    on_fail: retry
    next: [stays]
  - id: stays
    needs: [vax]
    produces: stays
    produce_path: work/boarding.csv
    tool: docs/tools/boarding-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/boarding.csv patient stay
    on_fail: retry
    next: [write]
  - id: write
    needs: [vax, stays]
    produces: vax-pack
    produce_path: out/missing-vaccine-files.md
    tool: docs/tools/vaccine-file-index.md
    check: python docs/tools/checks/file-exists.py out/missing-vaccine-files.md
    on_fail: retry
    next: []
```
