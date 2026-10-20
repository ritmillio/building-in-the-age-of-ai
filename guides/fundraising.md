# Raising money in the age of AI, and the "thin wrapper" problem

The guide behind slides 25-27 of the workshop. A prototype takes an afternoon now, for everyone. What does an investor pay for now?

Compiled 2026-10-20. Every figure below was read on the cited page unless marked otherwise. Most market data is US-centric (Carta, PitchBook) or global (Crunchbase); CEE data is thinner and flagged as such.

---

## Part 1. Summary in plain language

### 1. What changed in fundraising

- **The money is real, but it is concentrated.** More venture money is flowing than at almost any time before, but into fewer companies and bigger rounds. Most of it goes to AI, and a large slice goes to a handful of model labs.
- **Two markets at one stage.** An AI startup and a non-AI startup at the same stage are now priced as if they were in different markets. The AI premium is real, and so is the pressure on everyone else.
- **Fewer rounds, fewer bets.** Valuations at the top are rising while the number of funded companies falls. Investors are making fewer, larger, more concentrated bets.
- **Smaller teams go further.** AI lets a few people build and sell what used to need a department. More companies are started by one founder. Some reach serious revenue with a few dozen people.
- **"Raise once" is a real option.** Some founders raise one small round, get profitable, and keep control ("seed-strapping"). Venture is a choice, not a default.
- **The bar moved.** Growth that used to win a Series A can now be "not enough", because investors have seen AI companies grow faster. Speed alone no longer impresses; durability does.
- **What investors now ask:**
  - Why can't OpenAI, Anthropic or Google ship this next quarter?
  - What do you own that a model does not: data, workflow, customers, trust?
  - What happens to your margin when usage grows and you pay per token?
  - What if your model vendor cuts you off, raises prices, or competes with you?
  - Does your product get better with every customer, or only when the model improves?

### 2. The wrapper / moat debate

- **The fear:** if your product is a prompt on top of someone else's model, the model owner can copy it, bundle it for free, or cut your access.
- **It has happened.** A writing-assistant leader was undercut when a general chatbot became "good enough". A homework-help company lost most of its business to AI search and chatbots. A coding tool lost direct access to a model when it was about to be bought by that model maker's rival. A big coding company lost access to another lab's models after its acquisition.
- **It also moves public markets.** When a model vendor released a few "plugins" (essentially folders of instructions) for legal, finance and sales work, listed legal-information and software companies lost billions in value in a day. When the same vendor released a design tool, a listed design company's stock dropped.
- **But "wrappers" also won.** The biggest AI application successes (AI coding editors, AI search, app builders, presentation tools) were all mocked as wrappers. They won by being the best finished product, using several models, building their own models where it matters, and owning the user relationship.
- **Even vendor products are not permanent.** One model lab launched an agent-builder that was billed as a "Zapier killer", then announced it would shut it down within a year. Platform risk cuts both ways: do not build your core on a vendor's feature-of-the-month either.
- **What counts as a moat now (VC consensus, 2025-2026):**
  - Proprietary or hard-to-get data, and data that your product generates by doing the work.
  - Owning the workflow end to end, ideally becoming the system of record (where the truth lives).
  - Distribution and brand: being the name customers already trust and use.
  - Trust and compliance in regulated or local domains (law, tax, health, finance), where accuracy is existential.
  - Speed: useful early, but a "bailey" to abandon later, not a permanent wall.
  - Selling the outcome, not the tool: "if you sell the tool, you're in a race against the model."
- **What does not count:** a better prompt, a nicer chat UI, or being first. Lock-in by switching cost is also weakening, because AI makes migration easier.

### 3. "Your product is a markdown file"

