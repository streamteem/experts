# One RO write-up

One ticket write-up: concern in customer words, vehicle fields from their RO, parts file from confirmations, estimate questions from their labor matrix. Cause and correction only if the tech file has them. No invented diagnosis, VIN, book time, or auth. Keep declined lines. MPI only from their form. Phone approval only from their log. Independent and dealer packs follow the same completeness idea. Ask when a needed file is missing rather than filling the three C's from memory.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: one-ro
steps:
  - id: parts
    needs: []
    produces: ro-parts
    produce_path: work/ro-parts.csv
    tool: docs/tools/parts-counter.md
    check: python docs/tools/checks/csv-has-columns.py work/ro-parts.csv part status
    on_fail: retry
    next: [notes]
  - id: notes
    needs: [ro-parts]
    produces: ro-notes
    produce_path: work/ro-notes.md
    tool: docs/tools/ro-pdf.md
    check: python docs/tools/checks/file-exists.py work/ro-notes.md
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [ro-notes]
    produces: ro-writeup
    produce_path: out/ro-writeup.md
    tool: docs/tools/ro-pdf.md
    check: python docs/tools/checks/file-exists.py out/ro-writeup.md
    on_fail: retry
    next: []
```
