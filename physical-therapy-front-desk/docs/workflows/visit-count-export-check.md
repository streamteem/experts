# Visit-count export check

Compare their visit-count export to the auth tracker for the charts they named. List mismatches of used, authorized, or remaining as questions. Do not pick a winner and do not invent a remaining number to tidy the sheet. Do not apply KX or timed units. If either file is stale or undated, ask before you treat counts as current. Prefer chart and auth id. Produce the exception CSV plus a write-up. They correct the live tracker.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: visit-count-export-check
steps:
  - id: counts
    needs: []
    produces: counts
    produce_path: work/visit-counts.csv
    tool: docs/tools/visit-count-export.md
    check: python docs/tools/checks/csv-has-columns.py work/visit-counts.csv chart used
    on_fail: retry
    next: [auth]
  - id: auth
    needs: [counts]
    produces: auth
    produce_path: work/auth-tracker.csv
    tool: docs/tools/auth-tracker.md
    check: python docs/tools/checks/file-exists.py work/auth-tracker.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [counts, auth]
    produces: count-writeup
    produce_path: out/visit-counts.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/visit-counts.md
    on_fail: retry
    next: []
```