- Agent Skills, plugins and MCP connectors are plain text files: instructions, a few scripts, a list of tool connections. That is their strength (anyone can write, share and run them) and the founder's problem (anyone can copy them).
- The model vendors say it themselves: their plugins are "just markdown files", "no code, no infrastructure", "fork the repo".
- Skills became an open standard adopted by multiple AI tools, so a skill written for one assistant runs in others. Portability is good for users and bad for anyone whose whole product is the skill.
- **Implication for founders:** if a competent user can paste your instructions into a general assistant and get most of your output, you have a demo, not a company. Treat your prompts and skills like your website copy: necessary, visible, not defensible.
- **How to show defensibility instead:**
  - Show what improves with every customer: your data, your evaluations, your feedback loop.
  - Show where you sit in the customer's real workflow and records, not just in a chat window.
  - Show what is hard to get: licensed data, local legal/tax knowledge, certifications, integrations with local systems.
  - Show that model progress makes you better and cheaper, not obsolete (multi-model, own evals, own smaller models where it matters).
  - Show gross margin that holds up as usage grows.
  - Show distribution you already have, not distribution you hope for.

### 4. AI in fundraising itself (brief)

- Founders use AI to research investors, draft and stress-test decks, prepare Q&A, and build clean data rooms. Generic AI-written decks and cold emails are easy to spot and count against you.
- Investors increasingly run AI on your materials first: screening decks, extracting metrics, flagging contradictions. Assume the first reader of your data room is a machine; make it consistent and machine-readable.
- Fund tools now plug straight into AI assistants (cap tables, CRM, portfolio data), so expect faster, more data-driven diligence.
- An academic study with a German VC found that an AI screening agent picked startups with better survival odds than human analysts, much faster and cheaper; the best picks were those both humans and AI chose.

### 5. CEE / Hungary angle

- CEE raised roughly the same total VC in 2025 as the year before, but over half of it went to AI, a higher share than in Europe overall.
- Local funds dominate pre-seed and seed in CEE; Series A and later money mostly comes from abroad. Plan your later rounds as an international raise from day one.
- CEE produces more enterprise value per euro invested than the European average, on far less funding per unit of GDP: capital-efficient by necessity, which suits the "small team, raise less" era.
- Hungary: the state fund Hiventures launched a new early-stage fund focused on AI, deeptech, medtech and greentech in 2026, with small tickets alongside angels and private VCs. Regional funds such as Day One Capital raised new pre-seed/seed funds. Recent Hungarian AI-relevant rounds are mostly seed-sized (e.g. Kodesage, Allonic) plus SEON's growth round.
- The local angle is a moat argument: regulated, language- and jurisdiction-specific work (law, tax, accounting, public registries) is exactly where global models are weakest and trust matters most.

---

## Part 2. The numbers, with sources

Format: figure: source (date). "Verified" = read on the page. Flags in **bold**.

### Concentration and AI share
- Global VC 2025: about $425B to 24,000+ companies, up 30% from $328B in 2024; third-largest year on record: Crunchbase News, Gené Teare (2026-01-07).
- AI took about $211B in 2025, roughly 50% of global VC, up 85% from $114B in 2024: Crunchbase News (2026-01-07).
- Five companies (OpenAI, Scale AI, Anthropic, Project Prometheus, xAI) raised $84B, about 20% of all 2025 VC: Crunchbase News (2026-01-07).
- About 60% of 2025 capital went to 629 companies raising $100M+ rounds; 68 companies raising $500M+ took more than a third: Crunchbase News (2026-01-07).
- Q3 2026: $159B global VC; AI $102B = 64%; record 27 companies raised $1B+ rounds and took about a third of the quarter's capital; YTD Q1-Q3 2026 $679B, highest ever for the first three quarters: Crunchbase News, Gené Teare (2026-10-05).
- Q3 2026: 50% of early-stage funding came in $100M+ rounds; about 20% of seed money came in $100M+ "seed" rounds: Crunchbase News (2026-10-05).
- Europe Q3 2026: $25B, AI 75% ($18.8B), highest share on record: Crunchbase News (2026-10-08).
- Europe 2025: 31% of funding to AI/ML companies (Atomico State of European Tech 2025 via Euronews, 2025-11-19). **Atomico's own page did not show the headline total; Europe-wide total not verified.**
- US (Carta platform): AI took over 60% of capital in Q1 2026, highest share recorded; foundation-model companies 14.2% of all capital; in SaaS 83% of capital went to AI startups: Carta, State of Private Markets Q1 2026, Ashley Neville (2026-05-29).
- US (PitchBook-NVCA via SiliconANGLE): 64% of Q3 2025 US deal value went to AI (2025-10-03). **Q3 2026 PitchBook AI share (~83%) seen only in a LinkedIn post; not verified.**

