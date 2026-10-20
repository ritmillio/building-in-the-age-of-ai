---
name: root-cause
description: Find the actual cause of a bug or unexpected behaviour (not a plausible one) with a reproduce, localise, minimise, hypothesise-and-verify loop, then make the smallest fix at the cause and add a regression guard. Use when the user asks "why did X happen", reports a UI glitch, a failing AI tool call, a 404/500, missing data, or a "this used to work" regression.
---

# /root-cause: the real cause, not a plausible one

**Works in:** Claude Code (it reads code, runs commands and tests). In claude.ai chat you can run steps 1 and 5 on pasted code, logs and screenshots.

A diagnosis loop tuned for shipping a small targeted fix, not for refactor-driven rewrites. Work the phases in order; do not move on until the current one has a concrete answer.

## 1. Reproduce

- Get the exact reproduction: page or route, input, payload, account, screenshot.
- If it is unclear, ask **one** targeted question ("web or mobile?", "which model?"), never "give me more info".
- If the user attached a screenshot, look at it first. Do not guess what is on screen.

## 2. Localise

Find the layer responsible. Write down your project's stable seams once (in your rules file) so this step is fast, for example:

| Symptom | First place to look |
|---|---|
| Wrong text on screen | the component that renders it |
| Wrong AI answer | the tool implementation, then the prompt |
| AI tool result shows as raw data | the renderer that maps tool results to UI |
| 404 / 500 | the route handler, then auth and routing config |
| Login redirect loop | the auth middleware and its public-route list |
| Missing column or field at runtime | schema vs migration drift |
| Search returns nothing | the index or embedding model differs between write and read |
| "Not found" when opening a result | an id from one table is looked up in another |

## 3. Minimise

Shrink the failing case to the smallest input that still breaks. For AI bugs: same question, less context, fewer tools enabled. For UI bugs: which exact element, which exact data.

## 4. One hypothesis at a time

Form one hypothesis and confirm or kill it with evidence (a code read, a search, a log line, a query) before forming the next. Never chain three guesses.

## 5. Symptom vs cause

Before proposing a fix, answer: **which assumption was violated?** Not "which line is wrong".

Example: a "failed to load" error when opening a search result. Symptom: the 404. Cause: the search tool returns ids from two different tables under the same field name, and the viewer assumes they are always from one of them.

If you cannot name the violated assumption, keep digging.

## 6. Fix scope

Default to the **smallest fix at the cause site**. No surrounding refactors. Answer two questions out loud before editing:

1. Is this safe to ship to live users today, or does it need a flag or a migration window?
2. Do other call sites share the same violated assumption? List them, but do not fix them in the same change unless the user agrees.

## 7. Regression guard

For anything that was rendered, stored or sent to a model wrong, add one of: an automated test (preferred), a standalone repro script, or (only if untestable) a code comment naming the violated assumption. If you decide a guard is not worth it, say so and why.

## Report

```
**Symptom:** <what the user saw>
**Cause:** <the violated assumption, one sentence>
**Where:** <file:line>
**Fix:** <one sentence>
**Other call sites at risk:** <list, or "none">
**Regression guard:** <test added / not needed because ...>
```

## Not for

- New feature design: `/grill` first.
- Exploratory UI work: `/spike`.
- "Clean up this messy module": a separate refactor task.
