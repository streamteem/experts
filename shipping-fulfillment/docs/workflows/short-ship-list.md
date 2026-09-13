# Short-ship list

From pick versus pack, list orders where packed qty is less than ordered or picked qty they still wanted. Say short. Do not write shipped-complete. Remaining qty stays visible for backorder or cancel — they decide. Do not invent a packed qty to tidy the board. This is outbound, not a receiving short. They tell the customer or release a later backorder ship.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: short-ship-list
steps:
  - id: picks
    needs: []
    produces: picks
    produce_path: work/picks.csv
    tool: docs/tools/pick-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/picks.csv order sku qty
    on_fail: retry
    next: [packs]
  - id: packs
    needs: [picks]
    produces: packs
    produce_path: work/packs.csv
    tool: docs/tools/pack-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/packs.csv order sku qty
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [picks, packs]
    produces: short-pack
    produce_path: out/short-ships.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/short-ships.md
    on_fail: retry
    next: []
```
