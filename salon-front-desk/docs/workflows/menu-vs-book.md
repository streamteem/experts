# Menu vs book check

Compare services on the day’s book to the menu file. Flag names or prices that do not appear on the menu. Do not invent a price to match the ticket. Quote print versus POS if they disagree. Add-ons need a menu row. Duration mismatches are flags, not a reason to shorten a color slot. They decide which file wins today. You do not rewrite the live menu. Starter until they teach the current menu file.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: menu-vs-book
steps:
  - id: menu
    needs: []
    produces: menu
    produce_path: work/menu.csv
    tool: docs/tools/service-menu-file.md
    check: python docs/tools/checks/file-exists.py work/menu.csv
    on_fail: retry
    next: [book]
  - id: book
    needs: [menu]
    produces: book
    produce_path: work/book.csv
    tool: docs/tools/booking-export.md
    check: python docs/tools/checks/file-exists.py work/book.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [menu, book]
    produces: menu-pack
    produce_path: out/menu-vs-book.md
    tool: docs/tools/service-menu-file.md
    check: python docs/tools/checks/file-exists.py out/menu-vs-book.md
    on_fail: retry
    next: []
```
