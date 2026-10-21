# Never start from a blank page: how I scaffold a new product

Slide 20 of the workshop, written out. Every command below was checked against the official docs on 2026-10-20. Templates get renamed and CLIs change flags, so if something fails, open the linked page first.

## The idea

A new product has three layers:

1. **A template that already runs.** Sign-in, database, file upload, an AI chat, a deploy pipeline. Someone else built it, thousands of people use it, and it works on day one. You own the code from the first commit.
2. **Your rules on top.** `AGENTS.md`, a design-rules file, your skills, your checks. This is what makes the agent work *your* way.
3. **Your one job.** The thing only you know: your customers, your domain, your data. This is where your time goes.

Most first-time builders do it the other way round: weeks on plumbing (auth, database, deploys) and a tired weekend on the actual idea.

**Why this matters more with agents:** an agent imitates the code it can see. In a clean, popular template the patterns are already there, and the model has seen them thousands of times. That's the best rules file you can get for free. A messy hand-rolled start teaches the agent to write more mess.

## Our own start

Our product's first commit (24 November 2025) was Vercel's open-source AI chatbot template, version 3.1.0: Next.js, the AI SDK, Postgres through Drizzle, file upload, a streaming chat with history. We merged our own sign-in into it in the same commit, so the first evening already had a working chat with login. Search over the law started the next day; the first week went into that, the part only we could build.

Eleven months later it's a Turborepo monorepo: web, mobile (Expo), desktop (Tauri), Word and Outlook add-ins, background workers (Trigger.dev). We swapped the auth library, moved the models behind our own routing and wrote our own design system. The template's bones are still visible in the code, and that's fine: they were good bones.

We do the same for smaller things. My blog started from `create-next-app` (which now writes an `AGENTS.md` for you), with the layout adapted from an MIT-licensed personal site, credited in an `ATTRIBUTION.md`. Open-source libraries get the same treatment: the very first commit sets up the licence, the checks and the agent's rules, before any feature.

## Step 1. Pick the closest template

Pick the template closest to the *shape* of your product, not to its topic.

