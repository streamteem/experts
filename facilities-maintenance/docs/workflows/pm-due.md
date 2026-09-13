# PM due list

List PMs due or overdue from their PM calendar, then join the asset list for location and criticality they stored. Never invent an interval or a next-due. Meter-based rows stay meter-based if that is how they filed them. Do not mark a PM complete from a photo. Write-up is a due list plus missing-plan asks, not an OSHA-compliant PM stamp and not a production dispatch rewrite.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: pm-due
steps:
  - id: calendar
    needs: []
    produces: pm-cal
    produce_path: work/pm-calendar.csv
    tool: docs/tools/pm-calendar.md
    check: python docs/tools/checks/csv-has-columns.py work/pm-calendar.csv asset next-due
    on_fail: retry
    next: [assets]
  - id: assets
    needs: [pm-cal]
    produces: assets
    produce_path: work/asset-list.csv
    tool: docs/tools/asset-list.md
    check: python docs/tools/checks/file-exists.py work/asset-list.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [pm-cal, assets]
    produces: pm-due
    produce_path: out/pm-due.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/pm-due.md
    on_fail: retry
    next: []
```
