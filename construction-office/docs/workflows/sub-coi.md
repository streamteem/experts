# Sub and COI watch

Roster plus certificate dates they already track. Flag missing or past dates. Do not invent insurance, type in force, or decide additional-insured wording is enough. Copy named insured and expirations as the PDF shows. A company on last week's daily is not automatically on this roster. Missing endorsement pages are missing pages. The flag file is a date compare, not a legal opinion. The pack lists who is on their sheet and which certificates need their broker or sub to refresh.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: sub-coi
steps:
  - id: roster
    needs: []
    produces: subs
    produce_path: work/sub-roster.csv
    tool: docs/tools/sub-roster.md
    check: python docs/tools/checks/csv-has-columns.py work/sub-roster.csv company trade
    on_fail: retry
    next: [flag]
  - id: flag
    needs: [subs]
    produces: coi-flags
    produce_path: work/coi-flags.csv
    tool: docs/tools/sub-roster.md
    check: python docs/tools/checks/csv-has-columns.py work/coi-flags.csv company flag
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [coi-flags]
    produces: coi-pack
    produce_path: out/sub-coi.md
    tool: docs/tools/sub-roster.md
    check: python docs/tools/checks/file-exists.py out/sub-coi.md
    on_fail: retry
    next: []
```
