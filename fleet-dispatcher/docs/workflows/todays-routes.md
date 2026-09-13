# Today's routes

Stops and missing PODs from their sheet for one service date. Sequence stays theirs unless they asked for a labeled draft. Pull the route export into the work CSV, then write the pack the checks can see. Do not invent addresses, windows, or a second day’s stops. POD presence is yes/no from their process and folder, not a signature you invent. Starter / guess until they teach this shop.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: todays-routes
steps:
  - id: pull
    needs: []
    produces: routes
    produce_path: work/routes.csv
    tool: docs/tools/route-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/routes.csv route stop date
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [routes]
    produces: route-pack
    produce_path: out/routes.md
    tool: docs/tools/route-sheet.md
    check: python docs/tools/checks/file-exists.py out/routes.md
    on_fail: retry
    next: []
```