### Valuation gap
- Series A median valuation: AI 38% higher than non-AI in 2025; at Series E+ the premium was 193%: Carta, State of Private Markets 2025 in review, Neville & Dowd (2026-02-18).
- Q1 2026 Series A medians: foundation-model AI startup about $300M vs non-AI about $55M: Carta Q1 2026 (2026-05-29).
- 2025 round count on Carta fell to 4,859, lowest in at least six years, down 41% from 2021, while capital rose 16.9% to $119.5B: Carta (2026-02-18).
- 95th-percentile seed valuation Q2 2026: $200.4M vs $72.2M in Q2 2025 (+177% in a year); median seed (software, last 6 months) $24.3M post on $4.1M raised; median Series A $80M on $14.4M: Peter Walker, Carta data posts archive (2026-07-08/10).
- Investor quote circulated (Harry Stebbings, later deleted): "Turned down a founder with $1.5M ARR this year and $5M ARR next year... that isn't good enough to raise a Series A." Discussed by Peter Walker, Carta archive (2026-06-26). **Original post deleted; quoted second-hand.**

### Smaller teams, faster revenue
- Solo-founded share of new US startups: 23.7% (2019) to 36.3% (H1 2025); solo founders were 30% of 2024 startups but got only 14.7% of priced-round cash: Carta Solo Founders Report 2025, Peter Walker & Hamza Shad (2025-12-09).
- Top 100 AI companies on Stripe reached $1M annualized revenue in a median 11.5 months, about 4 months faster than the fastest SaaS cohort: Stripe blog, Lauren Thomas (2025-06-30). **Cohort ranking method not defined on the page.**
- YC W25 batch grew about 10% per week in aggregate; for about a quarter of the batch, ~95% of code was AI-written; Garry Tan: "You don't have to raise as much. The capital goes much longer.": CNBC, Kate Rooney (2025-03-15). **Causality to AI disputed by critics.**
- Bessemer "Supernovas": ~$40M ARR year 1, ~$125M year 2, ~25% gross margin (often negative), ~$1.13M ARR per FTE; "Shooting Stars": ~$3M to ~$103M ARR by year 4, ~60% gross margin, ~$164K ARR/FTE: Bessemer State of AI 2025 (2025-08-13).
- Lovable (Sweden): $400M ARR in Feb 2026 with 146 full-time employees (~$2.77M ARR per employee): TechCrunch, Anna Heim (2026-03-11); $500M run-rate June 2026, $400M Series C at $13.3B: TechCrunch, Julie Bort (2026-08-12).
- Gamma: $100M ARR profitably with about 50 employees; $68M Series B at $2.1B; ~$90M raised in total: TechCrunch, Julie Bort (2025-11-10).
- Seed-strapping: "raising once, becoming profitable immediately, and keeping 70%+ of their companies": Henry Shi, Substack (2025-03-25). **Paywalled; preview only.**

### Margins and inference cost
- Supernova AI apps ~25% gross margin vs ~60% for Shooting Stars (vs typical SaaS 75%+): Bessemer (2025-08-13).
- a16z: "it's shortsighted to be optimizing for 80% gross margin"; optimise total gross profit growth while you build the system of work: Joe Schmidt, a16z (2025-06-04).
- ICONIQ survey (300 execs, April 2025): companies use on average 2.8 models in customer-facing products; 37% plan to change pricing within a year: ICONIQ 2025 State of AI. **ICONIQ gross-margin trend figures (41% to 52%) seen only in secondary summaries; not verified.**

