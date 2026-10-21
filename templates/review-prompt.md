# Review prompt: a second pair of eyes on a change (template)

> The agent that wrote the change believes its own work. A fresh session that only sees the change does not ([trick 16](../guides/tricks.md#prompting-and-talking-to-the-agent), [tricks 41 to 49](../guides/tricks.md#verification)). Run this in a NEW session, never in the one that did the work.

## The prompt

```text
Role: a senior reviewer who did not write this change and does not trust it.
Context: the change is [the pull request link / `git diff main...HEAD` / the pasted diff].
What it is supposed to do: [one or two sentences, from the task or the ticket].
What must not break: [the flows, data or customers that matter most].
Task: review it. Read every changed file in full, not only the diff lines, and the code that calls it.
Format:
1. Verdict: ship / ship with notes / not ready, in one line.
2. Findings, most serious first. Each: file and line, what goes wrong, a concrete case that triggers it
   (input, state, what the user sees), and the fix.
3. What you could not check, in those words ("not verified": needs a browser, real data, a login).
Check: only report what you can show. No style comments unless they hide a bug.
If you find nothing serious, say so; do not invent findings to fill the list.
```

## After the review

- Ask the agent that wrote the change to fix the findings, then run the review again in another fresh session. Stop when a full pass finds nothing new.
- For anything the reviewer marked "not verified", do it yourself or hand it to an agent with a browser: click the real button, check the row in the database, read the email that was sent.

## Built in, if you use Claude Code

Claude Code ships a `/code-review` command (alias `/review`) and a `/security-review` command ([commands docs](https://code.claude.com/docs/en/slash-commands), checked 2026-10-21). Use them for the first pass; use the prompt above when you want to state the contract ("what it is supposed to do, what must not break") yourself. Our longer version, which also writes the missing tests and uses the feature like a real user, is the [`verify`](../skills/verify/SKILL.md) skill.

## When it fails

- **Same session.** A reviewer that saw the work being written repeats its blind spots. Always a fresh session.
- **No contract.** Without "what it is supposed to do", you get a review of taste. Write the two sentences.
- **Diff only.** A bug often sits in the code that calls the changed lines. Ask for the full files.
- **Green tests as proof.** The review is a hypothesis until someone has used the change for real.
