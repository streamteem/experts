# Pickup authorization list

Build or check today’s pickup list against the occupancy file. Names as spelled. Flag people not on the list. Emergency contacts are not pickup unless the card says so. You never release a dog. If card and software disagree, quote both. Do not add a same-day name from a phone vibe. A complete CSV is still not a release you perform. Starter / guess until they teach ID-at-door rules and same-day adds.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: pickup-list
steps:
  - id: auth
    needs: []
    produces: auth
    produce_path: work/pickup-auth.csv
    tool: docs/tools/pickup-list.md
    check: python docs/tools/checks/csv-has-columns.py work/pickup-auth.csv patient name
    on_fail: retry
    next: [occ]
  - id: occ
    needs: [auth]
    produces: occ
    produce_path: work/boarding.csv
    tool: docs/tools/boarding-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/boarding.csv patient stay
    on_fail: retry
    next: [write]
  - id: write
    needs: [auth, occ]
    produces: pickup-pack
    produce_path: out/pickup-list.md
    tool: docs/tools/pickup-list.md
    check: python docs/tools/checks/file-exists.py out/pickup-list.md
    on_fail: retry
    next: []
```
