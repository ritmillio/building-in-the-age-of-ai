# Tricks inventory (INTERNAL, delete before the repo goes public)

Raw material for `guides/tricks.md` (T2) and `guides/war-stories.md` (T3). One line per trick, then its source.
Sources are private (the product repo's `AGENTS.md`, `docs/reference/`, `.agents/skills/`, and the agent memory notes under `memory/`); never copy paths, names, numbers or ids from them into public files.

Tags: `[have: <file>]` already covered in this repo, `[war]` good war story for T3, `[S]` sensitive, founder must OK before any public use, `[product]` a practice for people building AI products (not for building with AI).

## Context

1. One task per session; when the topic changes, start fresh and carry state in a handoff note, not in the chat. src: `~/.claude/skills/handoff`, guides/context.md §6 [have: templates/handoff-prompt.md]
2. Long unattended work = a fresh process per iteration that reads and writes one committed ledger (inbox, health, standing rules, backlog, log). src: relay skill, this run's ledger
3. Durable decisions live in the repo (`docs/`), not in one tool's private memory, so every agent and every vendor's tool reads them. src: AGENTS.md "Shared agent setup"
4. Write memory as fact + **Why** + **How to apply**; the why lets the agent judge the edge case the rule did not foresee. src: memory/*.md format
5. Keep the memory index to one line per note and the bodies in separate files (progressive disclosure: the agent loads detail only when relevant). src: memory/MEMORY.md [have: templates/memory-index.md]
6. Send wide searches to a sub-agent so file dumps stay out of the main context; keep only the conclusion. src: guides/context.md §6 [have: guides/context.md]
7. Fence vendor boilerplate inside the rules file with marker comments and say "project rules override the vendor block". src: AGENTS.md header
8. Tell the agent how `docs/` is sorted (active / plans / reference / research / done / obsolete) so it files and finds things by state. src: AGENTS.md "Documentation Files"
9. Put a "how to read this" line at the top of any long doc an agent or human will skim: inbox first, then status, then the rest. src: relay ledger header

## Prompting and talking to the agent

10. Make the agent ask decisions as 2-4 selectable options, recommendation first and labelled, each option saying what it costs or unblocks. src: AGENTS.md "Reporting Rules", memory/ask-with-selectable-answers.md [war: a plan with many open decisions that were never put to the founder; asked as four options, all answered in one round]
11. Rule: "when reporting to me, be extremely concise". src: AGENTS.md "Reporting Rules"
12. Name the scope and stop: "only a hero section, full width, that's it". Agent asks before growing it. src: memory/feedback-ui-work-next-route-on-2-0.md [war]
13. Get something you can open first, then polish; long background runs before anything is viewable cost patience. src: same
14. Ask for versions side by side (A before, B new, C new on top of old) instead of a replacement. src: memory/feedback-versions-before-removing-1017.md [war]
15. A yes to a direction is not a yes to deleting things you liked: the agent asks per element before removing. src: same
16. Correct once, with the reason, and say "save it as a rule"; the next session inherits it. src: memory/feedback-no-rounded-full-slab-buttons.md ("fix all these, also save it to memory")
17. Choosing a model: list every candidate with price and trade-off first, pick, then implement. Do not let the agent jump from a catalogue to editing config. src: memory/model-selection-preferences.md
18. Trust real-workload experience over a "say OK" probe when judging a model. src: same
19. Grill the plan before any code: the agent interviews you until the decision tree is resolved. src: .agents/skills/grill [have: skills/grill]
20. Spike: a throwaway prototype when a choice is genuinely unclear, thrown away after the decision. src: .agents/skills/spike [have: skills/spike]
21. Draft the plan as a file, then have a second agent shred it (verify each claim against the code) before building. src: draft-plan + shred-plan skills
22. Fragments first, shape later: dump raw claims and stories into one file, then shape them into an article in a second session. src: writing-fragments + writing-shape skills

## Rules files and skills

23. One canonical `AGENTS.md`; `CLAUDE.md` is a symlink to it, so Claude Code, Codex and Kimi read the same rules. src: AGENTS.md, docs/reference/shared-agent-setup.md (vendor links listed there) [have: templates/AGENTS.md, partly]
24. One canonical skills folder (`.agents/skills/`) with `.claude/skills` linking to it; never per-tool copies. src: same
25. A small check script proves the sharing (links resolve, every skill has metadata, no duplicate names); run it in CI. src: same
26. Skills share instructions, not permissions, hooks, credentials or memory; those stay per tool. src: same
27. Restart the agent session after you change startup instructions or add a skill. src: same
28. When you explain the same thing a second time, turn it into a skill (scaffold-skill). src: .agents/skills/scaffold-skill [have: skills/scaffold-skill]
29. A verify skill: adversarial re-review, edge cases, new tests, all gates, drive it in a browser, verdict SHIP / SHIP WITH NOTES / NOT READY. src: .agents/skills/verify, memory/verify-skill.md [have: skills/verify]
30. A root-cause skill: reproduce, minimise, hypothesise, instrument, fix, regression test. src: .agents/skills/why, diagnose skill [have: skills/root-cause]
31. Every hard rule carries the incident that produced it (one line); agents respect rules they understand. src: AGENTS.md "Migration Rules" (each rule names its incident)
32. Code in English (identifiers, keys, comments); only user-facing text is localised. src: memory/feedback-code-identifiers-english.md
33. Borrow good third-party skills (React performance, copywriting, pricing, landing pages) instead of writing your own. src: .agents/skills/{vercel-react-best-practices,copywriting,pricing-strategy,landing-page-design} [have: skills/third-party.md]
34. Correct vendor examples in your own rules ("this sample is not our contract") instead of editing the injected block. src: AGENTS.md "Vendor example corrections"

## Agents and parallel work

35. One git worktree per agent or task; never two agents in one checkout. src: memory/concurrent-sessions-branch-flips.md [war: commits landed on the wrong branch because another session switched the checkout]
36. Assert the branch in the same command as the commit with a hard check, not a print: `[ "$(git branch --show-current)" = feat/x ] && git commit`. src: same, AGENTS.md "Git Rules"
37. Never `git stash`, `checkout --` or `reset` in a shared tree; look at the old version with `git show HEAD:path`. src: memory/feedback-never-stash-shared-worktree.md [war: a stash pulled other agents' unsaved work out of the tree for ten seconds while the app was hot-reloading]
38. Never `git add -A`; add explicit paths, and refuse to commit if the index already holds something you did not stage. src: memory/feedback-shared-index-commit-guard.md [war: one commit swept another agent's staged files under its own message]
39. Chain check and action with `if check; then act; fi`, never `check; act` (the `;` runs the action anyway). src: same [war]
40. Do merges and cherry-picks in a throwaway worktree; bring over only the resolved result. src: memory/feedback-atomic-edits-live-app.md [war: conflict markers on disk broke the live app window]
41. When a dev server watches the files, write each edit in one pass (import and use together) so no half-written file is ever served. src: same [war]
42. A fresh worktree has no `.env` (gitignored files stay behind); a build that "fails" there may be a missing secret, not your code. src: memory/verification-traps-web-build.md
43. In a monorepo, a worktree that borrows another checkout's `node_modules` runs your gates against the wrong source: phantom red or false green. src: memory/feedback-fold-worktree-workspace-links.md
44. Agents fold into one integration branch; only the human merges to main. Agents never merge a PR and never push main. src: AGENTS.md "Git Rules", memory/feedback-merge-into-integration-branch.md
45. One branch and one PR per initiative, phases as separate commits; no stacks of dependent PRs. src: memory/no-stacked-prs.md
46. Overnight relay: ledger with backlog, standing rules, founder inbox, iteration log; each iteration does one item, commits, exits. src: relay skill
47. Kill processes by a precise pattern (`pkill -f "vitest run"`), never a broad one that also matches long-running jobs. src: memory/pkill-vitest-kills-vite-node-fleet.md [war: a broad pkill killed a whole background fleet]
48. Cap how many agents and dev servers run at once; a machine pinned at full memory crashes and takes every session with it. src: memory/crash-recovery-1015.md, reclaim skill [war]
49. Keep scripts you will need again in the repo, not in /tmp scratch space: a crash or reboot wipes it. src: memory/crash-recovery-1015.md
50. A guard that puts the laptop to sleep on battery with the lid closed; a forgotten `caffeinate` kept it awake in a bag for hours. src: memory/sleep-guard-never-awake-in-bag-1019.md [war]

## Verification

51. "Done" means seen working: click the real control or re-ask the real question, then report what you saw, not what the tests say. src: memory/feedback-always-verify-live.md, memory/always-verify-work.md [have: guides/how-i-build.md §2] [war: fixes reported done on green tests, bugs found in the browser minutes later]
52. Four steps: gates; drive it; check the side effect where it lands (the row, the file, the email); screenshot. src: memory/always-verify-work.md
53. If it could not be checked live, the report says "not verified live" in those words. src: memory/feedback-always-verify-live.md
54. `cmd | tail` reports tail's exit code, not the command's: a failing build looks green. Use `cmd; echo EXIT=$?`. src: memory/verification-traps-web-build.md [war]
55. Some builds skip type checking (`next build` says so in its own output); run the type checker as its own gate. src: same [war]
56. Run the last gate on the exact commit you hand over, not on an earlier one. src: memory/feedback-tsc-before-fold-head.md
57. Restart the dev server after server-side changes before measuring anything, then probe once that the new code is live. src: memory/feedback-restart-dev-before-eval.md [war: two evaluation rounds measured three-hour-old code]
58. "I don't see the change": first check which folder the running dev server was started from. src: memory/concurrent-sessions-branch-flips.md
59. Read what CI actually runs; a job called "test" may skip your biggest suite. src: memory/ci-test-job-skips-web-suite.md [war]
60. CI path filters decide whether a guard runs at all; a guard outside the filter never fires. src: memory/cross-surface-guard-blindspots.md
61. A dead measurement looks like "zero differences" (a tool flag that works on Linux but not macOS); sanity-check a suspiciously clean result against a second source. src: memory/bsd-join-silent-empty-diff.md [war]
62. A feature can type-check with no data behind it; check that real data flows, not just that the UI renders. src: memory/always-verify-work.md

## Design

63. Design from real references: 6-10 real screens per screen (Mobbin), grouped into directions, pick per screen. src: memory/feedback-design-from-mobbin-refs.md [have: guides/my-stack.md "Where I find designs", partly]
64. Show a labelled contact sheet of the references on screen before asking to pick; text or ASCII previews get rejected. src: memory/feedback-show-refs-before-building.md
65. On marketing pages, mount the real product components on sample data; drawn replicas look fake and drift. src: memory/feedback-landing-real-components.md
66. Compare whole pages and rebuild in the reference system; patching an old page section by section fails. src: same
67. A design rules file (radius tiers, one button style, fonts, banned patterns) plus a test that fails on a banned pattern. src: memory/feedback-glass-floating-layers.md, AGENTS.md "Border Radius" [have: templates/design-rules.md]
68. When something "looks wrong", the complaint is usually inconsistency (mismatched corners, greys), not the effect itself. src: memory/feedback-glass-floating-layers.md
69. Build it in the real app at a real URL, not a standalone HTML mock. src: memory/feedback-ui-work-next-route-on-2-0.md
70. Never put a placeholder where the asked-for picture goes: show nothing or the real thing. src: same
71. Reading text in sans; a serif only for one display title per screen. src: memory/feedback-app-text-sans-1013.md
72. Talks: Excalidraw look, no numbers on slides, a story instead; numbers live in the notes. src: memory/feedback-talk-decks-excalidraw-no-numbers.md

## Shipping and ops

73. Agents never touch the production database; all work on dev branches or local copies. src: memory/never-touch-prod-db.md, AGENTS.md
74. Schema change and migration in the same commit; never push schema straight to a shared database; idempotent SQL (`IF NOT EXISTS`). src: AGENTS.md "Migration Rules" [war: a column dropped by hand, left in the schema, broke production for weeks]
75. Hosting env var changes need explicit human approval for that exact action; snapshot the list before and diff after. src: memory/feedback-vercel-env-never-rm-shared.md [war][S]
76. Env damage stays invisible until the next deploy (a running deploy keeps its snapshot); check production health after every merge. src: same [S]
77. Deploy without moving the domain, check, then promote; keep a rollback target. src: same
78. Read production errors from the CLI (`vercel logs --environment production --level error`) before saying "ready". src: same, memory/vercel-logs-cli-recipe.md
79. Small overruns on an agreed spend limit (under about a dollar) go ahead and get reported; anything bigger or irreversible gets asked. src: memory/feedback-small-spend-overruns.md

## Team and process

80. Every unit of work gets one record: what, why, how it was verified (or "not verified"), links, next steps. src: AGENTS.md "Document Every Piece of Work"
81. Search before creating a record; update the existing one. src: same
82. Never secrets, tokens or customer personal data in docs or tickets. src: same
83. One task list, not two. src: memory/one-task-list-1010.md
84. Tasks folded into one release all link to the PR the human actually merges. src: memory/feedback-notion-pr-link-release-pr.md
85. Pages the team reads are written as normal pages: no agent narration ("overnight run", "the founder asked"), no notes to the boss. src: memory/feedback-notion-pages-read-normal.md
86. An unattended run's open questions are put to the human as options at the next conversation, never left parked in a doc. src: memory/ask-with-selectable-answers.md

## Money and tools

87. Bake-offs on your own real data with ground truth, several runs per model, before switching. src: memory/gateway-cheap-model-bakeoff.md
88. Headline price traps: reasoning models bill thinking as output; measure cost per real task, not per token. src: same [war]
89. A cheap model can silently return an empty answer when its reasoning budget runs out; force low reasoning effort or check for empty output. src: same
90. Flex / batch tiers roughly halve the price; assert in the response metadata that the discount actually applied. src: same
91. Newer is not always better or cheaper: test the new version on your task before upgrading. src: same
92. Startup cloud credits pay for real model usage, but check which models they cover before planning on them. src: memory/azure-credits-foundry-1005.md [S: no amounts in public]
93. Product videos from code (Remotion) with TTS narration; listen to the output, because a voice model can silently fall back to a different voice. src: memory/video-good-prompt-snippet.md

## For people building AI products [product]

94. Let the model decide when to call a tool; forcing a tool on every turn wastes time on off-topic research. src: memory/feedback-smart-tool-layering.md
95. Check only the risky sentences of an answer (quotes, numbers with a citation) against the sources, and repair only on mismatch; no blanket second pass. src: memory/post-answer-source-check.md
96. One-click OAuth over pasted API keys: setup friction kills small-business adoption. src: memory/feedback-oauth-default-connections.md
97. Do not send users away from your product; open sources inside it. src: memory/feedback-never-navigate-away.md
98. Proactive agents act by default, each action with accept/undo and an off switch; irreversible or external actions still need approval. src: memory/feedback-proactive-coworkers-1015.md
99. Build the capability, not a copy of your own setup: what is shaped around your company does not sell to others. src: memory/feedback-replicate-capability-not-notion.md

## Not for publication

- Model vetoes naming vendors' models ("terrible", "does not work") and the "no Anthropic models in the runtime" ruling: private product decisions, keep out.
- Credit amounts, spend figures, customer or partner names from any memory note: keep out.
- The env var incident (75-76) is a strong war story but shows a production outage; publish only generalised and only with the founder's OK.
