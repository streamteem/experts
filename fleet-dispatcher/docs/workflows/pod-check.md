# POD yes/no

Match required stops to files in the POD folder. Unreadable images are questions. Use their signature-required flag; do not demand ink on a no-sig drop. Presence is file name yes/no, not a handwriting or porch analysis. Do not add coordinates to a photo. Ask when a required file is missing. Starter / guess until they teach this shop. If the required flag is missing on the stop row, ask before you mark a miss. Do not invent proof.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: pod-check
steps:
  - id: stops
    needs: []
    produces: pod-stops
    produce_path: work/pod-required.csv
    tool: docs/tools/route-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/pod-required.csv stop pod_required
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [pod-stops]
    produces: pod-pack
    produce_path: out/pod-check.md
    tool: docs/tools/pod-folder.md
    check: python docs/tools/checks/file-exists.py out/pod-check.md
    on_fail: retry
    next: []
```
