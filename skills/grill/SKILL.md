---
name: grill
description: Pressure-test a plan, spec or design before anything is built, by asking the uncomfortable questions one at a time and ending with resolved decisions, open questions and a recommendation. Use when the user says "what do you think of this plan", "grill this", "is this a good idea", or before work that touches many files, a data migration, a prompt change, auth, or several surfaces at once.
---

# /grill: interrogate the plan, not the planner

**Works in:** Claude Code and claude.ai chat (it only needs the conversation). Paste the plan or describe it.

A plan that survives `/grill` is one whose author has answered every uncomfortable question before building. The goal is to surface open decisions while changing them is still cheap. This is the cheapest skill in the toolkit; the expensive one is shipping the wrong design to real users.

## When to use

Before any of:
- A new feature that touches many files or several surfaces (web and mobile, app and email).
- A database schema change or data migration.
- A change to an AI system prompt or tool (regressions show up days later as user complaints).
- Anything touching login, permissions or payments.
- A new plan or spec document.

## When not to use

- Bug fixes: the plan is "fix the bug". Use `/root-cause`.
- One-file edits and pure styling: just do them.
- After the work has started: grilling mid-build is sunk-cost theatre.
- If a question can only be answered by running code, recommend `/spike` instead of asking it.

## Inputs

A plan document, a paragraph in chat, or an idea that is still verbal (then write it down first, before grilling). Read the whole plan before asking anything. Do not grill the title.

## The question library

Not a checklist. Ask the ones that matter for **this** plan, biggest unknowns first. Stop when you stop learning.

**Scope and necessity**
1. What is the one-sentence user-visible outcome? If it takes two sentences, the plan is doing two things.
2. What happens if we do nothing? Who asked for this: a customer, a ticket, data, or ourselves?
3. What is the smallest version still worth shipping? Can that go first and the rest later?
4. What are we explicitly *not* doing? Say it out loud so it does not creep in.

**Risk**
5. If this is wrong, what is the blast radius and who notices first?
6. Is there a feature flag, a gradual rollout, or a rollback story? If not, why is none needed?
7. How do existing records, users and drafts behave after the change?
8. Does it need a migration? Do the schema change and the migration ship together?

**AI specifics (if the plan involves a model)**
9. Does a new tool overlap with an existing one? Why not extend that one?
10. Which prompts and which models are affected? What is the regression test (a fixed set of example inputs with known good answers)?
11. Does the model emit ids or references that the UI later looks up? Do they come from the same place the UI reads?
12. What does the model do when it has no good answer: does the plan allow "I don't know"?

**Surfaces**
13. Which other surfaces need this too (mobile, extension, email, API, background jobs)? Who builds them and when?

**Observability and reversibility**
14. How will we know it worked in production? How will we know it broke?
15. If it ships broken, how do we undo it: revert, flag flip, config change, data fix?

**People**
16. Did the decision-maker actually say yes to this, or did we infer it? Read back the one-sentence outcome and confirm.

## Conducting the grill

- **One question at a time.** Wait for the answer before the next. Offer your recommended answer only if asked, or if the user wants a faster pace; the point is to make the author think.
- "I don't know yet" is the most useful answer in the session. Record it as an open question and move on.
- If the user gets impatient, stop and offer to list the remaining questions so they can answer in writing later.

## Output

```
**Plan in one sentence:** <restate>
**Resolved decisions:**
- <decision>: <answer>
**Open questions:**
- <question> (blocks: <what it blocks>)
**Recommendation:** proceed / narrow scope to X / defer until Y is answered / abandon
```

If the plan lives in a document, offer to write the resolved decisions and open questions into it. Do not edit it without permission.

## What this skill is not for

- Talking the user out of shipping. You surface, they decide.
- Architecture lectures. Stay on the plan in front of you.
