# Ask with options (template)

> Paste the rule into your rules file (`AGENTS.md` or `CLAUDE.md`) or into a project's custom instructions. It turns a wall of prose with three questions hidden in it into a list you answer in one message. Tricks [8](../guides/tricks.md#prompting-and-talking-to-the-agent) and [64](../guides/tricks.md#team-and-process).

## The rule

```markdown
## How to ask me things
- Every decision you need from me is a numbered question with 2 to 4 options.
- Option A is your recommendation, labelled "(recommended)", with one line on why.
- Each option says what it costs (time, money, risk) or what it unblocks.
- Questions go at the end of your message, never in the middle of a paragraph.
- If you can decide it yourself and undo it cheaply, decide, and tell me in one line.
- If you are working while I am away, collect the questions in one list and put it
  first in your report. Do not park them in a file I may never open.
```

## What a good ask looks like

```text
1. Where should the sign-up form send its data?
   A. (recommended) A spreadsheet for now. Zero setup, we move it when there are 50+ sign-ups.
   B. The CRM. Half a day of setup, but sales sees leads the same day.
   C. Email to you. Fastest, but nothing is searchable later.

2. The pricing page lists three plans; the spec has two. Which is right?
   A. (recommended) Two, as in the spec. I delete the third.
   B. Three. Tell me what the middle plan includes.
```

You answer `1A, 2B: the middle plan is "Team", up to 5 seats`. Done in one round.

## When it fails

- **Vague options.** "A: do it well, B: do it fast" is not a decision. Each option must be something the agent could start on right now.
- **Too many questions.** More than five in one message means the agent should have decided some of them. Push back: "Decide the ones you can undo."
- **A recommendation without a reason.** Ask for the one line on why; it is how you spot the agent misunderstanding the goal.
