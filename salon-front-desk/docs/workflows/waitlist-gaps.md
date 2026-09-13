# Waitlist and open-chair gaps

List open slots the hours file says are workable, plus waitlist names from their export. They call. Do not confirm a waitlist person onto the book. Processing buffers are not open unless the export marks them free. Pending requests are not waitlist confirmed. Do not message the list as a product. Do not invent turn order. Hours file beats a widget hole on a closed day. Starter until they teach this floor’s waitlist order.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: waitlist-gaps
steps:
  - id: book
    needs: []
    produces: book
    produce_path: work/book.csv
    tool: docs/tools/booking-export.md
    check: python docs/tools/checks/file-exists.py work/book.csv
    on_fail: retry
    next: [wait]
  - id: wait
    needs: [book]
    produces: wait
    produce_path: work/waitlist.csv
    tool: docs/tools/booking-export.md
    check: python docs/tools/checks/file-exists.py work/waitlist.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [book, wait]
    produces: gap-pack
    produce_path: out/waitlist-gaps.md
    tool: docs/tools/booking-export.md
    check: python docs/tools/checks/file-exists.py out/waitlist-gaps.md
    on_fail: retry
    next: []
```
