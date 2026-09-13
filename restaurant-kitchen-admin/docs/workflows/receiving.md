# Receiving questions

Receiving log or marked ticket versus the invoice. Credits are drafted as questions from their short, damage, or reject notes plus the invoice line. No invented reject temperatures as law. No invented credit dollars. They submit the credit. If they have no receiving log, say the pack is invoice-only and ask. Catch-weight scale versus ticket weight is a question when both exist. You do not reject the truck in the write-up. Spec subs stay questions.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: receiving
steps:
  - id: recv
    needs: []
    produces: recv-raw
    produce_path: work/receiving.csv
    tool: docs/tools/receiving-log.md
    check: python docs/tools/checks/csv-has-columns.py work/receiving.csv item qty
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [recv-raw]
    produces: recv-pack
    produce_path: out/receiving.md
    tool: docs/tools/invoice-pdf.md
    check: python docs/tools/checks/file-exists.py out/receiving.md
    on_fail: retry
    next: []
```
