# Building in the Age of AI

Slides, prompts, skills, templates and a big list of resources from my hands-on workshop for founders, product people and operators: how to go from an idea to a validated prototype with AI, how to work with agents without the chaos, and what changed when everyone can build.

No coding needed to use most of this. If you write code, there's more for you in `skills/` and `templates/`.

## If you only do one thing

Pick the task you hate most. Hand it to an AI assistant with [prompt 7](workshop/prompts.md#7-the-task-you-hate-most), try it for two weeks, keep it or drop it. You know that task inside out, so you can judge the output, and you'll feel the win on day one.

## What's in here

| | |
|---|---|
| [`workshop/slides.pdf`](workshop/slides.pdf) | The deck (37 slides). Part 1, the talk: how building changed, context, how I build, raising money. Part 2: the live build, then where to start |
| [`workshop/follow-along.md`](workshop/follow-along.md) | Laptop open? How to run the live build next to us: which assistant, a fresh Project, which prompts in which order |
| [`workshop/prompts.md`](workshop/prompts.md) | Every prompt from the live build, in order: research real customer words, business case, one-page spec, red team, prototype with references, design rules, launch kit, ops automation |
| [`workshop/prompt-pack.pdf`](workshop/prompt-pack.pdf) | The 4-page handout |
| [`workshop/faq.md`](workshop/faq.md) | The questions people ask, with short answers |
| [`guides/context.md`](guides/context.md) | Context windows, tokens, context rot, why a million tokens is not a better memory, and what to do about it. Sourced. |
| [`guides/scaffolding.md`](guides/scaffolding.md) | Never start from a blank page: which template fits which product (Vercel Chatbot, next-forge, eve, Chat SDK, create-next-app, Turborepo, Expo, Tauri…), deploy first, make it yours, give the agent its hands. Every command checked. |
| [`guides/how-i-build.md`](guides/how-i-build.md) | My setup: rules file, skills, memory, the plan → shred → build → verify loop, parallel agents, small tricks |
| [`guides/tricks.md`](guides/tricks.md) | Seventy-odd working habits for building faster with AI: context, prompting, rules files and skills, parallel agents, verification, design, shipping, money. Each with the exact prompt or command and when it fails |
| [`guides/my-stack.md`](guides/my-stack.md) | Every tool and service I use: agents, MCP servers, where I find designs, and what the product runs on (Vercel, Neon, Turbopuffer, Trigger.dev, Expo…) |
| [`guides/fundraising.md`](guides/fundraising.md) | Raising money in the AI era, the "thin wrapper" problem, what counts as a moat now. Sourced. |
| [`skills/`](skills/) | My skills, rewritten for anyone to use, plus a credited catalogue of other people's skills and install steps for Claude Code, claude.ai, ChatGPT and Gemini |
| [`templates/`](templates/) | `AGENTS.md` rules file, `design-rules.md`, a handoff prompt, a memory index |
| [`resources.md`](resources.md) | Hundreds of links I'd actually send a friend: official guides, agents, skills, MCP, prototyping, design, ops automation, evals, security, research, newsletters, books, free courses |
| [`open-source.md`](open-source.md) | Open-source projects for building with AI, licence-checked: coding agents, agent frameworks, MCP, local models, app builders, RAG, evals, browser agents, UI kits. Non-OSI licences and archived repos flagged |

## The ideas in one screen

- **AI didn't take the work, it took the waiting.** The bottleneck is now you: taste, customer knowledge, judgment.
- **Never start from a blank page.** Start from a template that already runs, add your rules, spend your time on the one job only you know.
- **Brief it like a smart new hire:** role, context, task, format, check ("no data" is an allowed answer).
- **Context is a desk.** What's on it, it knows. The fuller the desk, the worse it listens. One task per chat; hand off and start fresh.
- **Teach it once:** a rules file, skills, memory. Corrected the same thing twice? Write it down.
- **Never trust "done".** Plan, shred the plan, build, verify, then a human decides.
- **Red team your own plan** before the market does.
- **Good design comes from references and written-down taste,** not adjectives.
- **It drafts, you approve.** Anything that sends, pays or deletes waits for you.
- **Your product is not a markdown file.** If a prompt gets most of your output, you have a demo, not a company. Answer "why can't OpenAI ship this next quarter?" with what you own.

## Credits

Third-party skills are listed with their authors, repos and licenses in [`skills/third-party.md`](skills/third-party.md); nothing from them is copied into this repo. Facts in the guides link to their sources and carry the date they were checked. Tools and models change monthly: if a link or number is out of date, open an issue or a pull request.

## License

Skills and templates: MIT (see [LICENSE](LICENSE)). Slides, guides and prompts: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/), share and adapt with attribution.

Made by [Zoltán Fodor](https://zoltanfodor.dev).
