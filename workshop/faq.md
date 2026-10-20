# FAQ: questions people ask at the workshop


## Getting started

**1. Which tool should I start with: ChatGPT, Claude or Gemini?**
Any of the big three is good enough to start. Pick one, and build one Project (or GPT / Gem) with your own context: product, customers, rules, templates. The context you write down matters more than the model, and you can take it with you if you switch.

**2. Which model is the best right now?**
It changes every few months, so don't marry one. Keep your context in plain files (rules, docs, prompts) so switching is cheap. We use different models for different jobs.

**3. Where do I start in my own company?**
With the task you hate most (slide 35). You know it inside out, so you can judge the output; it comes back every week, so it pays back; and you feel the win on day one. Not with a strategy deck.

**4. How do I get my team to actually use it?**
Show a win on a real task, not a demo. Get everyone to level 2: one shared Project with the team's context. Give them two weeks on one hated task each, then compare notes. People adopt what saves them pain, not what they're told to use.

**5. Is a prompt engineering course worth it?**
Mostly no. The wording matters far less than the context. Brief it like a smart new hire: role, context, task, format, check (slide 13).

## Trust and quality

**6. How do I stop it making things up?**
Ask for sources and links, explicitly allow "no data" as an answer, verify every number, law and quote yourself, and know where the frontier is (slide 24). Local law, tax and fresh rules are where it is most confidently wrong.

**7. Can I trust AI research for validating an idea?**
It is a fast first pass over what people already said in public: reviews, forums, competitors. It does not replace talking to customers. Use it to find the questions worth asking, then go and ask real people.

**8. What happens when it's wrong in front of a customer?**
That's why anything that sends, pays or deletes waits for a human (slide 31). The AI drafts, you decide. Start with internal work before anything customer-facing.

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
Don't describe it in adjectives. Show it real reference screens, ask for three variants, pick one, and write your rules down in one file that every request uses (slides 22-23).

**19. How do your overnight runs work? Can I do that without a terminal?**
One command in the evening starts a loop; each lap is a fresh session that leaves a log, and in the morning there's a result to review. Without a terminal: scheduled tasks in Claude Cowork or ChatGPT, with connectors. (Mention only; don't promise to share the internal tool.)

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

## How I build (slides 21-23)

**Can I get your skills?**
Yes, they are in the repo on the last slide, rewritten generic, plus the third-party ones I use, credited to their authors, with install steps for Claude Code, claude.ai and plain ChatGPT/Gemini.

**Isn't running several agents at once chaos?**
Only if they share files. Each gets its own copy of the project (a git worktree) and its own task; I review each result separately.
