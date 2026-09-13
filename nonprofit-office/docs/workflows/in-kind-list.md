# In-kind log list

List in-kind rows from their log: date, donor label, description they wrote, program tag. No fair-market values and no wage for time. Point unusual items (vehicles, real estate, art, crypto) at their gift-acceptance policy and stop. Do not complete an appraisal or tell the donor what to deduct. Volunteer hours stay on the volunteer log unless their files already treat hours as in-kind. Blank descriptions are questions, not rows you finish from a photo guess. Output is the working log extract and a write-up of holes. They accept gifts. You list.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: in-kind-list
steps:
  - id: pull
    needs: []
    produces: inkind
    produce_path: work/inkind.csv
    tool: docs/tools/in-kind-log.md
    check: python docs/tools/checks/file-exists.py work/inkind.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [inkind]
    produces: inkind-out
    produce_path: out/inkind.md
    tool: docs/tools/in-kind-log.md
    check: python docs/tools/checks/file-exists.py out/inkind.md
    on_fail: retry
    next: []
```
