# Tuition list from their file

Build a tuition or past-due list only from their rate sheet and ledger export. Quote the rate that matches the child’s schedule on the contract. Do not invent a weekly number, sibling percent, or late fee. You never send money or store a card. Subsidy copays stay on the authorization file if they split them. NSF rows keep their code. Year-end paid totals use the paid column only. If contract and rate sheet disagree, quote both and ask.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: tuition-from-file
steps:
  - id: rates
    needs: []
    produces: rates
    produce_path: work/tuition.csv
    tool: docs/tools/tuition-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/tuition.csv child rate
    on_fail: retry
    next: [grid]
  - id: grid
    needs: [rates]
    produces: grid
    produce_path: work/tuition-list.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py work/tuition-list.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [rates, grid]
    produces: tuition-pack
    produce_path: out/tuition-from-file.md
    tool: docs/tools/tuition-sheet.md
    check: python docs/tools/checks/file-exists.py out/tuition-from-file.md
    on_fail: retry
    next: []
```
