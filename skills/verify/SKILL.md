---
name: verify
description: Post-implementation verification loop. Use right after finishing a feature or fix ("verify", "/verify", "make sure this isn't garbage") to adversarially re-review the work, hunt edge cases, write the missing tests, run every gate and use the feature like a real user. Loops until a full pass finds nothing new, then gives a ship / not-ready verdict.
---

# /verify: prove it works before calling it done

**Works in:** Claude Code (needs a shell, the test runner and ideally a browser). In claude.ai chat you can run phase 2 on pasted code.

"Finished" is a claim, not a fact. Treat the work you just did as a hostile pull request from a stranger and loop review, test, simulate until a complete pass produces zero new findings. The goal is a verdict you can defend: ship, ship with notes, or not ready.

## When to use

- Right after an implementation session, when the user says "verify" (optionally with a focus: "verify, focus on the mobile path").
- Before opening a pull request, or before taking one out of draft.
- After fixing something a previous `/verify` pass found (the loop restarts).

## When not to use

- Finding the cause of a reported bug: use `/root-cause`.
- Critiquing a plan before any code exists: use `/grill`.
- Nothing was built and there is no diff: say so and stop.

## Step 0: scope the work under test

1. `git status` and `git diff main...HEAD --stat` (plus uncommitted changes). That diff, together with what was built in this conversation, is the scope.
2. Branch sanity: confirm you are on the branch you think you are verifying, in the same command as the checks. If several agent sessions share a checkout, one of them may have switched branches, and the dev server on your usual port may be serving a different folder.
3. Write a three-line contract: what the feature must do, for whom, and what must not break. Every finding is judged against this contract, not against taste.

## The loop

Run phases 1 to 4 as one pass. If any phase led to a code change, run another full pass. Stop when a complete pass yields zero new findings, or after three passes (then report what is still open instead of looping forever).

### 1. Gates (cheap, run first, in parallel where possible)

- Type check, linter/formatter, the test suite. Scope the tests with a filter while iterating, but run the full suite once before the final verdict.
- Schema changed? A migration must exist in the same diff, and the project's migration check must pass. Never push schema directly to a shared or production database.

A red gate is a finding. Fix it and restart the pass.

### 2. Adversarial review

Read the full diff as a skeptic. For every changed file ask: which input, state or user makes this wrong? Hunt for:

- **Edge cases:** empty, null and undefined inputs, empty result sets, a brand-new account with no data, maximum-length input, non-ASCII characters (accents, emoji) in search, sort and URLs, the same action fired twice or concurrently, a stream aborted halfway.
- **Error paths:** what does the user see when the request fails, the tool throws, the network drops? A silent `catch` is a finding.
- **Auth and tenancy:** is every new query scoped to the right user or organisation? Is every new route behind the right auth? Can a user read someone else's record by changing an id?
- **Project rules:** whatever your rules file (AGENTS.md, CLAUDE.md) says always applies, check each rule against the diff. A violation is a finding.
- **Other surfaces:** does the change need a counterpart on mobile, in an extension, in an email template, in the API docs?

### 3. Write the missing tests

For each edge case from phase 2 that is testable as plain logic, write the test **before** deciding whether the code handles it, and let the test tell you. Prefer extracting pure logic over mocking half the app. If something can only be verified against the database or the running app, cover it in phase 4 and say so. A failing new test is a finding: fix the code, not the test (unless the test misread the contract).

### 4. Use it like a real user (when there is a UI or API)

1. Check a dev server is running and that it serves *this* checkout. If you start one in the background, say so, so it does not become a mystery process.
2. Walk the happy path from the entry point a real user actually uses, then two or three abuse paths: empty submit, double click, back button mid-flow, absurdly long input, refresh mid-stream.
3. After each flow, read the browser console and the network log. A console error on the happy path is a finding even if the screen looks fine.
4. Check light and dark theme if styling changed.
5. Never point the browser or a script at production data.

If a real-use check is impossible (no browser access, backend-only change), say so in the report instead of silently skipping it.

## Verdict report

Lead with the verdict, then the evidence:

1. **Verdict:** `SHIP` / `SHIP WITH NOTES` / `NOT READY`, one sentence why.
2. **Passes run** and what each found (one line per pass).
3. **Findings fixed:** file:line, what was wrong, how it is covered now.
4. **Tests added:** how many, what they pin down, and the final gate results verbatim (green or red, no hedging).
5. **Residual risk:** what was NOT verified (untestable paths, skipped flows, production-only behaviour, pending migrations). This list is mandatory, and an empty one must be earned, not assumed.

Do not soften `NOT READY` to be polite. The point of the skill is that "done" means proven.
