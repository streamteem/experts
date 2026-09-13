# Key-log completeness

Match issued key-ids on the key log to sites on the site list. Flag out-without-in and sites with no key row if their process requires one. Never copy a key or store a combination or alarm code. Contract-end returned lists use the issued set they stored. Write-up is outstanding rings plus questions. They collect hardware. You pack the gaps. Badge rows stay on this pack only if they keep badges on the same log.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: key-log-completeness
steps:
  - id: keys
    needs: []
    produces: keys
    produce_path: work/key-log.csv
    tool: docs/tools/key-log.md
    check: python docs/tools/checks/csv-has-columns.py work/key-log.csv site key
    on_fail: retry
    next: [sites]
  - id: sites
    needs: [keys]
    produces: sites
    produce_path: work/key-sites.csv
    tool: docs/tools/site-list.md
    check: python docs/tools/checks/file-exists.py work/key-sites.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [keys, sites]
    produces: key-pack
    produce_path: out/key-log.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/key-log.md
    on_fail: retry
    next: []
```
