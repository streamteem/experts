---
name: start-job
description: >-
  Before day-to-day work, open or create one items/ folder for this
  appointment, ticket, period, or pack so files do not mix. Use at the
  start of every real job.
---

# Start a work item

Day-to-day files live in **one folder per item** under `items/`. That is how this desk keeps appointments, tickets, and days from mixing.

## When

They asked for real work (a list, a pack, a write-up), dropped a file, or named an appointment / ticket / period. Run this **before** **run-map** or writing into `work/` or `out/`.

Skip only for a casual question that produces no files.

## Do

1. Read `docs/facts/how-we-file.md` (and `items/README.md`). Use **their** naming if they already taught one.
2. If `state.current_job_folder` is set and they clearly mean **that same** item, keep it. If they mean a new day, new appointment, or new ticket, do not reuse it.
3. If it is unclear which item this is, **ask** (date, time, chart/ticket/period, their id). Do not invent a person’s full name as a folder title when a chart or ticket number will do.
4. Create `items/<name>/` with `in/`, `work/`, `out/`, `evidence/` if it does not exist. Use a filesystem-safe name (letters, numbers, hyphens).
5. Put files they just dropped into **this** item’s `in/` (move or copy from a random place in the Expert folder if they left them at the top). Do not pour them into another item’s folder.
6. Set `state.current_job_folder` to that path (from the Expert root, like `items/2026-09-15-1000-chart-4412`). Set `current_job_label` in their words. Clear `artifacts` and `steps_passed` when this is a **new** item so yesterday’s files are not treated as this item’s.
7. Add or update a row in `items/INDEX.md`.
8. **journal-keeper**. Then continue with **run-map** or the work they asked.

## Do not

- Write new day-to-day outputs into the top-level `work/` or `out/` folders.
- Mix two appointments, two tickets, or two books periods in one item folder unless they asked for a named combined pack (for example one day list).
- Name a folder with a full SSN, card number, or extra clinical notes.
- Reuse yesterday’s folder because it is convenient.
