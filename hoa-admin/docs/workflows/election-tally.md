# Election tally from their roster

Count from the roster and ballot or proxy files they provide. Label the product a tally, not a certified election. List missing signatures and unmarked choices as questions. Do not rule on proxy validity or announce a legal winner. Do not publish how a named lot voted. One meeting and one association per tally. Produce the CSV the checks can see, then the write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: election-tally
steps:
  - id: roster
    needs: []
    produces: roster
    produce_path: work/roster.csv
    tool: docs/tools/roster-csv.md
    check: python docs/tools/checks/file-exists.py work/roster.csv
    on_fail: retry
    next: [tally]
  - id: tally
    needs: [roster]
    produces: tally-raw
    produce_path: work/election-tally.csv
    tool: docs/tools/roster-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/election-tally.csv candidate votes
    on_fail: retry
    next: [write]
  - id: write
    needs: [tally-raw]
    produces: tally-writeup
    produce_path: out/election-tally.md
    tool: docs/tools/roster-csv.md
    check: python docs/tools/checks/file-exists.py out/election-tally.md
    on_fail: retry
    next: []
```
