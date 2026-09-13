# Case par versus count

Compare pastry-case and bread-wall par to the count they recorded for the named daypart. Suggested pull or bake is par minus count only when both exist in the same unit. Do not invent a par or a count. Eighty-six case stays their note on top. Not a restaurant walk-in protein count. Write-up is holes plus 86-case. They count the case.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: case-par-vs-count
steps:
  - id: pars
    needs: []
    produces: case-par
    produce_path: work/case-par.csv
    tool: docs/tools/case-par-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/case-par.csv item par
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [case-par]
    produces: case-pack
    produce_path: out/case-par-vs-count.md
    tool: docs/tools/case-par-sheet.md
    check: python docs/tools/checks/file-exists.py out/case-par-vs-count.md
    on_fail: retry
    next: []
```
