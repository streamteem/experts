# Key and fob list

Who holds what from their log. No alarm codes, lockbox pins, or passwords. Do not rekey, call a locksmith, or invent a key number. Lost or unreturned keys are flags for them. Leavers show keys still out; you do not collect. Public packs omit master lists. Fobs use the same holder columns. Starter key-board notes; they still teach this shop's IDs and whether a quarterly audit exists.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: key-audit
steps:
  - id: list
    needs: []
    produces: keys
    produce_path: work/keys.csv
    tool: docs/tools/key-log.md
    check: python docs/tools/checks/csv-has-columns.py work/keys.csv key_id holder
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [keys]
    produces: key-pack
    produce_path: out/keys.md
    tool: docs/tools/key-log.md
    check: python docs/tools/checks/file-exists.py out/keys.md
    on_fail: retry
    next: []
```
