# FAQ: questions people ask at the workshop


## Getting started

**1. Which tool should I start with: ChatGPT, Claude or Gemini?**
Any of the big three is good enough to start. Pick one, and build one Project (in Claude or ChatGPT, or a Gem in Gemini) with your own context: product, customers, rules, templates. The context you write down matters more than the model, and you can take it with you if you switch.

**2. Which model is the best right now?**
It changes every few months, so don't marry one. Keep your context in plain files (rules, docs, prompts) so switching is cheap. We use different models for different jobs.

**3. Where do I start in my own company?**
With the task you hate most (slide 34). You know it inside out, so you can judge the output; it comes back every week, so it pays back; and you feel the win on day one. Not with a strategy deck.

**4. How do I get my team to actually use it?**
Show a win on a real task, not a demo. Get everyone to level 2: one shared Project with the team's context. Give them two weeks on one hated task each, then compare notes. People adopt what saves them pain, not what they're told to use.

**5. Is a prompt engineering course worth it?**
Mostly no. The wording matters far less than the context. Brief it like a smart new hire: role, context, task, format, check (slide 13).

## Trust and quality

**6. How do I stop it making things up?**
Ask for sources and links, explicitly allow "no data" as an answer, verify every number, law and quote yourself, and know where the frontier is (slide 23). Local law, tax and fresh rules are where it is most confidently wrong.

**7. Can I trust AI research for validating an idea?**
It is a fast first pass over what people already said in public: reviews, forums, competitors. It does not replace talking to customers. Use it to find the questions worth asking, then go and ask real people.

**8. What happens when it's wrong in front of a customer?**
That's why anything that sends, pays or deletes waits for a human (slide 33). The AI drafts, you decide. Start with internal work before anything customer-facing.

**9. How do you check AI-written code?**
The same way you check a junior colleague's code: tests, review, and a human makes the merge decision. Our overnight runs end with a result to review, not a deploy.

