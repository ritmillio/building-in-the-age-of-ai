# Third-party Agent Skills: a vetted catalogue

Checked on **2026-10-20** with the GitHub API (repo metadata, file tree, the actual LICENSE file, the SKILL.md frontmatter). Star counts are a rough popularity signal at that date.

**How to read the "claude.ai?" column**

- **Yes**: instructions-only (or Python scripts that run in Claude's code sandbox). Zip the skill folder and upload it (see `install-skills.md`).
- **Yes, after a small edit**: works in chat, but the SKILL.md uses Claude Code-only frontmatter keys. Claude Code's docs say that *"Outside Claude Code, such as in claude.ai uploads or the Skills API, only `name`, `description`, `license`, `compatibility`, `metadata`, and `allowed-tools` are accepted. Other keys cause a hard error."* ([source](https://code.claude.com/docs/en/skills)). Delete keys such as `disable-model-invocation`, `argument-hint`, `user-invocable`, `version` before zipping.
- **Claude Code / coding agent only**: needs a local codebase, a terminal, a CLI tool, or a browser on your machine.
- Also: the **Claude Help Center** says descriptions are limited to 200 characters ([source](https://support.claude.com/en/articles/12512198-how-to-create-custom-skills)), while the newer **claude.com docs** and the Agent Skills spec say 1,024 ([claude.com](https://claude.com/docs/skills/how-to), [spec](https://agentskills.io/specification)). Many popular skills have 300–1,000-character descriptions. If an upload is rejected, shorten the description first.
- **Plugins route (newer):** in claude.ai and the desktop app, **Customize > Plugins > Add > Add marketplace** accepts a GitHub `owner/repo` that contains `.claude-plugin/marketplace.json`; the plugin's skills then load in chat ([claude.com docs](https://claude.com/docs/plugins/overview)). The "Plugin marketplace?" column marks repos where this works. Not tested end-to-end for each repo.

**Safety first:** skills are code plus instructions that run with your access. Anthropic: *"Use Skills only from trusted sources … a malicious Skill can direct Claude to invoke tools or execute code in ways that don't match the Skill's stated purpose."* Read SKILL.md and every script before installing. ([source](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview))

---

## 1. Skills I use from others (origins confirmed)

| Skill | Original source (exact path) | Author | License (checked file) | What it does | claude.ai? |
|---|---|---|---|---|---|
| `grill-me` | [mattpocock/skills › skills/productivity/grill-me](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me) | Matt Pocock | MIT (repo `LICENSE`) | Interviews you relentlessly about a plan until every branch of the decision tree is resolved | **Yes, after a small edit** (remove `disable-model-invocation`). Great for idea validation in plain chat |
| `handoff` | [mattpocock/skills › skills/productivity/handoff](https://github.com/mattpocock/skills/tree/main/skills/productivity/handoff) | Matt Pocock | MIT | Compacts the current conversation into a hand-off document for a fresh agent/session | **Yes, after a small edit** (remove `argument-hint`, `disable-model-invocation`); designed around writing a temp file, so in chat it will produce the doc as output |
| `writing-fragments` | [mattpocock/skills › skills/in-progress/writing-fragments](https://github.com/mattpocock/skills/tree/main/skills/in-progress/writing-fragments) | Matt Pocock | MIT | Grills you for raw "fragments" (claims, vignettes, sharp sentences) and appends them to one document | **Yes, after a small edit**. Note it lives in the repo's `in-progress/` folder (Matt's label for unfinished skills) |
| `writing-shape` | [mattpocock/skills › skills/in-progress/writing-shape](https://github.com/mattpocock/skills/tree/main/skills/in-progress/writing-shape) | Matt Pocock | MIT | Shapes a pile of notes into an article, paragraph by paragraph, arguing format at each step | **Yes, after a small edit**; also `in-progress/` |
| `improve-codebase-architecture` | [mattpocock/skills › skills/engineering/improve-codebase-architecture](https://github.com/mattpocock/skills/tree/main/skills/engineering/improve-codebase-architecture) | Matt Pocock | MIT | Finds "deepening" refactors guided by the project glossary and ADRs; outputs a visual report | **Claude Code / coding agent only** (needs a repo) |
| `diagnose` | **Renamed.** It was `skills/engineering/diagnose` (a June 2026 install on this machine recorded that path); today it is [mattpocock/skills › skills/engineering/diagnosing-bugs](https://github.com/mattpocock/skills/tree/main/skills/engineering/diagnosing-bugs) | Matt Pocock | MIT | Disciplined loop for hard bugs and perf regressions: reproduce → minimise → hypothesise → instrument → fix → regression-test | **Claude Code / coding agent only** (needs running code; ships a shell script) |
| `find-skills` | [vercel-labs/skills › skills/find-skills](https://github.com/vercel-labs/skills/tree/main/skills/find-skills) | Vercel Labs | MIT (repo `LICENSE`) | Helps the agent search for and install skills via the `npx skills` CLI | **Coding agent only** (runs `npx skills`) |
| `ui-ux-pro-max` | [nextlevelbuilder/ui-ux-pro-max-skill › .claude/skills/ui-ux-pro-max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill/tree/main/.claude/skills/ui-ux-pro-max) | Next Level Builder | MIT (repo `LICENSE`) | Searchable design database (styles, palettes, font pairings, UX rules, chart types) queried by Python scripts | **Probably yes** (Python + CSV run in the code sandbox). Not tested; designed for coding agents |
| `vercel-react-best-practices` | [vercel-labs/agent-skills › skills/react-best-practices](https://github.com/vercel-labs/agent-skills/tree/main/skills/react-best-practices) (frontmatter `name: vercel-react-best-practices`) | Vercel | MIT, **declared in SKILL.md frontmatter only**; the repo has no LICENSE file | Prioritised React/Next.js performance rules for writing and reviewing code | Uploadable (pure Markdown), but useful mainly in a coding agent |
| `vercel-composition-patterns` | [vercel-labs/agent-skills › skills/composition-patterns](https://github.com/vercel-labs/agent-skills/tree/main/skills/composition-patterns) (frontmatter `name: vercel-composition-patterns`) | Vercel | MIT, frontmatter only (no LICENSE file) | React composition patterns: compound components, avoiding boolean-prop sprawl, React 19 changes | Same as above |
| `landing-page-design` | [elayadesign/ai-design-skills › skills/landing-page-design](https://github.com/elayadesign/ai-design-skills/tree/main/skills/landing-page-design) (byte-identical to the copy found locally) | Elaya | MIT (repo `LICENSE`, © 2026 Elaya) | Landing-page system: intake questions, structure, conversion copy, SEO, strict visual rules | **Yes** (pure Markdown; description 655 chars). Related: a similar `landing-page` skill exists in [MengTo/Skills › agent-skills/web-design/landing-page](https://github.com/MengTo/Skills/tree/main/agent-skills/web-design/landing-page) (MIT) |
| `copywriting` | [coreyhaines31/marketingskills › skills/copywriting](https://github.com/coreyhaines31/marketingskills/tree/main/skills/copywriting) | Corey Haines | MIT (repo `LICENSE`) | Conversion copywriting for homepages, landing, pricing and feature pages | **Yes** (description 989 chars, at the spec limit) |
| `pricing-strategy` | **Renamed to `pricing`** in v2.0 (commit 30f9b9a, 2026-05-14: "pricing-strategy → pricing"). Now [coreyhaines31/marketingskills › skills/pricing](https://github.com/coreyhaines31/marketingskills/tree/main/skills/pricing) | Corey Haines | MIT | Pricing research, tiers, packaging, value metric, Van Westendorp | **Yes** |
| `audit-website` | [squirrelscan/skills › skills/audit-website](https://github.com/squirrelscan/skills/tree/main/skills/audit-website) | squirrelscan | MIT (repo `LICENSE`, © 2025 squirrelscan) | Runs the `squirrel` CLI to audit a site for SEO, performance, security, broken links (230+ rules) | **Claude Code / coding agent only** (SKILL.md declares *"Requires squirrel CLI installed and accessible in PATH"*) |
| `impeccable` | [pbakaus/impeccable › plugin/skills/impeccable](https://github.com/pbakaus/impeccable/tree/main/plugin/skills/impeccable) (same skill mirrored in `.claude/`, `.cursor/`, `.agents/` etc.) | Paul Bakaus | Apache-2.0 (repo `LICENSE`) | Design-director skill with commands (shape, audit, critique, polish, bolder, quieter, typeset…) and 47 reference files | **Mostly coding agents** (JS scripts drive a live browser). A chat upload would need the extra frontmatter keys removed; untested |

Install one-liners from each README (quoted from the README text). On 2026-10-21 `npx skills@latest add <repo> --list` resolved for `mattpocock/skills`, `coreyhaines31/marketingskills`, `squirrelscan/skills`, `vercel-labs/agent-skills` and `vercel-labs/skills`, and every skill this page names from them was in the list (`grill-me`, `handoff`, `diagnosing-bugs`, `copywriting`, `pricing`, `customer-research`, `audit-website`, `find-skills`...). `--skill` takes several names separated by spaces:
- mattpocock: `claude plugin install mattpocock-skills@claude-plugins-official` (it is listed in Anthropic's official marketplace, pinned to a commit) or `/plugin marketplace add mattpocock/skills`; Codex: `codex plugin marketplace add mattpocock/skills`.
- marketingskills: `npx skills add coreyhaines31/marketingskills` (add `--skill copywriting pricing` to pick), or `/plugin marketplace add coreyhaines31/marketingskills` then `/plugin install marketing-skills`.
- ui-ux-pro-max: `/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill` then `/plugin install ui-ux-pro-max@ui-ux-pro-max-skill`; or `npm install -g ui-ux-pro-max-cli` + `uipro init --ai claude`.
- squirrelscan: `npx skills add squirrelscan/skills --skill audit-website`, or `/plugin marketplace add squirrelscan/skills` + `/plugin install squirrelscan@squirrelscan`.
- impeccable: `npx impeccable install`, or `/plugin marketplace add pbakaus/impeccable`; ZIP downloads per tool at [impeccable.style](https://impeccable.style).
- Vercel: `npx skills add vercel-labs/agent-skills`.
- elayadesign: README gives `git clone` + copy into `.claude/skills/`, and for claude.ai: *"Download the skill's `SKILL.md` and upload it to a Project, or attach it to a chat and say 'follow this.'"*

## 2. Official / first-party collections

| Collection | Author | License (checked) | What's in it | claude.ai? | Plugin marketplace? |
|---|---|---|---|---|---|
| [anthropics/skills](https://github.com/anthropics/skills) | Anthropic | **Mixed.** Per-skill `LICENSE.txt`: Apache-2.0 for `skill-creator`, `frontend-design`, `mcp-builder`, `webapp-testing`, `canvas-design`, `brand-guidelines`, `theme-factory`, `web-artifacts-builder`, `internal-comms`, `algorithmic-art`, `slack-gif-creator`, `claude-api`, `academy-guide`, `discernment-nudge`. **`docx`, `pdf`, `pptx`, `xlsx` are "© 2025 Anthropic, PBC. All rights reserved"**: the README calls them *"source-available, not open source"*. `doc-coauthoring` has no license file | Reference skills incl. the document skills that power Claude's file creation; `skill-creator` (writes and evals skills); `frontend-design` (anti-"AI slop" UI); a `template/` | Yes. README: *"These example skills are all already available to paid plans in Claude.ai"* (turn on in Customize > Skills) | Yes: `/plugin marketplace add anthropics/skills`, then `/plugin install document-skills@anthropic-agent-skills` or `example-skills@anthropic-agent-skills` |
| [anthropics/claude-plugins-official](https://github.com/anthropics/claude-plugins-official) | Anthropic | Apache-2.0 | The official Claude Code plugin directory (skill-creator, frontend-design, code-review, LSPs…) plus pinned third-party entries such as `mattpocock-skills`, `superpowers`, `vercel` | Via Customize > Plugins (Discover) | Added automatically in Claude Code |
| [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins) | Anthropic | Apache-2.0 | Plugins for non-engineers (sales, marketing, finance, legal, HR, product, operations, small business…), aimed at Cowork | Yes (plugins) | Yes |
| [openai/skills](https://github.com/openai/skills) | OpenAI | No root license; each curated skill has its own `LICENSE.txt` (Apache-2.0 on the one checked, `pdf`) | Curated Codex skills: Figma, Linear, Notion, Sentry, deploy (Vercel/Netlify/Render/Cloudflare), Playwright, security threat model, `gh-fix-ci`… | Many are instructions-only and portable; several need CLIs/MCP | Codex: `$skill-installer <name>` |
| [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) | Vercel | MIT in frontmatter of some skills; **no LICENSE file in repo** | React/Next performance, composition patterns, React Native, view transitions, web-design guidelines, deploy-to-vercel | Instructions-only ones upload fine | No marketplace.json; use `npx skills add vercel-labs/agent-skills` |
| [cloudflare/skills](https://github.com/cloudflare/skills) | Cloudflare | Apache-2.0 | Building on Workers, Durable Objects, Agents SDK | Coding agents | — |
| [supabase/agent-skills](https://github.com/supabase/agent-skills) | Supabase | MIT | Postgres/Supabase best practices | Mostly coding agents | — |
| [huggingface/skills](https://github.com/huggingface/skills) | Hugging Face | Apache-2.0 | Datasets, training, Hub workflows | Coding agents | — |
| [getsentry/skills](https://github.com/getsentry/skills) | Sentry | Apache-2.0 | Skills the Sentry team uses for development | Coding agents | — |
| [microsoft/skills](https://github.com/microsoft/skills) | Microsoft | MIT | Skills, MCP servers and AGENTS.md for Microsoft SDKs | Coding agents | — |
| [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills) | Google Labs | Apache-2.0 | Skills for the Stitch design MCP server | Needs Stitch MCP | — |
| [expo/skills](https://github.com/expo/skills) | Expo | MIT | Expo / EAS mobile app skills | Coding agents | — |

## 3. High-signal community collections

| Collection | Author | License (checked) | What it is | claude.ai? |
|---|---|---|---|---|
| [obra/superpowers](https://github.com/obra/superpowers) | Jesse Vincent (obra) | MIT | A full development methodology as composable skills: brainstorming, writing-plans, executing-plans, TDD, systematic-debugging, verification-before-completion, subagent-driven development. `/plugin install superpowers@claude-plugins-official` | Built for coding agents; `brainstorming` and `writing-plans` are readable in chat |
| [mattpocock/skills](https://github.com/mattpocock/skills) | Matt Pocock | MIT | ~40 small, composable skills (engineering, productivity, writing). Also `to-spec`, `to-tickets`, `tdd`, `triage`, `prototype`, `grilling`, `teach`, `writing-for-agents` | Productivity/writing ones: yes after removing Claude Code-only keys |
| [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) | Corey Haines | MIT | ~50 marketing skills: CRO, copywriting, SEO, pricing, launch, customer-research, cold-email, ads, onboarding… Reads a shared `product-marketing.md` context file | **Yes**, the best fit for non-coders in this list |
| [K-Dense-AI/scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills) (formerly `claude-scientific-skills`) | K-Dense AI | MIT | 170+ science/research skills (databases, bioinformatics, analysis) | Some; many need packages |
| [trailofbits/skills](https://github.com/trailofbits/skills) | Trail of Bits | **CC-BY-SA-4.0** (share-alike; note for commercial reuse) | Security research, vulnerability detection and audit workflows | Coding agents |
| [wshobson/agents](https://github.com/wshobson/agents) | Seth Hobson | MIT | Large multi-harness plugin marketplace (agents + skills) for Claude Code, Codex, Cursor and others | Coding agents |
| [MengTo/Skills](https://github.com/MengTo/Skills) | Meng To | MIT | Design-focused skills for designers and builders (landing page, design taste, anti-AI-slop audits) | Instructions-only ones: yes |
| [elayadesign/ai-design-skills](https://github.com/elayadesign/ai-design-skills) | Elaya | MIT | Design skills incl. `landing-page-design` | Yes |

## 4. Directories and "awesome" lists (for browsing, not installing blindly)

| Resource | License | Notes |
|---|---|---|
| [skills.sh](https://skills.sh) | (website) | Vercel's skills directory; each repo page shows the `npx skills add` command, e.g. [skills.sh/mattpocock/skills](https://skills.sh/mattpocock/skills), [skills.sh/anthropics/skills](https://skills.sh/anthropics/skills) |
| [vercel-labs/skills](https://github.com/vercel-labs/skills) | MIT | The `npx skills` CLI itself (supports Claude Code, Codex, Cursor, OpenCode and 75 more) |
| [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) | **No license file** (all rights reserved by default) | Curated list plus ~30 skill folders (e.g. `lead-research-assistant`, `meeting-insights-analyzer`, `domain-name-brainstormer`, `competitive-ads-extractor`); several are copies of Anthropic examples |
| [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills) | No license file | Link list only; last pushed April 2026 |
| [hesreallyhim/awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) | **CC BY-NC-ND 4.0** (non-commercial, no derivatives) | Big curated list of Claude Code skills, hooks, agents, status lines |
| [Claude Marketplace: plugins](https://claude.com/marketplace/plugins) | (website) | Anthropic-reviewed plugins, installable from claude.ai or Claude Code |

## 5. Suggested starter set for this workshop's audience

| Goal | Skill | Where it runs |
|---|---|---|
| Stress-test an idea or plan | `grill-me` (mattpocock) | claude.ai (after removing one key) or any agent |
| Customer research & positioning | `customer-research`, `product-marketing`, `copywriting`, `pricing` (marketingskills) | claude.ai |
| Landing page | `landing-page-design` (elayadesign) + `copywriting` | claude.ai or Claude Code |
| Better-looking UI | `frontend-design` (Anthropic, built into claude.ai) or `impeccable` / `ui-ux-pro-max` in a coding agent | — |
| Documents & decks | `docx`, `pptx`, `xlsx`, `pdf` (Anthropic, built into claude.ai) | claude.ai |
| Write your own skill | `skill-creator` (Anthropic) | claude.ai (Customize > Skills), Claude Code, ChatGPT/Codex include their own `skill-creator` |
| Hand work between sessions | `handoff` (mattpocock) | any agent |

---

### What could not be verified

- That every skill above actually *runs* in claude.ai. Compatibility is judged from file contents (frontmatter keys, scripts, CLI requirements) and from Anthropic's documented upload rules; uploads were not performed.
- The exact date `diagnose` became `diagnosing-bugs` in mattpocock/skills. Evidence: this machine's skill lock file (installed 2026-06-10) records `skills/engineering/diagnose/SKILL.md`; the current tree has only `diagnosing-bugs`.
- License of `remotion-dev/skills` (no LICENSE file found), so it was left out.
