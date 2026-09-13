# BEO pack

Assemble BEO pages for definite functions and attach menu prices only as printed on their menu file. Name any function that has no BEO page. Draft versus issued stays labeled. Do not invent a guarantee, a minimum, or a bar license. Diagrams and AV lists attach if those files exist; missing stays missing. They issue the packet to the floor. You deliver the completeness pack and write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: beo-pack
steps:
  - id: beos
    needs: []
    produces: beos
    produce_path: work/beos.csv
    tool: docs/tools/beo-pdf.md
    check: python docs/tools/checks/file-exists.py work/beos.csv
    on_fail: retry
    next: [menu]
  - id: menu
    needs: [beos]
    produces: menu
    produce_path: work/menu.csv
    tool: docs/tools/menu-file.md
    check: python docs/tools/checks/file-exists.py work/menu.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [beos, menu]
    produces: beo-pack
    produce_path: out/beo-pack.md
    tool: docs/tools/beo-pdf.md
    check: python docs/tools/checks/file-exists.py out/beo-pack.md
    on_fail: retry
    next: []
```
