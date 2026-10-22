# Building in the Age of AI

Slides, prompts, skills, templates and a big list of resources from my hands-on workshop for founders, product people and operators: how to go from an idea to a validated prototype with AI, how to work with agents without the chaos, and what changed when everyone can build.

No coding needed to use most of this. If you write code, there's more for you in `skills/` and `templates/`.

## If you only do one thing

Pick the task you hate most. Hand it to an AI assistant with [prompt 7](workshop/prompts.md#7-the-task-you-hate-most), try it for two weeks, keep it or drop it. You know that task inside out, so you can judge the output, and you'll feel the win on day one.

## Start here, by role

Pick the row closest to you and do the five steps in order. None of them needs more than an evening.

**Founder, not technical**
1. Do [the one thing](#if-you-only-do-one-thing) above, on the task you hate most.
2. Before you build anything, test the idea with customers: [succeed.md §1](guides/succeed.md#1-validate-before-you-build) (interviews, review mining, a landing page with prices).
3. Run the live-build prompts on your own idea, in order: [prompts.md](workshop/prompts.md). Were you in the room? [follow-along.md](workshop/follow-along.md) has the order. For the rest of the week (follow-ups, investor update, contracts): [prompts 8 to 12](workshop/prompts.md#after-the-workshop-not-in-the-live-build).
4. Learn why long chats get worse and what to do instead: [context.md §7](guides/context.md#7-practical-rules-for-the-audience-one-slide), then [trick 1](guides/tricks.md#context) and [tricks 8 to 13](guides/tricks.md#prompting-and-talking-to-the-agent).
5. Before you talk to investors: [fundraising.md](guides/fundraising.md) on the "thin wrapper" question, and [succeed.md §7](guides/succeed.md#7-the-few-numbers-that-matter-early) for the numbers that matter early.

**Product person or operator**
1. Brief it like a smart new hire (role, context, task, format, check): copy the shape from [prompts 1 to 3](workshop/prompts.md#1-research-real-customer-words-starts-during-the-talk-read-it-at-slide-29).
2. Make it ask with options, report briefly and stop at the scope you named: [tricks 8 to 10](guides/tricks.md#prompting-and-talking-to-the-agent).
3. Red team your spec before anyone builds it: [prompt 3b](workshop/prompts.md#3b-red-team-slide-30-the-most-valuable-step).
4. Design from real screens and written-down taste: [tricks 50 to 54](guides/tricks.md#design) and [design-rules.md](templates/design-rules.md).
5. Decide, price and sell with evidence: [succeed.md §2 to §5](guides/succeed.md#2-decide-with-a-number-not-a-feeling).

**Developer**
1. One rules file and one skills folder for every tool: [AGENTS.md template](templates/AGENTS.md), [tricks 19 to 24](guides/tricks.md#rules-files-and-skills).
2. Start from a template that runs and deploy it before you change anything: [scaffolding.md](guides/scaffolding.md).
3. Plan, shred the plan, build, verify: [how-i-build.md §2](guides/how-i-build.md#2-never-trust-done), the [`verify`](skills/verify/SKILL.md) skill and the [review prompt](templates/review-prompt.md) for a fresh session.
4. Before you run agents in parallel, read [war stories 1 to 5](guides/war-stories.md#when-agents-share-a-checkout) and [tricks 28 to 39](guides/tricks.md#agents-and-parallel-work).
5. Install the skills you want: [skills/install.md](skills/install.md) covers Claude Code, claude.ai, Codex, ChatGPT and Gemini.

**Team lead**
1. One shared rules file, every hard rule with the incident behind it: [tricks 19 and 25](guides/tricks.md#rules-files-and-skills) and the [never list](templates/never-list.md).
2. Agents work on branches and open pull requests, a human merges, nobody's agent touches production: [trick 36](guides/tricks.md#agents-and-parallel-work), [tricks 55 to 58](guides/tricks.md#shipping-and-ops).
3. "Done" means seen working, and "not verified" is said out loud: [tricks 41 to 49](guides/tricks.md#verification).
4. One record per unit of work, one task list: [tricks 60 to 64](guides/tricks.md#team-and-process) and the [`log-work`](skills/log-work/SKILL.md) skill.
5. Pick models on your own data and measure cost per task: [tricks 65 to 67](guides/tricks.md#money-and-models) and [the cheapest model story](guides/war-stories.md#one-more-about-money). Then hand the team [war-stories.md](guides/war-stories.md) as a checklist.

## What's in here

| | |
|---|---|
| [`workshop/slides.pdf`](workshop/slides.pdf) | The deck: 38 slides plus 4 Q&A backup slides (small tricks, five prompts to steal, files I never start without, code got cheap). Part 1, the talk: how building changed, context, how I build, raising money. Part 2: the live build, then where to start |
| [`workshop/follow-along.md`](workshop/follow-along.md) | Laptop open? How to run the live build next to us: which assistant, a fresh Project, which prompts in which order |
| [`workshop/prompts.md`](workshop/prompts.md) | Every prompt from the live build, in order: research real customer words, business case, one-page spec, red team, prototype with references, design rules, launch kit, ops automation; then five for after the workshop: sales follow-up, investor update, competitor teardown, meeting decisions, contract first read |
| [`workshop/prompt-pack.pdf`](workshop/prompt-pack.pdf) | The 5-page prompt pack: the live-build prompts plus prompts 8-12 for after the workshop |
| [`workshop/faq.md`](workshop/faq.md) | The questions people ask, with short answers |
| [`guides/context.md`](guides/context.md) | Context windows, tokens, context rot, why a million tokens is not a better memory, and what to do about it. Sourced. |
| [`guides/scaffolding.md`](guides/scaffolding.md) | Never start from a blank page: which template fits which product (Vercel Chatbot, next-forge, eve, Chat SDK, create-next-app, Turborepo, Expo, Tauri…), deploy first, make it yours, give the agent its hands. Every command checked. |
| [`guides/how-i-build.md`](guides/how-i-build.md) | My setup: rules file, skills, memory, the plan → shred → build → verify loop, parallel agents, small tricks |
| [`guides/tricks.md`](guides/tricks.md) | Seventy-odd working habits for building faster with AI: context, prompting, rules files and skills, parallel agents, verification, design, shipping, money. Each with the exact prompt or command and when it fails |
| [`guides/war-stories.md`](guides/war-stories.md) | Twelve real incidents from building with agents (a stash that emptied a shared folder, a build piped through `tail`, a column dropped by hand) with what each cost and the rule it left |
| [`guides/my-stack.md`](guides/my-stack.md) | Every tool and service I use: agents, MCP servers, where I find designs, and what the product runs on (Vercel, Neon, Turbopuffer, Trigger.dev, Expo…) |
| [`guides/succeed.md`](guides/succeed.md) | The go-to-market half: validate before you build (customer interviews, review mining, a landing page with prices), the product-market-fit question, pricing, the first ten customers, selling through partners, staying small, the few numbers that matter early. Each with a sourced rule and a prompt to paste |
| [`guides/fundraising.md`](guides/fundraising.md) | Raising money in the AI era, the "thin wrapper" problem, what counts as a moat now. Sourced. |
| [`skills/`](skills/) | My skills, rewritten for anyone to use, plus a credited catalogue of other people's skills and install steps for Claude Code, claude.ai, the Claude API, Codex, Cursor and other coding agents, ChatGPT and Gemini |
| [`templates/`](templates/) | `AGENTS.md` rules file, `design-rules.md`, a handoff prompt, a memory index, a never list, the ask-with-options rule, a review prompt for a fresh session, customer interview notes, a phone-notify hook |
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
