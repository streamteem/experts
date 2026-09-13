# Photo index

Index the photo folder with their file names and required angles if they stored a shot list. Do not invent a photo. Do not hide prior-damage or personal-items shots. Missing required names stay missing. Write-up is an index plus asks, not a hidden-damage diagnosis and not an MPI. You do not rename away their claim or stage meaning unless they asked.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: photo-index
steps:
  - id: photos
    needs: []
    produces: photos
    produce_path: work/photo-index.csv
    tool: docs/tools/photo-folder.md
    check: python docs/tools/checks/csv-has-columns.py work/photo-index.csv name
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [photos]
    produces: photo-pack
    produce_path: out/photo-index.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/photo-index.md
    on_fail: retry
    next: []
```