| You are building | Start from | Command |
|---|---|---|
| A chat app (assistant, AI over your data) | [Vercel Chatbot](https://github.com/vercel/chatbot) (formerly "AI Chatbot"), Apache-2.0 | Deploy button on [its template page](https://vercel.com/templates/next.js/chatbot), or clone and follow the local setup below |
| A SaaS with marketing site, payments, emails, docs | [next-forge](https://www.next-forge.com), MIT | `npx next-forge@latest init` |
| A backend agent (runs on its own, has tools, schedules, channels) | [eve](https://eve.dev/docs), Vercel's agent framework, Apache-2.0 | `npx eve@latest init my-agent` ([eve templates](https://vercel.com/templates/eve)) |
| A bot in Slack, Teams, Discord, Telegram, WhatsApp… | [Chat SDK](https://chat-sdk.dev), MIT | `npm create chat-sdk@latest my-bot` |
| Chat over your own documents (RAG) | [RAG with AI SDK](https://vercel.com/templates/next.js/ai-sdk-rag) | from the template page |
| An MCP server | [MCP with Next.js](https://vercel.com/templates/next.js/model-context-protocol-mcp-with-next-js), or [FastMCP](https://github.com/PrefectHQ/fastmcp) in Python | from the template page |
| A plain website or app | [create-next-app](https://nextjs.org/docs/app/api-reference/cli/create-next-app) | `npx create-next-app@latest my-app --yes` |
| Several apps sharing code | [Turborepo](https://turborepo.dev/docs/getting-started/installation) | `npx create-turbo@latest --example with-nextjs` |
| A mobile app | [Expo](https://docs.expo.dev/get-started/create-a-project/) | `npx create-expo-app@latest` (see the page for the current SDK template) |
| A desktop app | [Tauri 2](https://v2.tauri.app/start/create-project/) | `npm create tauri-app@latest` |
| A docs site | [Fumadocs](https://www.fumadocs.dev/docs) | `npm create fumadocs-app` |
| Emails | [React Email](https://react.email/docs/getting-started/automatic-setup) | `npx create-email@latest` |

Browse more: the [Vercel templates gallery](https://vercel.com/templates) ([AI](https://vercel.com/templates/ai), [SaaS](https://vercel.com/templates/saas), [starters](https://vercel.com/templates/starter), [monorepos](https://vercel.com/templates/monorepos)). `create-next-app --example <name or GitHub URL>` starts from any of the [Next.js examples](https://github.com/vercel/next.js/tree/canary/examples) or any public repo.

**Before you pick, check:** the licence (MIT/Apache = do what you like, keep the notice), the last commit (abandoned templates rot fast), and whether it uses services you're willing to pay for later.

## Step 2. Deploy before you change anything

Get a live URL on day one. Every later change is then "does it still deploy?", not "will it ever deploy?".

The fastest path is the template's **Deploy** button: it forks the repo to your GitHub, creates the Vercel project and provisions the database and storage the template needs.

Or from the terminal (the Chatbot's own README):

```bash
npm i -g vercel        # Vercel CLI
vercel link            # connect this folder to a Vercel project
vercel env pull        # download the env vars into .env.local
pnpm install
pnpm db:migrate        # create the tables
pnpm dev               # http://localhost:3000
```

Need a database, Redis, auth or payments? Add them from the [Vercel Marketplace](https://vercel.com/marketplace) without leaving the terminal. One command provisions the resource, connects it to the project and pulls its env vars:

```bash
vercel integration add neon       # Postgres
vercel integration add upstash    # Redis
vercel integration add clerk      # auth (or use Better Auth, below)
vercel integration add stripe     # payments
```

Then `vercel` for a preview deploy, `vercel --prod` for production. `vercel env run -- pnpm dev` runs a command with the env vars injected without writing a file. ([CLI docs](https://vercel.com/docs/cli))

## Step 3. Make it yours before the first feature

An hour here saves weeks later.

1. **Rules file.** `AGENTS.md` at the root: what the product is, how to run and test it, what never to do, where things live. New Next.js apps already get one: `create-next-app` writes it, and `next dev` keeps a block in it pointing agents at the docs bundled with your exact Next.js version ([details](https://nextjs.org/docs/app/guides/ai-agents)). Add your own sections around that block. Claude Code reads `CLAUDE.md`, so make it a symlink: `ln -s AGENTS.md CLAUDE.md`. One file, every agent. Template: [`../templates/AGENTS.md`](../templates/AGENTS.md). Convention: [agents.md](https://agents.md).
2. **Design rules.** One short file with your colours, fonts, spacing, corner radius and what's banned. Template: [`../templates/design-rules.md`](../templates/design-rules.md). If the template uses [shadcn/ui](https://ui.shadcn.com/docs/cli), set your look once with `npx shadcn@latest init --preset <code>` from [ui.shadcn.com/create](https://ui.shadcn.com/create) instead of restyling components one by one.
3. **Skills.** A `.claude/skills/` (or shared `.agents/skills/`) folder with the workflows you'll repeat: verify, plan, root-cause. Starters: [`../skills/`](../skills/).
4. **Checks the agent must pass.** Lint, type check, tests, in one command, and in CI. The templates ship most of this; make sure it runs and is green *before* you add anything. "Done" means the checks pass.
5. **Swap what you won't keep, now.** Auth library, model provider, analytics. Swapping on day one is a ten-minute job for an agent; swapping after a year is a project. (We swapped auth later, and it was a project.)
6. **Pick your models.** Templates default to whatever was cheap or new when they were written. The Chatbot routes through [AI Gateway](https://vercel.com/ai-gateway), so changing the model is a one-line edit in `lib/ai/models.ts`.

## Step 4. Give the agent its hands

Connect the agent to the services the template uses, so it reads real logs and real docs instead of guessing:

| What | How |
|---|---|
| Vercel (deploys, logs, env vars) | `claude mcp add --transport http vercel https://mcp.vercel.com` ([docs](https://vercel.com/docs/agent-resources/vercel-mcp)), or `vercel setup` to install the Vercel plugin for Claude Code or Codex |
| shadcn/ui components and registries | `npx shadcn@latest mcp init --client claude` ([docs](https://ui.shadcn.com/docs/mcp)) |
| Current library docs | [Context7](https://context7.com) MCP |
| Stripe | `stripe agent setup` (Stripe plugin, skills and MCP for Claude Code, Codex or Cursor) ([CLI](https://docs.stripe.com/cli)) |
| Skills from vendors | `npx skills add vercel/next.js --skill next-dev-loop`, `npx skills add vercel/chat`, more at [skills.sh](https://www.skills.sh) |

More MCP servers I use: [my-stack.md](my-stack.md).

## Step 5. Now build your one job

Write the plan to a file, shred it, build, verify: [how-i-build.md](how-i-build.md). Keep the template's patterns when you add things. When you have to break one, write the reason in `AGENTS.md`, or the agent will "fix" it back.

## The rest of the toolbox

| Job | Tool | Start with |
|---|---|---|
| Auth (you own the users table) | [Better Auth](https://better-auth.com/docs/concepts/cli) | `npx auth@latest init` (the old `@better-auth/cli` package is deprecated) |
| Database migrations | [Drizzle Kit](https://orm.drizzle.team/docs/kit-overview) | `npx drizzle-kit generate`, then `migrate` |
| Background jobs | [Trigger.dev](https://trigger.dev/docs/quick-start) | `npx trigger.dev@latest init` |
| Payments testing | [Stripe CLI](https://docs.stripe.com/cli) | `stripe listen --forward-to localhost:3000/api/webhooks/stripe` |
| Mobile builds | [EAS](https://docs.expo.dev/build/setup/) | `npm i -g eas-cli`, `eas build --platform all` |
| A first screen from a prompt | [v0](https://v0.app/docs) | connect it to your GitHub repo: it works on its own branch and opens pull requests ([docs](https://v0.app/docs/github)) |
| Components from a registry | [shadcn](https://ui.shadcn.com/docs/cli) | `npx shadcn@latest add card`, or `add @namespace/item` from any [registry](https://ui.shadcn.com/docs/registry/registry-index) |

## Traps we hit or saw

- **Templates move.** `vercel/ai-chatbot` is now [`vercel/chatbot`](https://github.com/vercel/chatbot), and `chat-sdk.dev` is now the multi-platform *bot* framework, not the chat template. Old blog posts point to the old names.
- **READMEs drift from code.** On 2026-10-20 the Chatbot README listed a model provider the code no longer had, and its docs site named a different database variable (`DATABASE_URL`) than `.env.example` (`POSTGRES_URL`). Trust the code and `.env.example`, and tell the agent to.
- **The build runs migrations.** In the Chatbot (and in ours), `build` runs the database migrations first. Check which database your env points at before you build locally against production values.
- **Never "push" a schema to a shared database.** `drizzle-kit push` skips migration files. Fine on your laptop's database; on a shared one, the schema and the migration history drift apart, and fixing that costs weeks. Generate a migration, review it, apply it ([trick 56](tricks.md#shipping-and-ops)).
- **A fresh worktree has no `.env`.** Ignored files stay behind when you open a new git worktree, so a build that fails there may just be missing a secret ([trick 35](tricks.md#agents-and-parallel-work)).
- **Startup credits only count if you call the cloud directly.** If you have AWS, Google or Azure credits, route the heavy model traffic to them with your own account, and keep a gateway as the fallback ([my-stack.md](my-stack.md#two-tricks-from-running-this)).
- **Credit what you copy.** Keep the template's `LICENSE` notice. If you adapt someone's design, say so in an `ATTRIBUTION.md`.

Once it is live: agents stay off the production database, schema and migration ship in one commit, deploy and check before you promote, read production errors before you say "ready" ([tricks 55-58](tricks.md#shipping-and-ops)).

## Prompt: start from a template (Claude Code)

The workshop's background build starts from an empty folder because it's a throwaway prototype. For something you'll keep, start like this instead:

```
Goal: [one sentence: what it does and for whom].
Start from the Vercel Chatbot template (github.com/vercel/chatbot) in this folder. Before changing anything:
1. Read its README, package.json and .env.example, and tell me what it ships and which services it needs.
2. Get it running locally with the template's own steps. Stop and ask me for anything that needs an account or a secret.
3. Write AGENTS.md (with CLAUDE.md as a symlink): what this product is, how to run, test and deploy it, what never to do. Keep any block Next.js already wrote in it.
4. Run lint, type check and tests; all must pass before any feature work.
Then plan the first feature for [the one job] in a file, and wait for my OK before building it.
```
