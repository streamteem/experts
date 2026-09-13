---
name: remember
description: >-
  Store a durable fact, rule, or tool pointer in docs/ when the operator says
  remember, save this, note this, or when teach/after-task routes here.
---

# Remember

Adapted from AIDeveloper **remember**. Here it files **facts, rules, or tools** — not facts only. No vector store. The INDEX is how we find it later.

## When

Operator (or **teach** / **after-task**) has something that must survive this chat.

## Do

1. Choose **kind**: `fact` (what is true here), `rule` (when / never), `tool` (how they use an app, file, or URL).
2. Infer a short **topic** (lowercase).
3. Open the matching INDEX (`docs/facts/INDEX.md`, `docs/rules/INDEX.md`, or `docs/tools/INDEX.md`).
   - Topic exists → append to that file.
   - New topic → create `docs/<kind>/<topic>.md` and add an INDEX row (topic, file, keywords).
   - Unsure → `captured.md` for that kind.
4. Append:

```markdown
---
date: YYYY-MM-DD
label: Short label
kind: fact | rule | tool
topics: [topic]
---

(Content. Keep their wording. Preserve links.)
```

5. Tell the operator the path. If this contradicts an existing entry, run **conflict-check** first.

**Not this skill:** decisions and Q&A → **journal-keeper**. Repeated full workflows → **playbook-keeper**.
