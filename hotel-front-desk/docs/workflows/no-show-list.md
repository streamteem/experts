# No-show list

Build the no-show list from arrivals that did not check in and from the night-audit PDF if it already coded them. Fees follow their cancellation and guarantee policy only. Do not invent a charge or run a card. Cancelled rows are not no-shows. Group no-shows use the block file when it speaks. They post. You deliver the list and write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: no-show-list
steps:
  - id: arr
    needs: []
    produces: arrivals
    produce_path: work/arrivals.csv
    tool: docs/tools/arrivals-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/arrivals.csv confirmation status
    on_fail: retry
    next: [audit]
  - id: audit
    needs: [arrivals]
    produces: audit
    produce_path: work/night-audit.pdf
    tool: docs/tools/night-audit-pdf.md
    check: python docs/tools/checks/file-exists.py work/night-audit.pdf
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [arrivals, audit]
    produces: noshow-pack
    produce_path: out/no-show-list.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/no-show-list.md
    on_fail: retry
    next: []
```
