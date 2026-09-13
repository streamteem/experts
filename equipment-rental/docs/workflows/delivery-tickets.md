# Delivery ticket pack

List today’s delivery and pickup tickets with zone lookup from their zone sheet. Do not invent miles, a zone letter, or an ETA. Missing site address is an ask. After-hours flags copy from the ticket or hours file. Gate codes stay out of the pack. Maintenance-due units still on the truck list are conflicts. You do not pay the hauler. Produce the run list and exception write-up. They dispatch.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: delivery-tickets
steps:
  - id: tix
    needs: []
    produces: tickets
    produce_path: work/delivery-tickets.csv
    tool: docs/tools/delivery-ticket-folder.md
    check: python docs/tools/checks/file-exists.py work/delivery-tickets.csv
    on_fail: retry
    next: [zone]
  - id: zone
    needs: [tickets]
    produces: zones
    produce_path: work/zones.csv
    tool: docs/tools/zone-sheet.md
    check: python docs/tools/checks/file-exists.py work/zones.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [tickets, zones]
    produces: del-pack
    produce_path: out/delivery-tickets.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/delivery-tickets.md
    on_fail: retry
    next: []
```
