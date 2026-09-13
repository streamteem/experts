# Dues aging from their file

List balances by current, thirty, sixty, and ninety-plus from their ledger export after you confirm community name and as-of date. No demand letter, no lien threat, no credit-reporting language. Late-fee math only if their policy file states the formula and they asked for arithmetic. Prepaid lots are not delinquent. One association per aging file. Produce the CSV the checks can see, then the write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: dues-aging
steps:
  - id: pull
    needs: []
    produces: dues-raw
    produce_path: work/dues-aging.csv
    tool: docs/tools/ledger-export.md
    check: python docs/tools/checks/file-exists.py work/dues-aging.csv
    on_fail: retry
    next: [columns]
  - id: columns
    needs: [dues-raw]
    produces: dues-cols
    produce_path: work/dues-aging.csv
    tool: docs/tools/ledger-export.md
    check: python docs/tools/checks/csv-has-columns.py work/dues-aging.csv lot balance
    on_fail: retry
    next: [write]
  - id: write
    needs: [dues-cols]
    produces: dues-writeup
    produce_path: out/dues-aging.md
    tool: docs/tools/ledger-export.md
    check: python docs/tools/checks/file-exists.py out/dues-aging.md
    on_fail: retry
    next: []
```
