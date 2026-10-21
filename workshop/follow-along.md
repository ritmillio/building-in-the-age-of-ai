# Follow along on your own laptop

In the second half of the workshop we build the room's idea live, prompt by prompt. You can run the same prompts next to us and end up with your own copy: the research, the business case, the spec, the red team and a clickable prototype.

## Before it starts (five minutes)

1. Open one assistant: [Claude](https://claude.ai), [ChatGPT](https://chatgpt.com) or [Gemini](https://gemini.google.com). The free plans are enough for the prompts; web search must be on for prompt 1.
2. Make a fresh **Project** for today and name it after the idea. Claude and ChatGPT call it a Project; Gemini calls it a [notebook](https://support.google.com/gemini/answer/16972047) (Menu, then **New notebook**). Google is rolling notebooks out gradually (checked 2026-10-21), so if you don't see it yet, a new chat is fine.
3. Use a private or test account. **No customer data, nothing confidential.** Everything today is about a made-up product.

## When the room has picked the idea

Paste this as the first message, with the idea in the room's own words:

```
The chosen idea: [the room's idea in 1-2 sentences]. Every following task is about this idea.
```

Then run the prompts in [prompts.md](prompts.md) in order, at your own pace:

| Step | Prompt | What you get |
|---|---|---|
| Validate | 1, 1b, 1c | What real users say, with links you can open, and ideas backed by quotes |
| Decide | 2, 3 | A simple business case, a one-page spec |
| Red team | 3b | The spec attacked by an engineer, a customer who says no, an investor and a risk officer, then fixed |
| Design | 4, 4b, 4c | Three clickable variants from reference screenshots, then your design rules in one file |
| Launch | 5 | A release note and subject lines |

Tips while you go:
- **Open the links.** Prompt 1 gives quotes with sources. Click two or three. If one doesn't say what the AI claims, you've just learned the most important lesson of the day.
- **Long chat getting worse?** Ask for a handoff ([template](../templates/handoff-prompt.md)), start a new chat in the same Project, paste it in.
- **Fell behind?** Skip to prompt 3b. It works on any spec, even a rough one you write yourself.

## The background build (optional, needs a coding agent)

On stage, a coding agent builds a full prototype in the background while we talk ([prompt 0](prompts.md#0-background-build-second-window-claude-code)). To run it yourself you need [Claude Code](https://code.claude.com/docs/en/quickstart), [Codex](https://developers.openai.com/codex) or a similar agent, an empty folder, and a paid plan for the agent. Starting a real product instead of a prototype? Use the template prompt in [guides/scaffolding.md](../guides/scaffolding.md#prompt-start-from-a-template-claude-code).

## Afterwards

- Do [prompt 7](prompts.md#7-the-task-you-hate-most) on a task from your own week.
- Prompts 8-12 are for the rest of the week: [sales call follow-up](prompts.md#8-after-a-sales-call-the-follow-up), [investor update](prompts.md#9-the-monthly-investor-update), [competitor teardown](prompts.md#10-competitor-teardown), [meeting notes into decisions](prompts.md#11-meeting-notes-into-decisions-and-owners) and [a contract's first read](prompts.md#12-contract-first-read-not-legal-advice).
- Building with an agent from here on? [guides/tricks.md](../guides/tricks.md) has the habits that save us the most time, each with the prompt or file and when it fails.
- Turning the idea into a business (interviews, pricing, the first ten customers): [guides/succeed.md](../guides/succeed.md).
- Everything else (guides, skills, templates, links) is in the [repo's README](../README.md).
