# Board meeting files

Assemble a present-or-missing list of files for the next meeting they name: agenda, last approved minutes, financials they already produced, and exhibits they listed. They run the meeting. Minutes stay actions, not a transcript. Keep collections detail out of the open pack unless their template separates it. One meeting date and one association per index. Produce the CSV the checks can see, then the write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: board-files
steps:
  - id: list
    needs: []
    produces: board-index
    produce_path: work/board-files.csv
    tool: docs/tools/board-folder.md
    check: python docs/tools/checks/file-exists.py work/board-files.csv
    on_fail: retry
    next: [columns]
  - id: columns
    needs: [board-index]
    produces: board-cols
    produce_path: work/board-files.csv
    tool: docs/tools/board-folder.md
    check: python docs/tools/checks/csv-has-columns.py work/board-files.csv file present
    on_fail: retry
    next: [write]
  - id: write
    needs: [board-cols]
    produces: board-writeup
    produce_path: out/board-files.md
    tool: docs/tools/board-folder.md
    check: python docs/tools/checks/file-exists.py out/board-files.md
    on_fail: retry
    next: []
```
