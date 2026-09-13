# Reserve-study file index

Confirm the reserve-study PDF is present, copy the report date and association name on the cover, and copy any printed number they asked for. Not an engineering restamp and not a cash transfer. A missing or unexpectedly old study is a question for the board. One association per index. Produce the CSV the checks can see, then the write-up. Do not add or delete components, and do not move operating cash into reserves.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: reserve-index
steps:
  - id: index
    needs: []
    produces: rs-raw
    produce_path: work/reserve-index.csv
    tool: docs/tools/reserve-study-pdf.md
    check: python docs/tools/checks/file-exists.py work/reserve-index.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [rs-raw]
    produces: rs-writeup
    produce_path: out/reserve-index.md
    tool: docs/tools/reserve-study-pdf.md
    check: python docs/tools/checks/file-exists.py out/reserve-index.md
    on_fail: retry
    next: []
```
