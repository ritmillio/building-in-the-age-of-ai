# AGENTS.md (template)

> The rules file every coding agent reads at the start of every session. Codex, Cursor, Gemini CLI and most others read `AGENTS.md`; Claude Code reads `CLAUDE.md`, so either keep one file and symlink the other (`ln -s AGENTS.md CLAUDE.md`) or put `@AGENTS.md` inside `CLAUDE.md`.
> Keep it short. Everything in here sits on the agent's desk in every session, so every line costs attention. Delete what you don't need, and add a line every time you correct the agent on the same thing twice.

## What this project is
- One paragraph: what the product does, for whom, and what "good" means here.
- Where things live: `app/` (web), `api/` (backend), `docs/` (plans and decisions).

## How we work
- Branch from `main`, name branches `feat/<thing>` or `fix/<thing>`. Never push to `main`.
- Small, revertable commits. One pull request per unit of work.
- Before saying "done": run `<test command>`, `<lint command>`, `<typecheck command>` and open the changed screen in a browser.
- Write plans, specs and decisions into `docs/`, not only into the chat.

## Never
- Never commit secrets, tokens or customer data.
- Never run destructive commands (drop tables, force-push, delete files you did not create) without asking first.
- Never send, pay or delete anything on a real account without explicit approval.
- Never say a test passed if you did not run it. If a step was skipped, say so.

## How to ask me things
- Ask decisions as a short list of options, recommendation first, with what each option costs.
- Report in a few bullets: what changed, how it was verified, what was NOT verified.

## Conventions
- Language, framework and style rules that are not obvious from the code.
- Naming: files `kebab-case`, components `PascalCase`.
- Design: follow `design-rules.md`.

## Gotchas
- Things that bit us before, one line each, with the fix. Example: "The dev server caches X; restart it after changing Y."
