# Context: what the AI actually "knows", and why long chats get worse

The guide behind slides 15-18 of the workshop. The short version: the context window is a desk. Everything on it, the model can use; nothing else exists for it. The fuller the desk, the worse it listens (context rot). A bigger desk is not a better memory. Keep it clean: one task per chat, hand off and start fresh, rules in a file, sub-agents for big reads, memory you can read.

---

Checked against vendor docs and the original papers on **2026-10-20**. Model names and limits change every few months, so re-check section 3 before you rely on a number. Quotes are verbatim from the source.

---

## 1. What a context window is (plain language)

**In one line:** the context window is the model's working memory for one conversation. It is everything the model can "see" when it writes its next answer: your instructions, the whole chat so far, any files or tool results, and the answer it is writing.

- Anthropic's definition: *"The 'context window' refers to all the text a language model can reference when generating a response, including the response itself. This is different from the large corpus of data the language model was trained on, and instead represents a 'working memory' for the model."* [Claude docs: Context windows](https://platform.claude.com/docs/en/build-with-claude/context-windows)
- **What counts:** *"Everything in the request counts toward the context window: the system prompt, every message in `messages` (including tool results, images, and documents), and your tool definitions. The output Claude generates for the turn, including its extended thinking, counts too."* (same page)
- **It grows every turn.** In a chat, each new message re-sends the whole history. Turn 20 carries turns 1 to 19 with it. That is why long chats get slow, expensive and confused.
- **The model doesn't "remember" between chats.** Unless a product feature (memory, projects, CLAUDE.md) puts information back into the window, a new chat starts empty. Claude Code's docs say it directly: *"Each Claude Code session begins with a fresh context window."* [How Claude remembers your project](https://code.claude.com/docs/en/memory)
- **Training data ≠ context.** What the model learned in training is its general knowledge; the context window is what it is looking at right now. Put the facts you care about *in* the context.

**Analogy:** a very smart new contractor with no memory of yesterday. Each morning you hand them a folder (the context). They only know what is in the folder plus general world knowledge. A thick folder with the important page buried in the middle is worse than a thin folder with exactly the right pages.

## 2. Tokens

- Models read and write **tokens**, not words. A token can be a word, part of a word, punctuation or a space-plus-word.
- OpenAI's rule of thumb for English: *"1 token is approximately 4 characters. 1 token is approximately three-quarters of a word. 100 tokens are approximately 75 words."* Other languages split differently. [OpenAI Help: Understanding and counting tokens](https://help.openai.com/en/articles/4936856-what-are-tokens-and-how-to-count-them)
- Anthropic's sizing note for current Claude models: *"1M tokens is roughly 555k words or 2.5M Unicode characters on the current tokenizer (introduced with Claude Opus 4.7); models before it fit about 750k words in 1M tokens. 200k tokens is roughly 150k words."* [Claude Models overview](https://platform.claude.com/docs/en/about-claude/models/overview). So the same text costs a different number of tokens on different models.
- Google's sizing note: 1 million tokens is about *"50,000 lines of code"*, *"eight average-length English novels"*, or *"transcripts of over 200 average-length podcast episodes."* [Gemini API: Long context](https://ai.google.dev/gemini-api/docs/long-context)
- **Reasoning ("thinking") tokens count too.** OpenAI: *"Reasoning tokens are not visible as answer text, but they count toward output usage and are billed as output tokens."* Anthropic: *"With thinking, all input and output tokens, including thinking tokens, count toward the context window limit."*
- **Try it live:** [OpenAI Tokenizer](https://platform.openai.com/tokenizer) shows how a sentence splits into tokens. [Claude token counting API](https://platform.claude.com/docs/en/build-with-claude/token-counting) counts a full request.
- **Why it matters for builders:** you pay per token, rate limits are in tokens, and quality degrades as tokens pile up (section 4).

## 3. Current context window sizes of flagship models (API, as of 2026-10-20)

| Vendor | Model (API ID) | Context window | Max output | Source |
|---|---|---|---|---|
| Anthropic | Claude Fable 5.1 (`claude-fable-5-1`) | **1M** | 128K | [Models overview](https://platform.claude.com/docs/en/about-claude/models/overview) |
| Anthropic | Claude Opus 5.5 (`claude-opus-5-5`), the recommended default | **1M** | 128K | same |
| Anthropic | Claude Sonnet 5.5 (`claude-sonnet-5-5`) | **1M** | 128K | same |
| Anthropic | Claude Haiku 5.5 (`claude-haiku-5-5`) | **1M** | 128K | same |
| OpenAI | GPT-6 Astra (`gpt-6-astra`), the recommended default | **1.05M** (1,050,000) | 128K | [OpenAI Models](https://developers.openai.com/api/docs/models), [GPT-6 Astra page](https://developers.openai.com/api/docs/models/gpt-6-astra) |
| OpenAI | GPT-6.1 Sol (`gpt-6.1-sol`) | **1.05M** | 128K | [OpenAI Models](https://developers.openai.com/api/docs/models) |
| OpenAI | GPT-6 Luna (`gpt-6-luna`) | **1.05M** | 128K | same |
| Google | Gemini 4 Argon (`gemini-4-argon`, stable) | **1,048,576** (shared by input + output) | 65,536 by default; up to 1,048,576 with "long decode" | [Gemini 4 Argon model page](https://ai.google.dev/gemini-api/docs/models/gemini-4-argon) |

Notes for accuracy:
- **All three vendors' flagships are at ~1M tokens.** Anthropic: *"For every model with a 1M-token context window, 1M is the default: you don't need a beta header, and long-context requests are billed at standard pricing, except on Claude Haiku 5.5, where prompts over 100,000 tokens cost more."* Older Claude models (for example Sonnet 4.5, deprecated) have 200K. [Context windows](https://platform.claude.com/docs/en/build-with-claude/context-windows)
- **OpenAI charges more for long prompts:** on GPT-6 Astra, *"Prompts with more than 272K input tokens are priced at 2x input and cache rates and 1.5x output for the full request."* [GPT-6 Astra](https://developers.openai.com/api/docs/models/gpt-6-astra)
- **Gemini:** the Gemini models page lists many current models (Gemini 3.x Flash / Flash-Lite, Gemini 3.1 Pro preview, etc.) but gives a token limit on that page only for Gemini 4 Argon. No current Gemini model is described as 2M. Check each model page for its own limit. [Gemini models](https://ai.google.dev/gemini-api/docs/models)

### In the consumer apps the window is often smaller than the API

| App | What the vendor states | Source |
|---|---|---|
| Claude (paid plans) | Opus 5.5, Sonnet 5.5 and Haiku 5.5 at **1M**; Sonnet 4.6 at 500K; *"Outside of these models, Claude's context window size is 200K."* On paid plans with code execution on, *"Claude summarizes earlier messages to make room for new content."* Free plan not covered by the article. | [How large is the context window on paid Claude plans?](https://support.claude.com/en/articles/8606394) |
| Gemini app | No AI plan: **32k**; Google AI Plus: **128k**; AI Pro and AI Ultra: **1 million** tokens | [Gemini Apps limits & feature availability](https://support.google.com/gemini/answer/16275805) |
| ChatGPT | Varies by plan and by model (Instant vs Thinking). **Not verified:** OpenAI's pricing page blocked automated access; third-party summaries disagree. Check chatgpt.com/pricing live before quoting a number. | — |

**In short:** "1M tokens" is roughly 2,000+ pages of text. Big, but a bigger window is not a better memory (next section).

## 4. Context rot: more context makes models worse

**The one-liner:** models get less accurate as the context gets longer, even on easy tasks. A full window is a noisy window.

Anthropic now uses the term in its official docs: *"A larger context window allows the model to handle more complex and lengthy prompts, but more context isn't automatically better. As token count grows, accuracy and recall degrade, a phenomenon known as context rot. This makes curating what's in context just as important as how much space is available."* [Context windows](https://platform.claude.com/docs/en/build-with-claude/context-windows)

### Chroma Research, "Context Rot" (July 14, 2025)
- Authors: Kelly Hong, Anton Troynikov, Jeff Huber (Chroma). [Context Rot](https://www.trychroma.com/research/context-rot)
- Tested **18 LLMs** (including GPT-4.1, Claude 4, Gemini 2.5, Qwen3).
- Findings:
  - Performance drops faster with length when the question and the answer ("needle") use **different words** (low semantic similarity).
  - **Distractors** (similar but wrong passages) hurt; even one distractor lowers accuracy, four lower it more.
  - Counter-intuitive: **shuffled** haystacks (random sentence order) scored *better* than coherent essays across all 18 models.
  - On **LongMemEval** (chat-memory questions), every model did better with a focused ~300-token prompt than with the full ~113K-token history.
  - Even **repeating a sequence of words** gets less reliable as input grows.
- Conclusion: models *"do not maintain consistent performance across input lengths, even on simple tasks"*, and how information is presented matters as much as whether it is present.

### "Lost in the Middle" (Liu et al., 2023)
- Nelson F. Liu, Kevin Lin, John Hewitt, Ashwin Paranjape, Michele Bevilacqua, Fabio Petroni, Percy Liang. arXiv 2307.03172 (v1 6 Jul 2023, v3 20 Nov 2023); accepted to TACL. [arXiv](https://arxiv.org/abs/2307.03172)
- Finding: accuracy is highest when the relevant information is at the **start or end** of the input and drops significantly when it is in the **middle**, even for long-context models. (The "U-shaped" curve.)
- **Practical rule:** put the most important instructions at the top and the actual question at the bottom. Google gives the same advice: *"the model's performance will be better if you put your query / question at the end of the prompt."* [Gemini long context](https://ai.google.dev/gemini-api/docs/long-context)

### NoLiMa (Modarressi et al., ICML 2025)
- Ali Modarressi, Hanieh Deilamsalehy, Franck Dernoncourt, Trung Bui, Ryan A. Rossi, Seunghyun Yoon, Hinrich Schütze. arXiv 2502.05167. [arXiv](https://arxiv.org/abs/2502.05167)
- Removes literal word overlap between question and answer (so the model must reason, not keyword-match).
- **13 LLMs** claiming ≥128K context. *"At 32K, 11 of the 13 models fall below 50% of their short-context baselines."* GPT-4o fell from 99.3% to 69.7%.

### Other useful evidence
- **RULER** (Hsieh et al., 2024): advertised context size is larger than the size models can use well. [arXiv 2404.06654](https://arxiv.org/abs/2404.06654)
- **Needle in a Haystack** (Greg Kamradt): the original single-fact retrieval test; models pass it easily, which is why it overstates real long-context ability. [GitHub](https://github.com/gkamradt/needle-in-a-haystack)
- **Google's own caveat:** single-needle retrieval is strong, but *"the model does not perform with the same accuracy"* when several pieces of information must be found. [Gemini long context](https://ai.google.dev/gemini-api/docs/long-context)
- **Drew Breunig's failure taxonomy:** context poisoning (an error gets repeated), distraction (the model over-focuses on history), confusion (irrelevant tools/info), clash (contradictory info). [How Long Contexts Fail](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html)

**In short:** "The window is a desk, not a filing cabinet. A clean desk with three right documents beats a desk buried in paper."

## 5. Anthropic, "Effective context engineering for AI agents" (Sept 29, 2025)

Authors: Prithvi Rajasekaran, Ethan Dixon, Carly Ryan, Jeremy Hadfield (Anthropic Applied AI). [Read it](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

- **Definition:** context engineering is the step after prompt engineering. Prompt engineering = writing good instructions. Context engineering = curating *everything* the model sees at each step (system prompt, tools, examples, message history, retrieved data), repeatedly, as the task runs.
- **Why:** *"Context, therefore, must be treated as a finite resource with diminishing marginal returns."* Transformers relate every token to every other (n² relationships for n tokens), so attention gets stretched: *"Every new token introduced depletes this budget by some amount."*
- **The goal:** *"find the smallest set of high-signal tokens that maximize the likelihood of your desired outcome."*
- **System prompts at the "right altitude":** *"The right altitude is the Goldilocks zone between two common failure modes"*: brittle hard-coded if-else logic on one side, vague high-level guidance on the other. Start minimal; add instructions for failures you observe.
- **Tools:** few, non-overlapping, token-efficient. If a human can't tell which tool to use, the agent can't either.
- **Examples:** a few diverse, canonical examples beat a long list of edge-case rules.
- **Just-in-time context:** keep lightweight references (file paths, links, queries) and load content when needed, instead of pre-loading everything. Claude Code does this: CLAUDE.md is loaded up front, files are found with search tools on demand.
- **Long-horizon techniques:**
  1. **Compaction:** summarise a nearly full context and restart from the summary.
  2. **Structured note-taking:** the agent writes notes (a to-do list, NOTES.md) outside the window and reads them back.
  3. **Sub-agent architectures:** specialised sub-agents work in clean windows and return short summaries to a lead agent.

## 6. Tools that fight context rot (what each one is, in plain language)

### Compaction / auto-compact
- **What:** when a conversation gets long, older turns are replaced by a summary so work can continue.
- **Claude API:** *"Compaction replaces the older turns of a conversation with a summary that Claude writes on the server … It keeps a long conversation or agent task inside the context window, and it keeps the active context small, because response quality degrades as a conversation grows."* Two modes (on demand, or at a token threshold), both in beta; the on-demand mode uses the `compact-2026-09-04` beta header. [Compaction overview](https://platform.claude.com/docs/en/build-with-claude/compaction)
- **Claude Code:** auto-compacts automatically. Models with a native 1M window *"compact before the window fills, at about 967K tokens by default."* You can set the threshold with `/autocompact 500k`, the `autoCompactWindow` setting, or `CLAUDE_CODE_AUTO_COMPACT_WINDOW`. [Model configuration](https://code.claude.com/docs/en/model-config)
- **Manual commands in Claude Code:** `/compact Focus on code samples and API usage` (tell it what to keep), and `/clear` to start fresh between unrelated tasks. *"Stale context wastes tokens on every subsequent message."* Also: *"`/compact` reads the conversation it summarizes, so compacting a large context is itself a large request. When you want a fresh start instead of continuity, `/clear` costs nothing."* [Manage costs effectively](https://code.claude.com/docs/en/costs)
- **What survives:** *"Project-root CLAUDE.md survives compaction: after `/compact`, Claude re-reads it from disk."* Instructions given only in chat can be lost; put durable rules in CLAUDE.md. [Memory docs](https://code.claude.com/docs/en/memory)
- **Claude apps:** on paid plans with code execution on, Claude summarises earlier messages automatically as a chat nears the limit. [Help Center](https://support.claude.com/en/articles/8606394)
- **Trade-off for the audience:** a summary loses detail. Compaction is a rescue, not a strategy. Better: shorter, focused sessions with a hand-off note.

### Context editing (API)
- Automatically clears old tool results and old thinking blocks instead of summarising. [Context editing](https://platform.claude.com/docs/en/build-with-claude/context-editing)

### Sub-agents
- **What:** a helper agent with its **own, separate context window**. It does a noisy side task (search, reading logs, running tests) and returns only a summary.
- Claude Code docs: *"Use one when a side task would flood your main conversation with search results, logs, or file contents you won't reference again: the subagent does that work in its own context and returns only the summary."* Defined as Markdown files in `.claude/agents/` (project) or `~/.claude/agents/` (personal). Built-ins: **Explore** (read-only search), **Plan** (research in plan mode), **general-purpose**. [Create custom subagents](https://code.claude.com/docs/en/sub-agents)
- **Cost:** each sub-agent uses its own tokens. Agent teams *"use approximately 7x more tokens than standard sessions when teammates run in plan mode."* [Costs](https://code.claude.com/docs/en/costs)
- **The counter-view:** Cognition argues sub-agents lose shared context and make conflicting decisions; share full traces or keep one thread. [Don't Build Multi-Agents](https://cognition.com/blog/dont-build-multi-agents)

### Memory files: CLAUDE.md and AGENTS.md
- **What:** a plain Markdown file the agent reads at the start of every session: build commands, conventions, "always do X" rules. The fix for "I keep re-explaining the same thing."
- **Claude Code locations** (load order, broad → specific): managed policy (org-wide) → `~/.claude/CLAUDE.md` (you, all projects) → `./CLAUDE.md` or `./.claude/CLAUDE.md` (team, in git) → `./CLAUDE.local.md` (you, this project, git-ignored). `/init` generates a starter file; `@path/to/file` imports other files. [How Claude remembers your project](https://code.claude.com/docs/en/memory)
- **Keep it short:** *"target under 200 lines per CLAUDE.md file. Longer files consume more context and reduce adherence."* Move multi-step procedures into skills, which load only when needed. [Memory docs](https://code.claude.com/docs/en/memory), [Costs](https://code.claude.com/docs/en/costs)
- **It's guidance, not enforcement:** *"Claude treats them as context, not enforced configuration. To block an action regardless of what Claude decides, use a PreToolUse hook instead."*
- **AGENTS.md** is the tool-neutral version, read by Codex, Cursor and others. [agents.md](https://agents.md), [Codex: Custom instructions with AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md). Claude Code (v2.1.277+) reads `AGENTS.md` when there is no `CLAUDE.md`; if both exist it reads only `CLAUDE.md`, so the usual pattern is a `CLAUDE.md` that contains `@AGENTS.md`. [Memory docs, AGENTS.md section](https://code.claude.com/docs/en/memory)
- **Auto memory (Claude Code):** Claude writes its own notes to `~/.claude/projects/<project>/memory/` with a `MEMORY.md` index; the first 200 lines or 25KB load each session; on by default in local sessions. [Memory docs](https://code.claude.com/docs/en/memory)
- **Memory tool (API):** the same idea for your own agents: Claude reads/writes files under `/memories`, which your app stores. Pairs with compaction: *"compaction keeps the active context small … and memory preserves the information that must survive summarization."* [Memory tool](https://platform.claude.com/docs/en/agents-and-tools/tool-use/memory-tool)

### Skills (progressive disclosure)
- A skill costs ~100 tokens (name + description) until it's needed; the full instructions (<5K tokens recommended) load only when triggered; bundled files load only when read. [Agent Skills overview](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview), [spec](https://agentskills.io/specification). This is context engineering packaged as a file format.

### Projects & memory in the chat apps
- **Claude Projects:** *"self-contained workspaces with their own chat histories and knowledge bases."* Available to all users including free (free: up to 5 projects). Each project has its own instructions. On paid plans, when project knowledge approaches the context limit Claude switches to RAG mode, which can *"expand capacity by up to 10x."* [What are projects?](https://support.claude.com/en/articles/9517075-what-are-projects)
- **Claude memory and chat search:** chat search across past conversations is on paid plans. Memory *"saves memory as a set of individual topics as you chat"*; on by default for Free, Pro and Max; off by default per member on Team/Enterprise until owners allow it. Each project keeps its own memory. Manage at **Settings > Memory**. Incognito chats are not searched later. [Chat search and memory](https://support.claude.com/en/articles/11817273)
- **ChatGPT Projects:** chats, files and instructions together; *"Project instructions apply only within that project and override your global custom instructions."* Projects can use their chats and files as context. [Projects in ChatGPT](https://help.openai.com/en/articles/10169521-projects-in-chatgpt)
- **ChatGPT memory:** sources can include past chats, saved memories, custom instructions, Library files and connected apps (by plan/region). Controls at **Settings > Personalization > Memory** (Reference saved memories, Reference chat history). Turning off chat-history reference schedules derived info for deletion within 30 days. [Memory in ChatGPT](https://help.openai.com/en/articles/8590148-memory-faq)
- **Gemini Gems, becoming skills:** a Gem is custom instructions + "Knowledge" files (**Explore Gems > New Gem**). From November 2026 Google converts personal-account Gems to skills (Workspace from March 2027); new work goes into **Customize > Skills**, invoked with `/` (checked 2026-10-21). [Tips for creating custom Gems](https://support.google.com/gemini/answer/15235603), [About the transition from Gems to skills](https://support.google.com/gemini/answer/18560919?hl=en)

**On memory features:** memory is convenient but it is context you didn't choose. For focused work (a pitch, a spec), use a project or an incognito/temporary chat so old, irrelevant "memories" don't leak in.

## 7. Practical rules for the audience (one slide)

1. **New task, new chat.** Don't drag yesterday's thread into today's problem.
2. **Brief, don't dump.** Give the 3 documents that matter, not the whole drive.
3. **Most important instructions first, the question last.**
4. **Write durable rules down once** (project instructions, CLAUDE.md / AGENTS.md, a skill) instead of repeating them.
5. **Offload noisy work** to sub-agents or separate chats and keep only the summary.
6. **Ask for a hand-off note** before a long session ends; start the next session from it.
7. **Watch for rot:** repeated mistakes, forgotten constraints, "it was fine an hour ago". Clear and restart with a summary.

## 8. Productivity research numbers (for the "why it matters / be careful" slide)

- **BCG "jagged frontier" (Dell'Acqua, McFowland, Mollick et al., 2023):** 758 BCG consultants. Inside the frontier, AI users completed 12.2% more tasks, 25.1% faster, with 40% higher quality. On a task outside the frontier, accuracy fell from 84% (no AI) to 60–70% with AI. [HBS working paper](https://www.hbs.edu/faculty/Pages/item.aspx?num=64700), [Mollick summary](https://www.oneusefulthing.org/p/centaurs-and-cyborgs-on-the-jagged)
- **P&G "Cybernetic Teammate" (Dell'Acqua et al., 2025):** RCT with 776 P&G professionals; *"Individuals working with AI performed just as well as teams without AI."* [HBS](https://www.hbs.edu/faculty/Pages/item.aspx?num=67197), [Mollick summary](https://www.oneusefulthing.org/p/the-cybernetic-teammate)
- **METR RCT (July 10, 2025):** 16 experienced open-source developers, 246 real issues, early-2025 tools (mostly Cursor + Claude 3.5/3.7 Sonnet). With AI they took **19% longer**, while expecting a 24% speed-up beforehand and still believing in a 20% speed-up afterwards. [METR](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/)
- **METR follow-up (Feb 24, 2026):** METR says the 2025 result is out of date; new data points to a speed-up with late-2025 tools, but selection bias (developers refusing to work without AI) made the experiment unreliable, so they changed the design. [METR update](https://metr.org/blog/2026-02-24-uplift-update/)
- **METR task horizon (March 2025):** the length of tasks agents can finish with 50% reliability *"has been doubling approximately every 7 months for the last 6 years"* (METR notes later estimates supersede the exact figure). [METR](https://metr.org/blog/2025-03-19-measuring-ai-ability-to-complete-long-tasks/)

---

### Caveats

- The model lineup in section 3 is what the vendors' docs show today (2026-10-20). Re-check on the day.
- ChatGPT's per-plan context window could not be verified from an OpenAI page (blocked); don't quote a number without checking chatgpt.com/pricing.
- Anthropic's docs disagree slightly on some app details (see install-skills.md); where they disagree, the newer claude.com/docs pages were preferred.
