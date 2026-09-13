---
name: continue
description: >-
  Resume from journal/state.json when they say continue, resume, or pick up
  where we left off. Continue is not a yes and not an answer. Walks one ready
  work-map step when a map is active.
---

# Continue

## When

They say continue / resume / start where we left off.

## Do

1. Read `journal/state.json` and `journal/progress.md`.
2. If `blocking_questions` is non-empty → ask those. Stop. Continue is not an answer.
3. If `next_action` is `define-role` → that skill.
4. If `active_map` is set (or `next_action` is a named workflow) → **read-saved-files** then **run-map** for **one ready step**. Then **journal-keeper**.
5. If `next_action` is empty or done → ask what they want next.
6. **journal-keeper** after the one step.

One step per continue unless they asked to run a whole named job (then **run-map** until the map is complete or blocked).
