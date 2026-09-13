# Preflight completeness

Run their checklist only against files in the proof or art folder: bleed, fonts, images, size, color space as they wrote. Failures become a missing-items list. Do not invent a dpi or a bleed. Do not quietly outline fonts unless that step is on the checklist. Do not give a copyright opinion because a logo failed. Write-up is pass/fail rows plus asks, not a press-ready stamp you invent.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: preflight-completeness
steps:
  - id: check
    needs: []
    produces: checklist
    produce_path: work/preflight-checklist.csv
    tool: docs/tools/preflight-checklist.md
    check: python docs/tools/checks/file-exists.py work/preflight-checklist.csv
    on_fail: retry
    next: [files]
  - id: files
    needs: [checklist]
    produces: files
    produce_path: work/proof-folder.csv
    tool: docs/tools/proof-folder.md
    check: python docs/tools/checks/file-exists.py work/proof-folder.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [checklist, files]
    produces: preflight-pack
    produce_path: out/preflight-completeness.md
    tool: docs/tools/preflight-checklist.md
    check: python docs/tools/checks/file-exists.py out/preflight-completeness.md
    on_fail: retry
    next: []
```
