# Waste recap

Waste from their log for the dates they name, using their reason codes and units. Patterns (same item several times) are questions for pars or batch size, not people-blame unless they asked. No invented spoilage to close a food-cost hole. Do not write theft. Compost or oil tickets are not this recap unless they taught that mapping. Missing log or blank reasons: ask. Staff meal and donation stay on those logs if separate. Date range stays the range they asked for.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: waste-week
steps:
  - id: pull
    needs: []
    produces: waste-raw
    produce_path: work/waste.csv
    tool: docs/tools/waste-log.md
    check: python docs/tools/checks/csv-has-columns.py work/waste.csv item qty reason
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [waste-raw]
    produces: waste-pack
    produce_path: out/waste.md
    tool: docs/tools/waste-log.md
    check: python docs/tools/checks/file-exists.py out/waste.md
    on_fail: retry
    next: []
```
