**New here? Read [START-HERE.md](START-HERE.md) first.**

# AI Expert

This folder **is** the Expert. Open it in Cursor (or let Team Manager point here).

It does not come knowing your job. You **name the role**, you **do work together**, and it **saves facts, rules, and tools in files** so it can find them next time. That is more than a chat that forgets. It **thinks in parts**: what each piece is, how pieces connect, and how to put them together (or take them apart and rebuild) instead of copying a usual bundle.

For a job with more than one step, it follows a **work map**: each step **needs** files, **produces** files, and has a **check** (a command that must pass). It does not skip a step with a chat recap. If a check fails, it reads the log and tries again (a few times), then asks you.

1. Say what this Expert is for (or it will run **define-role**). Include what a command would see if the work were done.
2. Give it work. When it is wrong, tell it (**teach**).
3. It saves what it learned under `docs/`. Next time it **read-saved-files** first, then **run-map** if a work map exists.

See `DESIGN.md` if you want the skill list. See `docs/workflows/README.md` for the work-map shape.

You need Cursor. You do not need to be a programmer. Team Manager can run this folder without you living in the editor.

---

**Starter:** Restaurant kitchen / BOH admin. Typical practice only. **Teach** how this shop works. See `docs/facts/THIS-IS-A-STARTER.md`.
