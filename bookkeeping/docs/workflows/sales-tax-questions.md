# Sales tax questions pack

From their invoice or POS file, list tax collected as they marked. Produce raw sales, a tax-collected CSV with date, amount, and tax_collected, and a questions pack. Ask nexus, rates, item taxability, filing frequency, and who files. Never invent a rate or jurisdiction. Never say a return is filed. Never remake a return. Marketplace payouts may mean the platform remitted; ask. Starter work is a list of collected amounts from their file only. Streamlined Sales Tax orientation does not give this shop a rate. Filing stays with them or their CPA.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: sales-tax-questions
steps:
  - id: sales-file
    needs: []
    produces: sales-raw
    produce_path: work/sales-raw.csv
    tool: docs/tools/sales-tax-sheet.md
    check: python docs/tools/checks/file-exists.py work/sales-raw.csv
    on_fail: retry
    next: [tax-listed]
  - id: tax-listed
    needs: [sales-raw]
    produces: tax-collected
    produce_path: work/tax-collected.csv
    tool: docs/tools/sales-tax-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/tax-collected.csv date amount tax_collected
    on_fail: retry
    next: [tax-ask]
  - id: tax-ask
    needs: [tax-collected]
    produces: sales-tax-ask
    produce_path: out/sales-tax-questions.md
    tool: docs/tools/sales-tax-sheet.md
    check: python docs/tools/checks/file-exists.py out/sales-tax-questions.md
    on_fail: retry
    next: []
```
