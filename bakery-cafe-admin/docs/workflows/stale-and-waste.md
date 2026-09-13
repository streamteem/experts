# Stales and waste recap

Recap their waste and stale logs for the dates they named, next to case par if they asked why the case overbaked. Do not invent waste or stales. Do not hide stales inside a par cut. Do not relabel as donation. Do not write theft. Patterns are questions for mix or par. Write-up is the recap plus asks. They change the plan.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: stale-and-waste
steps:
  - id: logs
    needs: []
    produces: logs
    produce_path: work/waste-stales.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py work/waste-stales.csv
    on_fail: retry
    next: [pars]
  - id: pars
    needs: [logs]
    produces: case-par
    produce_path: work/case-par.csv
    tool: docs/tools/case-par-sheet.md
    check: python docs/tools/checks/file-exists.py work/case-par.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [logs, case-par]
    produces: stale-pack
    produce_path: out/stale-and-waste.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/stale-and-waste.md
    on_fail: retry
    next: []
```
