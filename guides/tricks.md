# Tricks: building faster with AI, one habit at a time

These are the working habits behind the workshop, collected from our own rules file, skills and the notes our agents keep about what went wrong. Every one of them is something we actually do. Most came from a mistake, and where it helps we say which. The longer versions of those mistakes are in [war-stories.md](war-stories.md).

Each trick says **what** to do, **why** it works, the exact **prompt, command or file**, and **when it fails**. Where a trick is already covered in depth elsewhere in this repo, we link there instead of repeating it.

New to all this? Read [how-i-build.md](how-i-build.md) first (the loop), then come back here for the details. Vendor links were opened and checked on 2026-10-21.

**Groups:** [Context](#context) · [Prompting](#prompting-and-talking-to-the-agent) · [Rules and skills](#rules-files-and-skills) · [Agents and parallel work](#agents-and-parallel-work) · [Verification](#verification) · [Design](#design) · [Shipping and ops](#shipping-and-ops) · [Team and process](#team-and-process) · [Money and models](#money-and-models) · [If you build AI products](#if-you-build-ai-products)

---

## Context

**1. One task per session, state in a file.** When the topic changes, start a fresh session and carry what matters in a short handoff note, not in the chat history. *Why:* long chats get worse at following instructions ([context.md](context.md) explains context rot). *Do:* end with the [handoff prompt](../templates/handoff-prompt.md), paste the result into a new session. *Fails when:* the handoff is a transcript dump. It should be the decisions, the open questions and the next step, nothing else.

**2. Decisions live in the repo, not in one tool's memory.** Write durable decisions to `docs/` in the project. *Why:* every agent and every vendor's tool can read a file in the repo; only one tool can read its own private memory. When you switch tools, nothing is lost. *Fails when:* `docs/` becomes a dump nobody prunes. See trick 4.

**3. Memory notes carry their reason.** Write each memory as the fact, then a **Why:** line and a **How to apply:** line. *Why:* the reason lets the agent judge the edge case the rule did not foresee, instead of applying it blindly or ignoring it. *Do:* "Never stash in a shared checkout. **Why:** a stash removed another agent's unsaved work for ten seconds while the app was reloading. **How to apply:** to see an old version use `git show HEAD:path`." Template: [memory-index.md](../templates/memory-index.md).

**4. Tell the agent how your docs are sorted.** One line in the rules file: "`docs/active/` is in progress, `docs/plans/` is not started, `docs/reference/` is stable, `docs/done/` is finished, `docs/obsolete/` is kept for history." *Why:* the agent files new documents in the right place and stops trusting an obsolete plan. *Fails when:* nobody moves a doc when its state changes.

**5. Big reads go to a sub-agent.** "Use a sub-agent to search the codebase for every place we send email and report back only the list." *Why:* the file dumps stay in the sub-agent's context; yours gets the conclusion. Claude Code docs: [sub-agents](https://code.claude.com/docs/en/sub-agents). *Fails when:* you then ask the main agent to re-read all the files anyway.

**6. Put "how to read this" at the top of any long doc.** One line: "Open questions first, then status, then the rest." *Why:* a human skimming at 7am and an agent starting cold both read the part that matters first.

**7. Fence the vendor boilerplate in your rules file.** Some tools inject a block into `AGENTS.md`. Wrap it in marker comments and write above it "Project rules override the vendor block below." *Why:* the injected sample is generic; your rules are specific. When the two disagree, the agent knows which wins. If a vendor example contradicts your setup, add a line "the example above is not our contract; ours is X" rather than editing the injected block, which the tool may overwrite.

## Prompting and talking to the agent

**8. Make it ask with options, not paragraphs.** Rules file line: "Ask every decision as two to four options, recommendation first and labelled, each saying what it costs or unblocks." *Why:* a decision buried in prose gets skipped; four options get answered in one round. We once had a plan with many open decisions that were never put to us; asked as options, all of them were answered in one go. *Fails when:* the options are vague ("option A: do it well"). Template: [ask-with-options.md](../templates/ask-with-options.md).

**9. "When reporting to me, be extremely concise."** Put it in the rules file, word for word. *Why:* long reports hide the one line you needed, usually the one about what was not checked.

**10. Name the scope, then stop.** "Only a hero section, full width. That's it." *Why:* agents grow tasks. A named boundary makes the agent ask before going further. *Fails when:* you say "and anything else you think is useful".

**11. Something you can open first, polish later.** Ask for the smallest version you can look at in a minute or two, then iterate. *Why:* a long background run before anything is viewable costs patience and usually builds the wrong thing.

**12. Versions side by side, not replacements.** "Show me A (current), B (new), C (new on top of current)." *Why:* you can only judge a change next to what it replaces. And a yes to a direction is not a yes to deleting the parts you liked: ask the agent to check per element before removing anything.

**13. Correct once, with the reason, then "save it as a rule".** "Fix all of these. Rounded pill buttons look cheap next to our square cards. Save that as a rule." *Why:* the next session inherits the rule; you never correct it again. See [how-i-build.md §1](how-i-build.md#1-teach-it-once-not-every-day).

**14. Grill the plan before any code.** The agent interviews you, one question at a time, until every branch of the decision is resolved. Skill: [`grill`](../skills/grill/SKILL.md). *Fails when:* you answer "whatever you think" to every question.

**15. Spike when the choice is genuinely unclear.** A throwaway prototype that answers exactly one question, time-boxed, deleted after the decision. Skill: [`spike`](../skills/spike/SKILL.md). *Fails when:* the spike quietly becomes the product.

**16. Plan as a file, then have a second agent shred it.** One session writes the plan to `docs/plans/`; a fresh session checks every claim in it against the actual code before anything is built. Skills: `draft-plan` and `shred-plan` ([where to get them](../skills/README.md#also-by-the-author-published-separately)). *Why:* the planner believes its own assumptions; a second reader does not.

**17. Fragments first, shape later.** For writing (a post, a talk, a pitch): one session pulls raw claims, stories and half-sentences out of you into one file; a second session shapes them into a piece. Skills: `writing-fragments`, `writing-shape` ([credits](../skills/third-party.md)). *Why:* structure too early kills the good material.

**18. Choosing a model: list first, then pick, then change config.** "List every candidate model with price per task and the trade-off. Don't edit any config until I pick." *Why:* agents jump from a catalogue straight to editing settings. And judge models on your real workload, not on whether they answer "say OK" quickly.

## Rules files and skills

**19. One rules file for every tool.** Keep one `AGENTS.md`; make `CLAUDE.md` a symlink to it (`ln -s AGENTS.md CLAUDE.md`) or put `@AGENTS.md` inside it. *Why:* Codex and most others read `AGENTS.md` ([agents.md](https://agents.md), [Codex guide](https://developers.openai.com/codex/guides/agents-md)); Claude Code reads `CLAUDE.md` ([memory docs](https://code.claude.com/docs/en/memory)). Two copies drift within a week. Template: [templates/AGENTS.md](../templates/AGENTS.md).

**20. One skills folder for every tool.** Keep skills in one folder (we use `.agents/skills/`) and point each tool's skills folder at it with a symlink (`ln -s ../.agents/skills .claude/skills`). *Why:* same reason as trick 19. Skills are an open format several tools read ([agentskills.io](https://agentskills.io), [Claude Code skills](https://code.claude.com/docs/en/skills), [Codex skills](https://developers.openai.com/codex/skills/)).

**21. Prove the sharing with a small check script.** A script that fails if a symlink is broken, a skill has no `name`/`description`, or two skills share a name. Run it in CI. *Why:* a broken link fails silently; the agent just doesn't see the skill.

**22. Skills share instructions, not powers.** Permissions, hooks, credentials and memory stay per tool. *Why:* a skill that assumes a permission one tool has will misbehave in another. Write skills as instructions only.

**23. Restart the session after changing the rules or adding a skill.** *Why:* most agents read their startup files once, at the start. A running session does not see the new rule. *Fails when:* you test the new rule in the old session and conclude it does not work.

**24. Explained it twice? Make it a skill.** Skill: [`scaffold-skill`](../skills/scaffold-skill/SKILL.md). *Why:* a skill is loaded only when needed, so it costs nothing until it is used.

**25. Every hard rule carries its incident.** One line after the rule: "(We dropped a column by hand once and left it in the schema; production broke.)" *Why:* agents, like people, respect rules they understand, and the incident tells them where the edge is.

**26. Code in English; only user-facing text is translated.** Identifiers, keys, comments, commit messages in English. *Why:* models and tools work best in it, and a mixed codebase is hard to search.

**27. Borrow good skills before writing your own.** React performance, copywriting, pricing, landing pages: someone has already written a good one. Our credited list: [third-party.md](../skills/third-party.md).

## Agents and parallel work

**28. One worktree per agent.** `git worktree add ../proj-feature-x -b feat/x`. Never two agents in one checkout. *Why:* we had commits land on the wrong branch because another session switched the shared checkout under them. [git worktree docs](https://git-scm.com/docs/git-worktree).

**29. Check the branch in the same command as the commit.** `[ "$(git branch --show-current)" = feat/x ] && git commit -m "..."`. *Why:* a printed branch name is read once and forgotten; a hard check stops the commit. Another session can switch branches between two of your commands.

**30. Chain checks with `&&` or `if`, never `;`.** `check; commit` runs the commit even when the check fails. `if check; then commit; fi` does not.

**31. Never stash, `checkout --` or `reset` in a shared checkout.** To look at an old version: `git show HEAD:path/to/file`. *Why:* a stash once pulled other agents' unsaved work out of the tree for ten seconds while the app was hot-reloading. [git stash docs](https://git-scm.com/docs/git-stash): a stash takes *all* uncommitted changes, not just yours.

**32. Never `git add -A`.** Add explicit paths, and refuse to commit if the staging area already holds something you did not stage (`git diff --cached --name-only`). *Why:* one commit swept another agent's staged files in under its own message.

**33. Merge in a throwaway worktree.** Do merges and cherry-picks in a separate worktree and bring over only the resolved result. *Why:* conflict markers written to disk in a watched folder broke the running app for everyone using it.

**34. With a dev server watching, write each edit in one go.** Add the import and its use in the same edit. *Why:* a half-written file gets served and the app crashes mid-session.

**35. A fresh worktree has no `.env`.** Ignored files stay behind. A build that "fails" in a new worktree may just be missing a secret. Copy or link `.env` first, then judge. In a monorepo, don't borrow another checkout's `node_modules` either: the workspace links inside it point back at that checkout's packages, so your checks run against its source and you get red that isn't yours or green that isn't real. Install fresh in the worktree (with pnpm it is quick, packages come from a shared store).

**36. Agents fold into one branch; a human merges.** Agents commit to an integration branch and open pull requests. They never merge and never push `main`. One branch and one pull request per initiative, phases as separate commits, no stacks of dependent pull requests.

**37. Overnight work as a relay.** A chain of fresh sessions sharing one committed ledger: open questions for you, health, standing rules, backlog, a log. Each iteration does one item, commits, writes the ledger, exits. Skill: `relay` ([where to get it](../skills/README.md#also-by-the-author-published-separately)). *Why:* nothing lives long enough to rot, and the morning starts with a draft pull request. *Fails when:* an iteration does three items and the timeout kills all three.

**38. Kill processes by a precise pattern.** `pkill -f "vitest run"`, not `pkill -f vite`. *Why:* a broad pattern once killed a whole fleet of background agents along with the one stuck test run.

**39. Cap how many agents run at once.** *Why:* a machine pinned at full memory crashes and takes every session with it. Skill: `reclaim` ([where to get it](../skills/README.md#also-by-the-author-published-separately)) for getting a pinned machine back. Keep scripts you need again in the repo, not in `/tmp`: a crash or reboot wipes it. And never leave `caffeinate` (the macOS keep-awake command) running without an end: wrap the job (`caffeinate -i ./run.sh`), bind it to a process (`caffeinate -w <pid>`) or give it a time (`caffeinate -t 3600`). A forgotten one kept a closed laptop awake in a bag for hours.

**40. Let it ping your phone.** A hook sends a message when an agent finishes, fails or waits for permission. You stop babysitting terminals. [Hooks docs](https://code.claude.com/docs/en/hooks); our setup is in [my-stack.md](my-stack.md).

## Verification

**41. "Done" means seen working.** Click the real button, re-ask the real question, then report what you saw. Four steps: run the checks, use it, check the side effect where it lands (the database row, the file, the email), take a screenshot. *Why:* we had fixes reported done on green tests and the bug found in the browser minutes later. Skill: [`verify`](../skills/verify/SKILL.md).

**42. "Not verified live", in those words.** If something could not be checked for real, the report says so. *Why:* it is the most honest line in any report, and the one you most need.

**43. `cmd | tail` lies about failure.** The pipe reports `tail`'s exit code, so a failing build looks green. Use `cmd; echo "EXIT=$?"`, or `set -o pipefail` in scripts.

**44. Some builds skip type checking.** A build can be configured to ignore type errors (Next.js: [`typescript.ignoreBuildErrors`](https://nextjs.org/docs/app/api-reference/config/next-config-js/typescript)), and the build output says so in one easy-to-miss line. Run the type checker as its own step.

**45. Run the last check on the exact commit you hand over.** Not on the one before your "small final tweak".

**46. Restart the dev server before measuring.** After any server-side change, restart, then confirm once that the new code is live. *Why:* we spent two evaluation rounds measuring three-hour-old code. And if "I don't see the change": check which folder the running server was started from.

**47. Read what CI actually runs.** A job called "test" may skip your biggest test suite, and path filters decide whether a check runs at all. Open the workflow file.

**48. A suspiciously clean result is a dead measurement.** "Zero differences" can mean the tool silently did nothing (we hit a command flag that works on Linux and not on macOS). Check a clean result against a second source.

**49. Type-checks is not works.** A screen can compile and render with no real data behind it. Check that real data flows through.

## Design

**50. Design from real screens.** Collect several real screens per screen you are designing ([Mobbin](https://mobbin.com) is our source), group them into directions, and pick per screen. Show them as a labelled contact sheet before asking anyone to choose; text descriptions of a design get rejected. More in [my-stack.md](my-stack.md).

**51. Marketing pages use the real product components.** Mount the actual components on sample data. *Why:* drawn replicas look fake and drift from the product within weeks.

**52. Rebuild whole pages, don't patch.** Compare the whole page to the reference and rebuild it in the reference's system. Patching an old page section by section never converges.

**53. Write the taste down, then test for it.** A design rules file (corner radius tiers, one button style, fonts, banned patterns) plus a test that fails when a banned pattern appears. Template: [design-rules.md](../templates/design-rules.md). When something "looks wrong", it is usually inconsistency (mismatched corners, three different greys), not the effect itself. One rule worth stealing: reading text in a sans font, a serif only for the one big display title per screen; a book serif in a chat answer tires the eye.

**54. Build it in the real app, not a mock.** At a real URL, with real navigation. And never put a placeholder where the picture you asked for should go: show nothing, or the real thing.

## Shipping and ops

**55. Agents never touch the production database.** All agent work runs on development branches or local copies. [Neon branching](https://neon.com/docs/introduction/branching) makes a full copy cheap.

**56. Schema change and migration in the same commit.** Never push a schema straight to a shared database; write idempotent SQL (`CREATE TABLE IF NOT EXISTS`). [Drizzle migrations](https://orm.drizzle.team/docs/migrations) as one example. *Why:* a column dropped by hand and left in the schema broke production.

**57. Deploy, check, then promote.** Deploy without moving the domain, check it, then promote, and keep the previous deployment as a rollback target ([promoting](https://vercel.com/docs/deployments/promoting-a-deployment), [instant rollback](https://vercel.com/docs/instant-rollback)). Anything that changes shared hosting settings (environment variables, domains) waits for a human's explicit yes for that exact action.

**58. Read production errors before saying "ready".** `vercel logs --environment production --level error` ([CLI docs](https://vercel.com/docs/cli/logs)). Check production health after every merge.

**59. Agree a spend limit, then let small overruns through.** "Under about a dollar over the limit: go ahead and tell me. Anything bigger or irreversible: ask." *Why:* stopping a long run for cents costs more than the cents.

## Team and process

**60. One record per unit of work.** What, why, how it was verified (or "not verified"), links, next steps. Search before creating one; update the existing record. No secrets, tokens or customer data in it. Skill: [`log-work`](../skills/log-work/SKILL.md).

**61. One task list, not two.** Two lists means one of them is wrong.

**62. Link the release, not the draft.** Tasks folded into one release all link to the pull request a human actually merged.

**63. Team pages read like normal pages.** No agent narration ("overnight run", "as requested"). Write for the colleague who opens it next month.

**64. Open questions go to the human as options at the next conversation.** An unattended run's questions are never left parked in a doc nobody opens.

## Money and models

**65. Bake-off on your own data before switching.** Real tasks with known right answers, several runs per model. *Why:* benchmarks are not your workload, and newer is not always better or cheaper for your task.

**66. Measure cost per task, not per token.** Reasoning models bill their thinking as output, so a cheap per-token price can be an expensive task. Some cheap models also return an empty answer when the reasoning budget runs out: set the reasoning effort explicitly and check for empty output.

**67. Use the slow, cheap tier for work that can wait.** Batch and flex tiers cost less ([Anthropic batch](https://platform.claude.com/docs/en/build-with-claude/batch-processing): half price; [OpenAI flex](https://platform.openai.com/docs/guides/flex-processing): batch rates). Check in the response metadata that the discount was actually applied.

**68. Product videos from code.** [Remotion](https://www.remotion.dev) renders video from React, with text-to-speech narration. Listen to the result: a voice model can silently fall back to a different voice.

## If you build AI products

**69. Let the model decide when to use a tool.** Forcing a search on every turn wastes time on off-topic research.

**70. Check only the risky sentences.** Quotes and numbers with a citation get checked against the source and repaired only on mismatch. A blanket second pass over everything is slow and rarely finds more.

**71. One-click sign-in over pasted API keys.** Setup friction kills adoption with small businesses. Offer OAuth connections by default.

**72. Don't send users away.** Open sources and documents inside the product instead of a new tab somewhere else.

**73. Proactive agents act, with an undo.** Let the agent act by default, each action with accept/undo and an off switch. Anything irreversible or outward-facing (sending, paying, deleting) still waits for approval.

---

More in the same spirit: [how-i-build.md](how-i-build.md) (the loop), [context.md](context.md) (why sessions rot), [my-stack.md](my-stack.md) (the tools), [scaffolding.md](scaffolding.md) (never start from blank), and Anthropic's own [Claude Code best practices](https://www.anthropic.com/engineering/claude-code-best-practices) and [context engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) write-ups.
