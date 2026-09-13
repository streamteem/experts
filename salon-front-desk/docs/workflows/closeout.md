# Close-out pack

From the POS export, list sales types, tenders, tips, voids, and gift-card activity. They count cash. Do not invent a drawer total. Split booth versus employee only if the roster is on file; if a provider has no role, ask before one pile. Quote holes—missing cash column, missing tickets—without plug lines. You do not take payment or close tickets in the live POS. Starter until they teach the official close report.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: closeout
steps:
  - id: pull
    needs: []
    produces: close
    produce_path: work/close.csv
    tool: docs/tools/pos-export.md
    check: python docs/tools/checks/file-exists.py work/close.csv
    on_fail: retry
    next: [roster]
  - id: roster
    needs: [close]
    produces: roster
    produce_path: work/booth-roster.csv
    tool: docs/tools/booth-roster.md
    check: python docs/tools/checks/file-exists.py work/booth-roster.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [close, roster]
    produces: close-pack
    produce_path: out/closeout.md
    tool: docs/tools/pos-export.md
    check: python docs/tools/checks/file-exists.py out/closeout.md
    on_fail: retry
    next: []
```
