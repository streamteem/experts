# Expert — skill design

**Updated:** 2026-09-09  
**Folder:** `experts/Expert/` — open this in Cursor. Generic Expert that learns a role (`templates.md`).

Copied from `D:\AIDeveloper` only where the *loop* is the same. Software-build skills (design docs, implement-feature, tests, git) are **not** copied.

Use ordinary words with the person. No jargon and no confusing analogies. Finished work is a **write-up**. Look in saved files before starting. Think in **parts**: what each part is, how parts connect, assemble or reassemble a solution. Do not invent missing parts. Multi-step work is a **work map**: steps with **needs**, **produces**, and a **check**. A step is done only when the check exits 0.

## Copied and adapted

| AIDeveloper skill | In this Expert | Change |
| --- | --- | --- |
| **remember** | `remember` | Saves **facts, rules, or tools**. INDEX per kind. |
| **journal-keeper** | `journal-keeper` | Updates `progress.md` and `state.json` (map, step, artifacts, last_check). No software phases. |
| **playbook-keeper** | `playbook-keeper` | After a workflow the person approved twice, save the steps **and** a work map with checks. |
| **librarian** | folded into **read-saved-files** | Before work: indexes + role + a short file list. Then **run-map** if a map matches. |
| **verifier** | `verifier` | Gate is exit-0 **checks** on every step. Prose in `role.md` is extra. |
| **continue** | `continue` | Resume from the journal. One ready work-map step. Continue is not a yes. |
| **task-breakdown** | `task-breakdown` | Split a request into a work map (or a slice of one), not a disconnected list. |
| **tool-operator** | `tool-operator` | Run only what `docs/tools/` describes. Log under `evidence/`. Failed command during a step → **run-until-check**. |
| **orchestrate-subagents** | `orchestrate-subagents` | Optional extra worker with a short file list. This chat owns the journal. |

## Not copied (software-only)

implement-feature, hld-writer, dd-writer, spec-parser, scaffold-project, test-writer, test-ui-automation, refactor, git-workflow, hierarchy-expander, diagram-generator, generate-dashboard, integration-manifest-keeper, reconcile-artifact-graph, reconcile-stale, iterative-feature, program-scoper, orchestrate-program, workflow-composer, goal-keeper, autopilot (as written in AIDeveloper).

## New skills (learning a job)

1. **define-role** — Ask what this Expert is for; write `role.md` and stub workflows (including what a command would see if done).
2. **read-saved-files** — Before work, read the indexes and only the matching files.
3. **teach** — They said this was wrong. Save a fact, rule, or tool. Do not only apologize.
4. **after-task** — After a run, save anything new into `docs/`.
5. **ask-dont-invent** — No file for how this business works → **ask**. Do not make it up.
6. **refuse-outside-role** — Outside `role.md` → refuse or send to another Expert folder.
7. **write-up** — Summary, parts, **artifacts**, **check logs**, actions, questions, `docs/` files used.
8. **ingest-example** — They drop a good old example. Pull facts/rules/steps out of it.
9. **conflict-check** — New statement vs an old file. Ask which is right.
10. **first-principles** — Break the job into parts; those parts become work-map steps and artifacts.
11. **run-map** — Load the work map; run the next ready step only.
12. **run-until-check** — Run the tool, run the check, read the log, retry (cap 3).
13. **write-check** — Propose a check command; save it only after they approve.
14. **start-job** — Before real work, open one `items/` folder so days and appointments do not mix.

**Later if needed:** archive old rules that never get used. Recurring jobs belong in Team Manager, not this folder.
