# Restricted funds ASK list

From the gifts or bank-coding sheet and the bookkeeper’s fund or class export, list rows with no fund code, ambiguous restriction language (“for the kids”), grant leftovers, or board-designated labels that someone called restricted. Ask the bookkeeper. Do not spend them in a narrative, invoice, or liquidity note. Quote the gift words or award clause next to each question. If the restricted-fund sheet is missing, the whole pack is an ASK list, not a spend plan. Their codes win after they teach. You do not post a release or a reclass.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: restricted-ask
steps:
  - id: pull
    needs: []
    produces: funds
    produce_path: work/funds.csv
    tool: docs/tools/restricted-fund-sheet.md
    check: python docs/tools/checks/file-exists.py work/funds.csv
    on_fail: retry
    next: [gifts]
  - id: gifts
    needs: [funds]
    produces: gifts
    produce_path: work/gifts.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py work/gifts.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [funds, gifts]
    produces: ask-pack
    produce_path: out/restricted-ask.md
    tool: docs/tools/restricted-fund-sheet.md
    check: python docs/tools/checks/file-exists.py out/restricted-ask.md
    on_fail: retry
    next: []
```
