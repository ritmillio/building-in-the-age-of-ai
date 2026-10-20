---
name: log-work
description: Record every finished piece of agent work where the team actually reads it (a Notion database, Linear, GitHub issues, or a markdown log), one record per unit of work, with what was done, why, how it was verified, links and open questions. Use at the end of any task that changed code, ran QA, produced research or a plan, or got a decision; and when the user says "log this", "put it on the board", "add a task" or "log a decision".
---

# /log-work: if it is not written down where people read, it did not happen

**Works in:** Claude Code and claude.ai chat, with whatever connector you have (Notion, Linear, GitHub, Google Docs). Without a connector it writes a markdown entry you paste yourself.

Agents produce a lot of work in terminal scrollback that nobody reads. This skill turns each unit of work into one durable record in the team's tracker, written for a human who was not in the session.

## Setup (once, in your rules file)

Write down for the agent:
- **Where records go** per kind of work, for example:

  | Work | Record |
  |---|---|
  | Code change, fix, feature | one task per unit of work, status and PR link kept current |
  | QA / testing pass | one task per real finding + one summary page for the pass |
  | Plan, spec, research | the document lives in the repo; a short page links to it, never a copy of the body |
  | A decision was made, or one is needed | a decisions row: `Approved` or `Proposed` |
  | Outage or incident | an incidents row |
- **Status values** your tracker uses, and who may change them.
- Database or project ids, so the agent does not have to search for them every time.

## The rule that matters: propose, then apply

People and other agents work the tracker every day. An agent that silently flips statuses or invents tasks destroys trust in it.

- **Creating your own record** for the work you just did: do it directly, then report the link.
- **Anything derived** (bulk updates, status changes you inferred, a sync against the repo): show the diff, wait for a yes, then apply.
- **Never delete or archive** anything without an explicit instruction naming that record.

## Workflow

1. **Search before creating.** One wide query (or the ticket id in the branch / PR title). Existing record: update it. None: create one.
2. **Pick the record type** from your table.
3. **Set the state:** in progress while working; in review with the PR link once a PR is open; done only when merged or confirmed by the owner.
4. **Append a work-log entry** to the record's body. Append, never rewrite earlier entries:

   ```
   ## <date> · <agent> · <one-line outcome>
   - Did: ...
   - Why: ...
   - Verified: <tests, commands, live checks, or "not verified">
   - Links: PR, branch, commit, doc path
   - Open: <questions and next steps, or "none">
   ```
5. **Report** the record's link in your final reply.

## Writing for the reader

- Write it as a normal page for a teammate: no agent narration ("I then ran..."), no notes to yourself.
- Titles short and specific; details in the body.
- "Not verified" is an honest and acceptable value. A guessed "verified" is not.

## No connector available

Put the same entry in the PR description or the run log under a `## Log (pending)` heading, and tell the user it still needs to be filed. Never claim it was recorded.

## Never

- One record per commit. One record per unit of work; later commits and PRs update it.
- Restructure databases, views or fields as a side effect. Additive only.
- Put secrets, tokens, connection strings or customers' personal data in the tracker.
