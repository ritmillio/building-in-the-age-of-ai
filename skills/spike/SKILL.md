---
name: spike
description: Build a throwaway prototype that answers one question (which layout, does the model use this field, does this library do what the docs claim) before committing to a real implementation. Use when the user says "let's try", "what if we", "show me two versions", "spike this", or when a design choice is genuinely unclear and a static mockup would not settle it.
---

# /spike: a throwaway prototype, not real code

**Works in:** Claude Code (a dev route or a script in your project) and claude.ai chat (a single HTML artifact with the variants side by side).

A spike is disposable exploration. It exists to answer one question, get deleted, and inform the real build. It is not a first draft of production code.

## Good reasons to spike

- A UI question with several plausible answers ("drawer, sidebar or inline?").
- An AI behaviour question ("does the model actually use this new field the way we expect?").
- A mobile feel question where a static mockup would lie ("does this bottom sheet feel right on a real phone?").
- A new library or API whose docs are ambiguous, where a 30-line demo settles it.

## Bad reasons

- "Just build the feature." That is the work, not a spike.
- Tiny style tweaks: try them inline.
- Database schema changes: there is no safe spike path for those.

## Where to put it

Pick the lightest place that proves the point:

| Question | Where |
|---|---|
| UI variants | One dev-only page with the variants side by side (guarded so it never ships), or one standalone HTML file / artifact |
| Logic, no UI | `scripts/spike-<name>.(ts|py)` |
| AI prompt or tool behaviour | A script that calls the existing prompt/tool with 5 sample inputs; use the cheapest model unless the question is about a specific one; no unbounded loops |
| Mobile screen | A hidden screen reachable only by direct link, never wired into navigation |

## Rules

1. **One question per spike.** Two questions means two spikes, or drop one.
2. **Time-box it.** Say the budget out loud before starting ("30 minutes", "until I can compare the layouts"). When it runs out: stop, then extend with a reason or kill it.
3. **Hardcode aggressively.** Fake data, fake auth, copied types. Spikes do not need to generalise.
4. **No tests, no migrations, no new dependencies** unless the dependency is the thing being evaluated.
5. **Use the real design tokens and icons anyway**, so the visual verdict transfers to the real build.
6. **Mark it.** First line of every spike file: `SPIKE: <the question>. Delete after <date or condition>.`

## Workflow

1. State the question in one sentence. If you cannot, you are not ready to spike.
2. State the success criterion ("I can see A, B and C side by side and pick one"; "the model uses the field in 4 of 5 sample inputs").
3. State the budget.
4. Pick the location from the table.
5. Build, hardcoding everything that is not under test.
6. Show the result: screenshots, the script output, the artifact. Whatever lets the user decide.
7. Get the decision from the user. Do not assume it.
8. Write the real plan in one paragraph: which variant, which files the real build touches, what changes from the spike, what is deferred.
9. Delete the spike (or move it to an ignored scratch folder). Never merge a spike.

## Report

```
**Question:** <one sentence>
**Answer:** <variant chosen, value measured, behaviour observed>
**Evidence:** <screenshot, output, link>
**Next:** <one-paragraph plan for the real build>
**Cleanup:** <files deleted>
```

## Refuse these

- "Spike it and merge it if it works." Build it properly or not at all.
- "Spike a refactor." Refactor spikes turn into rewrites; grill the refactor first, then plan a real change.
