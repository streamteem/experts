# Bid numbers comparison

Compare amounts, allowances, exclusions, and dates from bid PDFs they provided for one project. Do not pick a winner or lowest responsible bidder. Missing scope pages and vendors not on their insurance checklist are questions. Keep add-alternates labeled. One project per comparison write-up unless they asked for an index with a project column. Produce the CSV the checks can see, then the write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: bid-compare
steps:
  - id: index
    needs: []
    produces: bids-raw
    produce_path: work/bids.csv
    tool: docs/tools/bid-pdf.md
    check: python docs/tools/checks/file-exists.py work/bids.csv
    on_fail: retry
    next: [columns]
  - id: columns
    needs: [bids-raw]
    produces: bids-cols
    produce_path: work/bids.csv
    tool: docs/tools/bid-pdf.md
    check: python docs/tools/checks/csv-has-columns.py work/bids.csv vendor amount
    on_fail: retry
    next: [write]
  - id: write
    needs: [bids-cols]
    produces: bids-writeup
    produce_path: out/bid-compare.md
    tool: docs/tools/bid-pdf.md
    check: python docs/tools/checks/file-exists.py out/bid-compare.md
    on_fail: retry
    next: []
```
