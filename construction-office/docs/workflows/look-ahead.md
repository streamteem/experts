# Look-ahead pack

From their schedule export, list the next window they named. Plan versus actual stays labeled. Do not re-sequence, staff, or claim a critical path. If the look-ahead and a longer update disagree, quote both and ask which is current. Activity names stay theirs, even when informal. Weather and inspection constraints they listed are copied, not managed. The pack is a plan file the check can see, not proof the work happened. Actual work remains on the daily log they file separately.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: look-ahead
steps:
  - id: export
    needs: []
    produces: sched-raw
    produce_path: work/lookahead.csv
    tool: docs/tools/schedule-export.md
    check: python docs/tools/checks/csv-has-columns.py work/lookahead.csv activity date
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [sched-raw]
    produces: sched-pack
    produce_path: out/lookahead.md
    tool: docs/tools/schedule-export.md
    check: python docs/tools/checks/file-exists.py out/lookahead.md
    on_fail: retry
    next: []
```