**10. If asked for numbers on "faster and better":**
Harvard-BCG field experiment with consultants (Dell'Acqua et al.): inside the frontier, about 12% more tasks, about 25% faster, 40%+ higher quality; outside it, AI users were 19 points less likely to be right. It used an older model; the frontier has moved, but the lesson holds.

## Data, security, law

**11. Is my data safe? Will it train on my data?**
Use a business or team plan where training on your data is off by default, and read the data terms. Free consumer accounts are for public information only. Anonymise customer data where you can.

**12. Is it safe to connect my Gmail or Drive through MCP?**
Start read-only and with one tool. Check what the connector can do: reading is low risk, sending and deleting are not. Keep a human approval on anything that leaves the building.

**13. What about GDPR and the EU AI Act?**
GDPR applies to any personal data you put in, exactly as with any other software vendor: business plan, data processing agreement, minimum data. Most internal productivity use is low-risk under the AI Act; obligations grow when AI makes decisions about people (hiring, credit) or talks to customers without saying it's AI. For your specific case, ask a lawyer; this is general orientation, not legal advice.

**14. Does it work well in Hungarian?**
For drafts, summaries and analysis, yes, the big models handle Hungarian well. Always check legal and tax specifics, and have a native speaker read anything customer-facing.

## Building

**15. Can a non-technical founder build the product with AI?**
The prototype, the landing page and the first user test: yes, today. Production with payments, security and customer data: bring in an engineer to review the fundamentals. Your prototype is input for them, not a replacement.

**16. When do I need to hire engineers?**
When real users and real money depend on it: security, data, payments, scaling. AI made the first version cheap; it didn't make the fundamentals cheap (slide 11).

**17. Will AI replace developers and designers?**
It replaced the waiting and the cheap parts: boilerplate, first drafts. Taste, judgment, architecture and knowing what not to build became more valuable. Small teams that use it well will outrun bigger ones that don't.

**18. How do I get design that doesn't look like every other AI app?**
Don't describe it in adjectives. Show it real reference screens, ask for three variants, pick one, and write your rules down in one file that every request uses (slides 31-32).

**19. How do your overnight runs work? Can I do that without a terminal?**
One command in the evening starts a loop; each lap is a fresh session that leaves a log, and in the morning there's a result to review. Without a terminal: scheduled tasks in Claude (Cowork) or ChatGPT, with connectors. The relay skill is linked from the repo's skills page, but start with scheduled tasks if you don't use a terminal.

## Money

**20. What does it cost?**
A business seat is roughly 20-30 EUR per person per month (check current pricing). Compare it with a few saved hours a week per person. The real cost is the time to set up your context, and that's a one-off.

**21. Isn't this all hype?**
Some of it is. The test is simple: pick the task you hate most, try it for two weeks, and keep it only if it saved you real time. That's the whole method.

## Context (slides 15-18)

**Why does it get worse the longer we chat?**
Every message, the whole conversation is read again from the top, and models use long inputs worse than short ones, especially the middle (context rot). Start a new chat with a short handoff when it drifts.

**Doesn't a million-token window fix that?**
It holds more, it doesn't focus better. Use it for one big read (a contract bundle, a codebase), ask, close. Not for one endless chat.

**Does it remember me between chats?**
Only what a memory feature or a Project puts back on the desk. Keep the important context in files you control, so it survives switching tools.

**What's a sub-agent?**
A helper the agent starts with its own clean desk: it reads the big pile and brings back only the answer, so the main conversation stays sharp.

## How I build (slides 20-22)

**Should I start from a template or from scratch?**
From a template, almost always. Pick the one closest to the shape of your product (a chat app, a SaaS, a bot), deploy it on day one, add your rules, then spend your time on the one thing only you know. We started our product from Vercel's open-source chatbot template. Which template for what, and the commands: guides/scaffolding.md.

**Won't a template lock me in?**
No, you own the code from the first commit. Swap what you won't keep (auth, models, analytics) in the first days, while it's a ten-minute job for an agent.

**Can I get your skills?**
Yes, they are in the repo on the last slide, rewritten generic, plus the third-party ones I use, credited to their authors, with install steps for Claude Code, claude.ai and plain ChatGPT/Gemini.

**Isn't running several agents at once chaos?**
Only if they share files. Each gets its own copy of the project (a git worktree) and its own task; I review each result separately.

## The tricks, agents and selling (guides/tricks.md, war-stories.md, succeed.md)

Links checked 2026-10-21.

**Is this only for developers?**
No. Most of the tricks are about context, briefing, checking and process, and they work in a chat window: [prompting](../guides/tricks.md#prompting-and-talking-to-the-agent), [design](../guides/tricks.md#design), [team and process](../guides/tricks.md#team-and-process). The README has [five steps per role](../README.md#start-here-by-role), and [prompts 8 to 12](prompts.md#after-the-workshop-not-in-the-live-build) are for sales, investors and contracts. The terminal parts (worktrees, overnight runs) are for people who already use one.

**What does running agents all day cost, and which plan do I need?**
Start on the plan you already have. On Anthropic's [pricing page](https://claude.com/pricing) (checked 2026-10-21) Claude Code comes with Pro, Max, Team and Enterprise, not Free; Max is five or twenty times Pro's usage, for people who hit the limit every day. OpenAI's plans also differ mainly by usage; its pricing page blocks automated checks, so look at chatgpt.com/pricing yourself. If you pay through the API: measure cost per task, not per token ([trick 66](../guides/tricks.md#money-and-models)), send work that can wait to the batch tier at half price ([trick 67](../guides/tricks.md#money-and-models)), and agree a spend limit with the agent ([trick 59](../guides/tricks.md#shipping-and-ops)).

**Is it safe to let an agent read my email, my documents or the web?**
Reading is where the risk starts. Text the agent reads can carry instructions (prompt injection), and no filter stops that reliably. Simon Willison's rule, [the lethal trifecta](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/): never give one agent access to your private data, exposure to untrusted content and a way to send things out, all three at once. In practice: connectors read-only first, one at a time, and anything that sends, pays or deletes waits for a human ([trick 73](../guides/tricks.md#if-you-build-ai-products)). The [Claude Code security page](https://code.claude.com/docs/en/security) gives the same advice for coding agents: review commands before you approve them, don't pipe untrusted content straight in, and isolate anything that talks to outside services.

**How do I know the agent really did what it says?**
You don't, until you see it. "Done" means seen working: run the checks, use the thing, find the side effect where it lands, take a screenshot ([tricks 41 to 49](../guides/tricks.md#verification)). Ask for the words "not verified live" when it could not check. [Five of our war stories](../guides/war-stories.md#when-green-was-not-green) are green results that were red.

**What stops an agent from breaking production?**
Rules and permissions, not hope. Agents work on branches and open pull requests; a human merges ([trick 36](../guides/tricks.md#agents-and-parallel-work)). No agent touches the production database; it gets a copy ([trick 55](../guides/tricks.md#shipping-and-ops)). Hosting settings (environment variables, domains) change only after a human says yes to that exact action ([trick 57](../guides/tricks.md#shipping-and-ops)). Every hard rule carries the incident behind it in one line ([trick 25](../guides/tricks.md#rules-files-and-skills)); [war story 12](../guides/war-stories.md#when-the-machine-and-the-data-bite-back) is one of those incidents.

**How many agents can I run at once?**
Start with one, then two. Each gets its own copy of the project (a git worktree, [trick 28](../guides/tricks.md#agents-and-parallel-work)) and its own task. The real limit is how many results you can review well. The laptop has a limit too: [war story 11](../guides/war-stories.md#when-the-machine-and-the-data-bite-back) is a crash with eight agents running ([trick 39](../guides/tricks.md#agents-and-parallel-work)).

**If building is this cheap, why validate first?**
Because the cost moved. Building the wrong thing takes an afternoon now; finding out it is wrong still takes customers. Before you build, talk to five of them about what they did last month and what it cost them ([succeed.md §1](../guides/succeed.md#1-validate-before-you-build)), and ask what they pay today, in money or hours ([§3](../guides/succeed.md#3-price-it)).

**Which model should we use, and when do we switch?**
Whichever wins on your own work. Before switching, run a small bake-off: real tasks with known right answers, several runs per model ([trick 65](../guides/tricks.md#money-and-models)). Benchmarks are not your workload, and the cheapest price per token can be the most expensive task ([the story about money](../guides/war-stories.md#one-more-about-money)).
