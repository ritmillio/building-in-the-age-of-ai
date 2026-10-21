# Never list (template)

> The short list of things an agent must not do in this project, each with the reason. Keep it inside your rules file (the "Never" section of [AGENTS.md](AGENTS.md)) or as its own file linked from there. A rule with its reason lets the agent judge the case the rule did not foresee ([trick 3](../guides/tricks.md#context)). Add a line every time something goes wrong, and delete the lines that no longer apply.

```markdown
## Never

### Data and accounts
- Never touch the production database. Work on a development branch or a local copy.
  Why: an agent cannot tell a test row from a customer's row.
- Never send, pay, publish or delete anything on a real account without my explicit yes in this session.
  Why: approval for one email is not approval for the next.
- Never paste secrets, tokens or customer data into a chat, a log, a commit or a ticket.
  Why: those places are read by more people and kept longer than you think.

### Git and shared folders
- Never push to `main`. Branch, commit, open a pull request; a human merges.
- Never `git add -A`. Add the files you changed by name.
  Why: other sessions may have work in the same folder.
- Never `git stash`, `git checkout -- .` or `git reset --hard` in a shared checkout.
  Why: those commands take everyone's uncommitted work, not just yours.
- Never run two agents in one folder. One worktree per agent.

### Honesty
- Never say a test passed if you did not run it.
- Never report "done" on green tests alone. Use the thing and say what you saw.
- If something could not be checked for real, write "not verified live".

### This project
- Never [the thing that bit us]. Why: [what happened, one line].
- Never [a word, name or claim that must not appear in public files]. Why: [...].
```

## How to grow it

- When you correct the agent on the same thing twice, ask it: "Add this to the never list, with the reason."
- Keep each line to one action an agent can recognise in the moment ("never run X"), not a value ("be careful with data").
- Ten to twenty lines is plenty. If it grows past that, move project-specific lines into the skill or guide where they matter.

## When it fails

- **No reason.** "Never use library X" gets ignored or applied in the wrong place. "Never use X: it breaks the build on Windows" gets applied right.
- **Rules nobody checks.** For the ones that really matter (secrets, pushes to `main`, production data), add a hard stop as well: branch protection, read-only credentials, a pre-commit secret scan. A rule in a file is a request; a permission is a wall.