### Vendor-risk events (dated)
- Jasper: internal valuation cut ~20% (to ~$1.2B from $1.5B), 2023 ARR forecast cut 30%+, attributed to ChatGPT as a "formidable low-cost competitor": Maginative citing The Information (2023-09-29). **Pre-2025; unofficial figures.**
- Chegg: 22% workforce cut (248 people), Q1 2025 subscribers -31%, revenue -30%; pressure from AI tools and Google AI Overviews: Maginative (2025-05-12).
- Windsurf: Anthropic cut first-party access to Claude 3.x models with little notice amid OpenAI acquisition reports: TechCrunch, Maxwell Zeff (2025-06-03).
- Anthropic "Agent Skills" incl. Excel, PowerPoint, Word, PDF skills: Anthropic/Claude blog (2025-10-16); published as open standard (agentskills.io) 2025-12-18; OpenAI Codex adopted within days: Simon Willison (2025-12-19/20).
- OpenAI AgentKit/Agent Builder launched 2025-10-06; update 2026-06-03: Agent Builder and Evals winding down, unavailable from 2026-11-30: OpenAI.
- Claude Cowork plugins (11 open-source, legal/finance/sales etc.) 2026-01-30: Claude blog. Repo README: "Every component is file-based - markdown and JSON, no code, no infrastructure, no build steps."
- Market reaction 2026-02-03: Thomson Reuters -14.2% (Nasdaq), RELX -14%, Wolters Kluwer -10.5%, LSEG -8.5%: Canadian Lawyer (2026-02-03). About $285B wiped off listed tech that day per Bloomberg as cited by Martin Alderson (2026-02-05). **$285B is second-hand (Bloomberg not opened).**
- Claude Design launched 2026-04-17 (exports to PPTX, PDF, Canva): Anthropic. Figma fell ~7% that day: **design-press/aggregator reports only; not verified at a primary market source.**
- Cursor: $2.3B Series D at $29.3B, $1B+ annualized revenue: Cursor blog / CNBC (2025-11-13); SpaceX $60B all-stock acquisition announced 2026-06-16, completed 2026-08-14: CNBC/Bloomberg/TechCrunch; OpenAI to end model access via Cursor from 2026-11-12 (OpenAI models ~5% of Cursor traffic per CEO): CNBC (2026-08-29).
- Perplexity CEO: annualized revenue tripled since start of 2026 "thanks to model advances that have been made by Anthropic"; last reported valuation $20B: CNBC (2026-06-03). A "wrapper" whose growth rides its supplier.
- Stripe founders (2025 annual letter): "Some people have called these startups 'LLM wrappers'; those people are missing the point": TechCrunch, Mary Ann Azevedo (2025-02-27).
- TechCrunch survey of 20 enterprise VCs: more than half named quality/rarity of proprietary data as the main AI moat (2025-01-10).

### AI in fundraising / VC
- AI screening agent (with Freigeist Capital, 61,814 startups 2018-2023): ~13.4 s vs ~2 h per analysis, ~$0.07 vs ~$70; AI-selected startups had significantly higher survival; Freigeist filters ~70% of off-thesis startups with it: Angry Optimist/Warp News summary (2025-12-08) of a ScienceDirect paper (S105752192500835X). **Paper itself not opened.**
- Carta now ships "Investors", "CRM" and "Cap Table" plugins for Claude (seen on carta.com navigation, 2026).

### CEE / Hungary
- CEE startups raised €2.3B VC in 2025; recovery from Q4 2025 (€756M) into Q1 2026 (€952M); AI took 52% of CEE VC in 2025 (23% in 2024; Europe 34%); deep tech 17% to 37%; ecosystem value €274B: Dealroom, "CEE startups 2025 in review" (2026-04-30). **Dealroom's CEE perimeter appears to include Austria (Austria listed among top countries).**
- CEE firms are 90% of the ten most active pre-seed/seed investors, 40% at Series A, 10% at Series B+; CEE produces 120% of the European average enterprise value per euro of VC on 40% of the average VC per unit of GDP: Dealroom (2026-04-30).
- Q2 2026 CEE: ~€495M across 143 rounds (Q1 2026 ~€821M); Poland led; Hungary not quantified (Kodesage, Volteum listed): Vestbee (2026-08-13).
- Hiventures new HUF 17B (~€42M) fund for AI/deeptech/medtech/greentech, tickets up to €300K, announced 2026-02-18: Xpatloop (2026-02-19). **Secondary source; Hiventures release not opened.**
- SEON (Budapest/Austin, fraud prevention): $80M Series C led by Sixth Street Growth, total $187M: SEON / Tech.eu (2025-09-16).
- **Not found: a verified 2025 total for Hungarian VC or a Hungary-specific AI share.** The Recursive's "Top funding rounds raised by Hungarian startups in 2025" (2026-01-26) is paywalled.

---

## Part 3. Reading list

