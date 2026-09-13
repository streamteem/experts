# Gift-card and package list

From their gift-card export, list sales, redemptions, and remaining balances using last-four or internal IDs only. No full card numbers. Liability is not the same as today’s service revenue. Do not invent a remaining balance. Packages stay on their own lines if the export splits them. You do not issue or refund. They handle guest questions. Starter until they teach this shop’s gift-card report.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: gift-card-recon
steps:
  - id: pull
    needs: []
    produces: gc
    produce_path: work/gift-cards.csv
    tool: docs/tools/gift-card-export.md
    check: python docs/tools/checks/file-exists.py work/gift-cards.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [gc]
    produces: gc-pack
    produce_path: out/gift-cards.md
    tool: docs/tools/gift-card-export.md
    check: python docs/tools/checks/file-exists.py out/gift-cards.md
    on_fail: retry
    next: []
```
