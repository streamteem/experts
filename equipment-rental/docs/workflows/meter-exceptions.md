# Meter exceptions

Compare meter or telematics export to fleet and inspection hours. Flag blanks, return below outgoing, and GPS-versus-gauge disagreements. Do not invent a reading and do not diagnose a rolled meter. Overage math waits for their allowance file and both real readings. Portal passwords stay out. Produce the exception list and write-up. They re-read the unit or they accept a photo as the record if that is their rule.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: meter-exceptions
steps:
  - id: meter
    needs: []
    produces: meters
    produce_path: work/meters.csv
    tool: docs/tools/meter-export.md
    check: python docs/tools/checks/csv-has-columns.py work/meters.csv unit
    on_fail: retry
    next: [fleet]
  - id: fleet
    needs: [meters]
    produces: fleet
    produce_path: work/fleet.csv
    tool: docs/tools/fleet-csv.md
    check: python docs/tools/checks/file-exists.py work/fleet.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [meters, fleet]
    produces: meter-pack
    produce_path: out/meter-exceptions.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/meter-exceptions.md
    on_fail: retry
    next: []
```
