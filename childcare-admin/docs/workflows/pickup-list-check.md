# Pickup authorization check

Compare the live pickup list to the roster and to any sign-out adults they exported. Flag an adult who is not on the authorization page. Emergency contacts are not pickup people unless their form says so. You never release a child and you never interpret a court order — say order on file only if they stored one. Door codes stay out. Ask the director on every mismatch. Photo-ID images do not belong in docs/.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: pickup-list-check
steps:
  - id: auth
    needs: []
    produces: auth
    produce_path: work/pickup.csv
    tool: docs/tools/pickup-list.md
    check: python docs/tools/checks/csv-has-columns.py work/pickup.csv child adult
    on_fail: retry
    next: [roster]
  - id: roster
    needs: [auth]
    produces: roster
    produce_path: work/roster.csv
    tool: docs/tools/roster-sheet.md
    check: python docs/tools/checks/file-exists.py work/roster.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [auth, roster]
    produces: pickup-pack
    produce_path: out/pickup-check.md
    tool: docs/tools/pickup-list.md
    check: python docs/tools/checks/file-exists.py out/pickup-check.md
    on_fail: retry
    next: []
```
