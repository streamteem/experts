# Receipts to card or bank

Index receipt files for one period and match them to card or bank lines. Produce the receipts index, a match sheet with date, amount, and status, and an exceptions write-up for unmatched receipts and unmatched lines. Do not invent payees. Do not treat a chat recap as the source when they promised a file. Do not copy full card numbers from photos into docs/. Ask their dollar threshold for "enough" support if they have one. Starter matches are same-date same-amount guesses labeled as guesses until they confirm. This pack supports coding and the rec; it does not pay anyone.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: receipt-match
steps:
  - id: receipts
    needs: []
    produces: receipts-index
    produce_path: work/receipts-index.csv
    tool: docs/tools/receipt-folder.md
    check: python docs/tools/checks/file-exists.py work/receipts-index.csv
    on_fail: retry
    next: [match-lines]
  - id: match-lines
    needs: [receipts-index]
    produces: receipt-match
    produce_path: work/receipt-match.csv
    tool: docs/tools/credit-card-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/receipt-match.csv date amount status
    on_fail: retry
    next: [exceptions]
  - id: exceptions
    needs: [receipt-match]
    produces: receipt-exceptions
    produce_path: out/receipt-exceptions.md
    tool: docs/tools/receipt-folder.md
    check: python docs/tools/checks/file-exists.py out/receipt-exceptions.md
    on_fail: retry
    next: []
```
