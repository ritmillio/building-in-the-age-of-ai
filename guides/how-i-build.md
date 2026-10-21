# How I build with AI agents

The tools and services behind all of this: [my-stack.md](my-stack.md). Seventy-odd smaller habits, each with its prompt or command: [tricks.md](tricks.md). How a new product starts (from a template, never a blank page): [scaffolding.md](scaffolding.md).

The setup behind slides 19-22 of the workshop. I'm a founder running a small team, and AI agents do most of the typing. None of this needs a big team or a special tool; most of it is habits.

## 1. Teach it once, not every day

Three things an agent reads so you don't have to repeat yourself:

| | What | Where |
|---|---|---|
| **Rules file** | How we work, what we never do, where things are. Read first, every session. | `AGENTS.md` at the project root (Claude Code reads it too, unless a `CLAUDE.md` exists; then that file needs `@AGENTS.md` inside or should be a symlink). Template: [`templates/AGENTS.md`](../templates/AGENTS.md) |
| **Skills** | A workflow I explained twice, saved once, called by name: `/verify`, `/grill`, `/relay`. Loaded only when needed, so they don't clutter the desk. | `.claude/skills/<name>/SKILL.md`. Mine: [`skills/`](../skills/). Others': [`skills/third-party.md`](../skills/third-party.md) |
| **Memory** | Decisions, lessons, mistakes it must not repeat. One note per fact, plus an index. | Template: [`templates/memory-index.md`](../templates/memory-index.md) |

The one habit: **corrected the same thing twice? Write it down.** Into the rules file if it's always true, into a skill if it's a procedure, into memory if it's a fact or a decision.

No terminal? A claude.ai Project, a ChatGPT Project, or a Gemini skill (Gems turn into skills from November 2026; OpenAI is retiring custom GPTs) is the same idea: the instructions box is your rules file, the uploaded files are its context, and claude.ai lets you upload skills too ([install guide](../skills/install.md)).

## 2. Never trust "done"

My loop for anything bigger than a one-line fix:

1. **Plan, written to a file.** A plan that lives only in a chat dies with the chat (and rots with it). `draft-plan` turns a conversation into one.
2. **Shred it before building.** `shred-plan` or `grill` check every claim in the plan against reality and hunt for missing failure modes, hidden dependencies and done-criteria nobody can verify. Same idea as the red team in the workshop build.
3. **Build.** Often several agents at once, each in its own copy of the project (a git worktree) so they don't overwrite each other.
4. **Verify.** "Done" is a claim, not a fact. `verify` treats the result like a stranger's pull request: review it adversarially, add the missing tests, run every check, then click through it in a real browser. It loops until a full pass finds nothing new. Without the skill, paste [`templates/review-prompt.md`](../templates/review-prompt.md) into a fresh session.
5. **A human decides** what goes live. Agents open pull requests; they don't merge them.

Found something in step 4? Back to step 1, not a quick patch on top.

## 3. Context hygiene (why the loop works)

Long sessions get worse ([guides/context.md](context.md)). So:

- One task per session. New topic, new session.
- Big reads go to a sub-agent: it reads the pile in its own context and brings back only the conclusion.
- For long jobs, `relay` runs overnight as a chain of **fresh** sessions. Each one reads a ledger committed to git, does one step, writes the ledger, exits. Nothing lives long enough to rot, and in the morning there is a draft pull request to review.

## 4. Small tricks that add up

- **Parallel agents, separate worktrees.** `git worktree add ../proj-feature-x -b feat/x`. The trap: two agents editing the same file. Give each a lane.
- **It asks me with buttons, not paragraphs.** A line in my rules file: every decision comes as a short list of options, recommendation first, with what each costs. Decisions take seconds, and nothing gets buried in prose.
- **It pings my phone.** A hook sends a Telegram message when an agent finishes, fails or waits for permission (`telegram-notify`). I stop babysitting terminals.
- **Real screens before any design.** I collect reference screens (Mobbin, apps I admire), ask for three variants side by side, pick one, then write the taste down ([`templates/design-rules.md`](../templates/design-rules.md)).
- **Checked live, not just "tests pass".** Every UI change is opened in a browser (the agent can drive one) before it counts as done.
- **Every task leaves a written record.** What was done, why, how it was verified, what is still open, in the task tracker (`log-work`). The next session, and the team, can pick it up cold.
- **Report what was NOT verified.** I ask every agent to end with that line. It's the most honest line in the report.

## 5. What I never hand over

- Anything that sends, pays or deletes on a real account: the agent drafts, I approve.
- Customer data in tools without a business agreement and training switched off.
- The decision. Agents can argue every side; the call is mine.

The agent's side of this list, each rule with its reason, is in our rules file: start from [`templates/never-list.md`](../templates/never-list.md).
