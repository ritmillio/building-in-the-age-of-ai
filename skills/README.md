# Skills

Skills written by the repo author, Zoltán Fodor, from the workflows he uses every day to build with AI agents. Each one is a folder with a `SKILL.md`, in the open Agent Skills format: YAML frontmatter (`name`, `description`) and Markdown instructions.

## In this folder

| Skill | What it does | Works in |
|---|---|---|
| [`grill`](grill/SKILL.md) | Pressure-tests a plan before anything is built: one question at a time, ends with decisions, open questions and a recommendation | Claude Code + claude.ai chat |
| [`spike`](spike/SKILL.md) | A throwaway prototype that answers exactly one question, time-boxed, then deleted | Claude Code + claude.ai chat (as an HTML artifact) |
| [`verify`](verify/SKILL.md) | Adversarial loop after building: gates, edge-case review, missing tests, real use, repeated until a pass finds nothing new | Claude Code |
| [`root-cause`](root-cause/SKILL.md) | Reproduce, localise, minimise, one hypothesis at a time, name the violated assumption, smallest fix, regression guard | Claude Code (partly in chat) |
| [`log-work`](log-work/SKILL.md) | One record per unit of work in your tracker: what, why, how verified, links, open questions | Claude Code + claude.ai chat (with a connector) |
| [`scaffold-skill`](scaffold-skill/SKILL.md) | Turns a workflow you keep re-explaining into a new skill | Claude Code + claude.ai chat |

## Also by the author, published separately

These live in the author's skills library, [github.com/ritmillio/skills](https://github.com/ritmillio/skills) (MIT), so they are installed from there rather than copied here:

| Skill | What it does |
|---|---|
| `relay` | Unattended work for hours on its own worktree and draft PR. Every iteration is a fresh process that hands a committed ledger to the next, so nothing lives long enough to suffer context rot |
| `draft-plan` | Turns a conversation into a written plan: diagnosis, scope, workstreams with proofs of done, open questions |
| `shred-plan` | Tears a written plan apart: verifies every claim with evidence, ranks the gaps by severity |
| `telegram-notify` | A Telegram ping when the agent finishes, commits or gets stuck |
| `reclaim` | Gets a dev machine pinned by agents and build watchers back |
| `morning-brief`, `safe-migration`, `vercel-triage`, `collect-bills`, `mac-compromise-check` | Founder routines: a daily brief, careful database migrations, deploy triage, invoice collection, a laptop security check |

```bash
npx skills@latest add ritmillio/skills
```

## Skills by other people

The third-party skills I use, and other collections worth knowing, each credited to its author with repo, license and where it works: [third-party.md](third-party.md). Install them from their own repos, not from here.

## Install

Step-by-step for every surface (Claude Code, claude.ai, the Claude API, Codex and other coding agents, ChatGPT, Gemini): [install.md](install.md).

The short version:

```bash
# Claude Code, for every project
cp -r skills/grill ~/.claude/skills/

# any agent the cross-agent installer detects
npx skills@latest add <owner>/<repo>
```

No terminal? In claude.ai, zip a skill folder and upload it as a skill. In ChatGPT or Gemini, paste the body of `SKILL.md` into a Project or Gem as its instructions: you lose the automatic triggering, not the method.

## License

MIT, like the rest of this repository.