- [Global Venture Funding In 2025 Surged As Startup Deals And Valuations Set All-Time Records](https://news.crunchbase.com/venture/funding-data-third-largest-year-2025/) — 2025 totals, AI ~50%, mega-round concentration (Gené Teare, Crunchbase News, 2026-01-07)
- [Q3 2026 Posted A Record Count Of Billion-Dollar Rounds As The Global AI Race Heats Up](https://news.crunchbase.com/venture/q3-2026-global-startup-funding-ai-billion-dollar-rounds-exits-data/) — freshest global data, AI 64%, 27 billion-dollar rounds (Gené Teare, Crunchbase News, 2026-10-05)
- [Europe Posted Its Strongest Quarter In Q3 In 4 Years](https://news.crunchbase.com/venture/q3-2026-europe-strong-quarter-ai-uk-germany-france/) — Europe AI share at 75% (Gené Teare, Crunchbase News, 2026-10-08)
- [State of Private Markets: 2025 in review](https://carta.com/data/state-of-private-markets-q4-2025/) — fewer rounds, AI valuation premium by stage (Ashley Neville, Kevin Dowd, Carta, 2026-02-18)
- [State of Private Markets: Q1 2026](https://carta.com/data/state-of-private-markets-q1-2026/) — AI >60% of capital; $300M vs $55M Series A gap (Ashley Neville, Carta, 2026-05-29)
- [Solo Founders Report 2025](https://carta.com/data/solo-founders-report/) — solo founders rising to 36%, AI as force multiplier (Peter Walker, Hamza Shad, Carta, 2025-12-09)
- [Inside the growth of the top AI companies on Stripe](https://stripe.com/blog/inside-the-growth-of-the-top-ai-companies-on-stripe) — AI companies reach $1M ARR faster than SaaS (Lauren Thomas, Stripe, 2025-06-30)
- [The State of AI 2025](https://www.bvp.com/atlas/the-state-of-ai-2025) — Supernovas vs Shooting Stars, margins, "context and memory may be the new moats" (Bessemer, 2025-08-13)
- [Context is King](https://a16z.com/context-is-king/) — "AI is an extraordinary engine for product differentiation. But it's not a moat." (David Haber, a16z, 2025-08-18)
- [Trading Margin for Moat](https://a16z.com/services-led-growth/) — why wrapper-like integrations break; services-led growth into the system of work (Joe Schmidt, a16z, 2025-06-04)
- [Fruits of the Walled Garden](https://a16z.com/fruits-of-the-walled-garden/) — proprietary, hard-to-access data as moat (legal, medical examples) (Marc Andrusko, Alex Rampell, a16z, 2025-10-09)
- [Good news: AI Will Eat Application Software](https://a16z.com/good-news-ai-will-eat-application-software/) — which moats persist; thin frontend wrappers vulnerable; switching costs weaken (Alex Immerman, Santiago Rodriguez, a16z, 2026-03-02)
- [How AI Companies Will Build Real Defensibility](https://www.nfx.com/post/ai-defensibility) — motte-and-bailey: speed/brand first, network effects and embedding later (Pete Flint, NFX, July 2025)
- [The AI Wrapper is Dead](https://www.nfx.com/post/ai-wrapper-dead-verticalization-startups) — vertical integration as the defence; "The wrapper was just scaffolding" (Pete Flint, NFX, July 2026)
- [Services: The New Software](https://sequoiacap.com/article/services-the-new-software/) — sell the outcome: "If you sell the tool, you're in a race against the model" (Julien Bek, Sequoia, byline 2026-03-05; page metadata conflicts)
- [Own Your Intelligence: A How-to Guide](https://sequoiacap.com/article/own-your-intelligence-a-how-to-guide/) — labs move up into product, apps move down into training loops (Sonya Huang, Sequoia, 2026-08-19)
- [Generative AI's Act o1](https://sequoiacap.com/article/generative-ais-act-o1/) — "wrappers" evolved into "cognitive architectures" (Sonya Huang, Pat Grady, Sequoia, 2024-10-09; **pre-2025, historical context**)
- [VCs say AI companies need proprietary data to stand out from the pack](https://techcrunch.com/2025/01/10/vcs-say-ai-companies-need-proprietary-data-to-stand-out-from-the-pack) — survey of 20 VCs on moats (Rebecca Szkutak, TechCrunch, 2025-01-10)
- [Stripe CEO says AI startups are growing faster than SaaS ever did, and calling them wrappers misses the point](https://techcrunch.com/2025/02/27/stripe-ceo-says-ai-startups-are-growing-faster-than-saas-ever-did-and-calling-them-wrappers-misses-the-point) — the pro-wrapper argument (Mary Ann Azevedo, TechCrunch, 2025-02-27)
- [Why Cursor's CEO believes OpenAI, Anthropic competition won't crush his startup](https://techcrunch.com/2025/12/09/why-cursors-ceo-believes-openai-anthropic-competition-wont-crush-his-startup/) — finished product vs "concept car", multi-model, own models (Julie Bort, TechCrunch, 2025-12-09)
- [OpenAI to end model access to Cursor after acquisition by SpaceX](https://www.cnbc.com/2026/08/29/openai-cursor-spacex-model-access.html) — model-vendor risk even for the winner; recalls the Windsurf cut-off (CNBC, 2026-08-29)
- [Windsurf says Anthropic is limiting its direct access to Claude AI models](https://techcrunch.com/2025/06/03/windsurf-says-anthropic-is-limiting-its-direct-access-to-claude-ai-models/) — supplier cut-off with little notice (Maxwell Zeff, TechCrunch, 2025-06-03)
- [Perplexity CEO tells CNBC one metric will determine who wins the AI race](https://www.cnbc.com/2026/06/03/perplexity-ceo-ai-valuations-computer-agentic.html) — orchestration as the moat; revenue tripled on Anthropic model gains (CNBC, 2026-06-03)
- [Introducing Agent Skills](https://claude.com/blog/skills) — skills as folders of instructions; Office document skills; open standard update (Anthropic, 2025-10-16, updated 2025-12-18)
- [Claude Skills are awesome, maybe a bigger deal than MCP](https://simonwillison.net/2025/Oct/16/claude-skills/) — "a skill is a Markdown file telling the model how to do something"; easy to share (Simon Willison, 2025-10-16)
- [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins) — the "just markdown files" plugins behind the Feb 2026 sell-off (Anthropic, 2026)
- [Wall Street lost $285 billion because of 13 markdown files](https://martinalderson.com/posts/wall-street-lost-285-billion-because-of-13-markdown-files/) — what is exposed (UI-process SaaS, services) vs safer (systems of record with good APIs) (Martin Alderson, 2026-02-05)
- [Anthropic legal tool jolts share price of global legal data leaders](https://www.canadianlawyermag.com/news/international/anthropic-legal-tool-jolts-share-price-of-global-legal-data-leaders/393665) — dated share-price moves (Canadian Lawyer, 2026-02-03)
- [Introducing AgentKit](https://openai.com/index/introducing-agentkit/) — the "Zapier killer" and its 2026 wind-down notice; platform features churn too (OpenAI, 2025-10-06, updated 2026-06-03)
- [Central and Eastern European startups: 2025 in review](https://dealroom.co/reports/central-and-eastern-european-startups-2025-in-review/) — CEE totals, AI 52%, foreign capital at Series A+ (Dealroom, 2026-04-30)
- [VC funding in CEE: Q2 2026](https://vestbee.com/insights/articles/vc-funding-in-cee-report-q2-2026) — latest quarterly CEE deal data by country (Konrad Koncerewicz, Lisa Palchynska, Vestbee, 2026-08-13)

---

## What could not be verified
- Atomico State of European Tech 2025 total funding figure (only the 31% AI share via Euronews).
- Hungary 2025 VC total and Hungary AI share (no open source found; The Recursive list is paywalled).
- Hiventures fund details (secondary source only).
- PitchBook-NVCA Q3 2026 AI share (~83%) and the Bloomberg $285B figure (second-hand).
- Figma -7% on Claude Design launch (aggregators only).
- ICONIQ gross-margin trend numbers, Affinity "AI in investment decisions 13% to 28%", DocSend 2025/2026 deck-review times (secondary or vendor sources only).
- Freigeist/AI-screening paper read via summary, not the paper itself.
