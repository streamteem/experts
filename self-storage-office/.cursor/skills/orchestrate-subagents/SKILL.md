---
name: orchestrate-subagents
description: >-
  Start an extra worker with only the files listed in journal state. This chat
  merges results and owns the journal. Use for a long search or a long write-up.
---

# Extra workers

Keep it small.

## When

**read-saved-files** needs a wide search, or a write-up is large enough to split (e.g. one worker reads quotes, this chat writes the write-up).

## Do

1. Read `allowed_reads` from `journal/state.json`.
2. Start a worker with **only** those paths. Tell it not to edit `journal/` or INDEX files.
3. Merge the result. This chat runs **journal-keeper** / **remember** if something must be saved.
4. Do not let a worker invent how this business works if it is not in the saved files.
