---
name: scaffold-skill
description: Turn a workflow you keep re-explaining into a reusable skill (a folder with a SKILL.md). Use when the user says "create a skill", "make this repeatable", "let's codify this", or when you notice the same instructions being given across sessions.
---

# /scaffold-skill: explain it twice, save it once

**Works in:** Claude Code (writes the folder into your project or user skills directory) and claude.ai chat (produces the SKILL.md for you to zip and upload in Settings, Capabilities, Skills).

## Good candidates

- A workflow that touches the **same files in the same order** every time ("add a new AI tool": tool file, prompt, tool list, renderer, types).
- A workflow with **gotchas that bit you before** (migration numbering, a field that must stay in sync, a deploy step people forget).
- Something that is half-written in your rules file but still gets done wrong.

## Bad candidates

- One-off tasks: just do them.
- Something an existing skill already covers: check your installed skills first.
- Something that is really a script: write the script, and at most a one-line skill that runs it.

## Collect before writing

1. **Name / trigger:** a short kebab-case verb or noun (`/root-cause`, `/spike`). Avoid names that clash with built-in commands.
2. **Goal in one sentence:** what does success look like?
3. **Inputs:** what does the user hand over (paths, ticket ids, free text, a screenshot)?
4. **Done state:** what exists when the skill finishes (files, commits, a report, a passing test)?
5. **Known gotchas:** what went wrong before.

If one is missing, ask one focused question. Do not invent.

## Layout

```
<skills dir>/<name>/
  SKILL.md        required: frontmatter + body
  references/     optional: long reference material the body links to
  scripts/        optional: helper scripts the body runs
```

`SKILL.md` alone is enough for most skills. Move detail into `references/` once the body passes about 150 lines; the agent reads the description first, the body only when the skill fits, and references only when the body points there.

## Template

```markdown
---
name: <kebab-case-name>
description: <what it does + when to use it, including the phrases a user would type. The agent decides relevance from this line alone, so be specific.>
---

# /<name>: <one-line hook>

<One paragraph: what problem this solves and why it exists.>

## When to use
- <case>

## When not to use
- <case, and which skill fits better>

## Workflow
1. <one concrete step per line, with exact commands or file paths>

## Rules that always apply
- <project conventions the agent keeps getting wrong>

## Report
<how the result is reported back: lead with the outcome, then evidence, then what was not verified>
```

## Naming

- Short, kebab-case. If the name needs explaining in the description, rename it.
- Avoid overlapping built-ins (`/run`, `/review`, `/init`, `/commit`).

## After writing

1. Show the user the path of the new `SKILL.md` to review.
2. Tell them it should show up in `/skills` straight away (Claude Code and Codex watch skill folders); if it does not, run `/reload-skills` in Claude Code or restart the tool.
3. If the skill is useful beyond this project, suggest moving it to the user-level skills directory, and ask before writing outside the project.
