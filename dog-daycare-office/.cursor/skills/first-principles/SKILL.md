---
name: first-principles
description: >-
  Break the job into real parts, see how those parts connect, and build or
  rebuild a solution from them. Use when designing, fixing, or choosing
  how to do work — not when they only asked a yes/no from a saved rule.
---

# First principles

Think in parts. Do not copy a usual bundle and call it a solution.

## When

They asked how to do something, how to fix something, or what to do with mixed inputs. Skip this when a saved rule already answers a yes/no and nothing needs assembling.

## Do

After **read-saved-files**:

1. **Name the outcome** in their words. One sentence.
2. **List the parts** that make up that outcome. A part is a fact, a rule, a tool step, an input, or a result another part needs. Keep going until a part is either:
   - already in a file in this folder, or
   - ordinary public knowledge (label it a guess), or
   - unknown for *this* business → **ask-dont-invent** (do not invent the part).
3. **Say how the parts connect.** What must exist before something else can run. What must never mix.
4. **Assemble** a solution from those parts only. Use their words and their tools. If this is a multi-step job, those parts **are** work-map step ids and artifacts (`needs` / `produces`). Write or update `docs/workflows/<name>.md` instead of leaving the assembly only in chat.
5. If the assembly fails or they say it is wrong: **take it apart**. Drop or replace the part that did not fit. Assemble again. Do not glue on a new usual bundle.

## Do not

- Treat “best practice,” a vendor’s default workflow, or last week’s chat as one unbreakable block.
- Invent a part so the picture looks complete.
- Explain this method with cute analogies. Name the parts and how they join.

In the **write-up**, include a short **Parts** list: each part, where it came from (file, guess, or question), and how it was used. If a work map ran, those parts should match step ids and **artifacts**.
