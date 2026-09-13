# Day-close tender

From their close report or drawer sheet, list tender types and amounts they recorded for one clinic date. Split exam versus optical collections if their close report does. Do not store PAN or check account numbers. Do not send a deposit or mark a bill paid. Short-or-over versus their expected total is a flag from their math, not a silent fix. Copay posted amounts, if compared, come from their fee or posted-copay file — do not invent expected collect. Insurance posting is not tender. One location unless they asked.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: day-close
steps:
  - id: close
    needs: []
    produces: close
    produce_path: work/day-close.csv
    tool: docs/tools/ehr-export.md
    check: python docs/tools/checks/file-exists.py work/day-close.csv
    on_fail: retry
    next: [fees]
  - id: fees
    needs: [close]
    produces: fees
    produce_path: work/posted-copay.csv
    tool: docs/tools/fee-file.md
    check: python docs/tools/checks/file-exists.py work/posted-copay.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [close, fees]
    produces: close-writeup
    produce_path: out/day-close.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/day-close.md
    on_fail: retry
    next: []
```
