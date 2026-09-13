# Credit card coding pack

Import one card statement period, code lines to their accounts or labeled guesses, and flag personal-looking charges and missing receipts. Produce raw, coded (date, amount, category), and a write-up. The payment from the operating bank is a transfer that reduces the card, not a second expense. Ask every card they use. No full card numbers in files you write. Do not pay the card. Do not treat the card as a bank. Reconcile the statement ending balance if they asked for a rec. Starter categories are guesses until they teach the vendor map.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: credit-card-code
steps:
  - id: card-import
    needs: []
    produces: card-raw
    produce_path: work/card-raw.csv
    tool: docs/tools/credit-card-csv.md
    check: python docs/tools/checks/file-exists.py work/card-raw.csv
    on_fail: retry
    next: [card-code]
  - id: card-code
    needs: [card-raw]
    produces: card-coded
    produce_path: work/card-coded.csv
    tool: docs/tools/credit-card-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/card-coded.csv date amount category
    on_fail: retry
    next: [card-pack]
  - id: card-pack
    needs: [card-coded]
    produces: card-writeup
    produce_path: out/card-coding.md
    tool: docs/tools/credit-card-csv.md
    check: python docs/tools/checks/file-exists.py out/card-coding.md
    on_fail: retry
    next: []
```
