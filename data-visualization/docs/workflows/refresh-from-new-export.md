# Refresh from a new export

Read a new CSV with the same columns they already named. Write a dated PNG and a write-up that compares old file name versus new file name, row counts, and date ranges — not growth you invented. If columns changed, stop and ask. Do not scrape. Keep the prior PNG unless they said replace. Same filters as last pack. Version the source names in the markdown.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: refresh-from-new-export
steps:
  - id: newfile
    needs: []
    produces: newfile
    produce_path: work/refresh-new.csv
    tool: docs/tools/csv-folder.md
    check: python docs/tools/checks/file-exists.py work/refresh-new.csv
    on_fail: retry
    next: [chart]
  - id: chart
    needs: [newfile]
    produces: png
    produce_path: out/refresh-dated.png
    tool: docs/tools/matplotlib.md
    check: python docs/tools/checks/file-exists.py out/refresh-dated.png
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [png]
    produces: writeup
    produce_path: out/refresh-from-new-export.md
    tool: docs/tools/python.md
    check: python docs/tools/checks/file-exists.py out/refresh-from-new-export.md
    on_fail: retry
    next: []
```
