# Proof-status list

List each open ticket's proof type and status from the export, then confirm a matching PDF or hard-proof slip in the folder. Quote disagreements. Do not invent approved. Do not send a job to press on a missing required proof. Waive only if their rule is in the folder. Write-up is a status list plus missing-proof asks, not a copyright opinion on the art.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: proof-status
steps:
  - id: status
    needs: []
    produces: status
    produce_path: work/proof-status.csv
    tool: docs/tools/proof-status-export.md
    check: python docs/tools/checks/csv-has-columns.py work/proof-status.csv job status
    on_fail: retry
    next: [folder]
  - id: folder
    needs: [status]
    produces: proofs
    produce_path: work/proof-folder.csv
    tool: docs/tools/proof-folder.md
    check: python docs/tools/checks/file-exists.py work/proof-folder.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [status, proofs]
    produces: proof-pack
    produce_path: out/proof-status.md
    tool: docs/tools/proof-status-export.md
    check: python docs/tools/checks/file-exists.py out/proof-status.md
    on_fail: retry
    next: []
```
