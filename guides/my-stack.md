# My stack: every tool and service I actually use

What a small team building an AI product runs on, day to day. No affiliate links, no sponsorships. This changes every few months; the date of this version is 2026-10-20. How I combine these is in [how-i-build.md](how-i-build.md); how a new project starts from a template is in [scaffolding.md](scaffolding.md).

## How a day looks

- **Agents do most of the typing.** [Claude Code](https://claude.com/product/claude-code) is the main one. [Codex](https://developers.openai.com/codex) and [Kimi Code](https://www.kimi.com/code) run on the same project with the same instructions: one `AGENTS.md` rules file (Claude Code's `CLAUDE.md` is a symlink to it) and one shared skills folder that every agent reads. One setup, three agents, no copies that drift apart.
- **Several sessions at once**, each in its own git worktree, each with its own task.
- **Long jobs run overnight** as a chain of fresh sessions (the `relay` skill), with a ledger committed to git and a draft pull request to review in the morning.
- **Every decision comes to me as clickable options** with a recommendation first. It's a line in the rules file.
- **My phone pings** when an agent finishes, fails or waits for permission: a [hook](https://code.claude.com/docs/en/hooks) calls a small script that posts to a [Telegram bot](https://core.telegram.org/bots). A custom [status line](https://code.claude.com/docs/en/statusline) shows branch and context use.
- **Every task leaves a record** in [Notion](https://www.notion.com): what was done, why, how it was verified, what is open. The agents write it themselves through the Notion connector.
- **Every UI change is checked live in a browser** before it counts as done. [Claude in Chrome](https://claude.com/chrome) lets the agent click through it itself.

## On my desk

| What | Tool |
|---|---|
| Main coding agent | [Claude Code](https://claude.com/product/claude-code) (terminal + desktop app) |
| Second opinions, parallel lanes | [Codex](https://developers.openai.com/codex), [Kimi Code](https://www.kimi.com/code), sometimes [Cursor](https://cursor.com) |
| Terminal | [Ghostty](https://ghostty.org), [Warp](https://www.warp.dev) |
| Launcher | [Raycast](https://www.raycast.com) |
| Dictation (talk instead of type) | [Wispr Flow](https://wisprflow.ai) |
| Browsers | [Arc](https://arc.net), Chrome with [Claude in Chrome](https://claude.com/chrome) |
| Tasks, docs, decisions | [Notion](https://www.notion.com) |
| Diagrams and slides | [Excalidraw](https://excalidraw.com) (this deck is drawn in it) |

## What the agents are plugged into (MCP servers and plugins)

[MCP](../resources.md#8-mcp-model-context-protocol) is how an agent reaches a tool directly instead of clicking through a screen. The ones I keep connected:

| Server / plugin | What I use it for |
|---|---|
| [GitHub MCP](https://github.com/github/github-mcp-server) | Issues, pull requests, code search across repos |
| [Context7](https://context7.com) | Current docs for any library, so the agent doesn't code against last year's API |
| [Mobbin MCP](https://mobbin.com/mcp) | Real app screens as design references, pulled straight into the session |
| [21st.dev Magic](https://21st.dev/magic) | UI components and inspiration from the 21st.dev community library |
| [PostHog MCP](https://posthog.com/docs/model-context-protocol) | "What did users actually do?" questions against product analytics |
| [Resend MCP](https://resend.com/docs/mcp-server) | Email templates and sending, from the agent |
| [ZenRows](https://www.zenrows.com) | Reading public web pages that block simple scrapers |
| [Circleback](https://circleback.ai) | Meeting notes the agent can search |
| Notion connector | Tasks, decisions and work logs |
| Plugins: Vercel, Cloudflare, Stripe | Deploys, logs, env vars; Workers and storage; billing, all from the session |
| [Impeccable](https://impeccable.style) plugin | Design vocabulary and review commands for the agent |
| TypeScript and Rust language servers | Precise "go to definition / find references" for the agent instead of text search |

Rule of thumb I follow: I don't sign up for a service the agent can't reach through MCP or an API.

## Where I find designs

Describe a design in adjectives and you get the generic AI look. Show real screens instead.

| Source | Use it for |
|---|---|
| [Mobbin](https://mobbin.com) | Real app screens and flows, searchable by pattern (onboarding, paywall, settings…). Also as an MCP server. |
| [21st.dev](https://21st.dev) | Community React/Tailwind components, from buttons to whole sections, copy-paste or via Magic MCP |
| [Refero](https://refero.design) | Searchable UI reference library |
| [shadcn/ui](https://ui.shadcn.com) and [Radix](https://www.radix-ui.com) | The component base most AI tools generate; learn it to steer them |
| [Magic UI](https://magicui.design), [Aceternity UI](https://ui.aceternity.com), [Origin UI](https://originui.com) | Animated and ready-made components on top of shadcn/Tailwind |
| [Tailwind Plus](https://tailwindcss.com/plus) | Professionally designed Tailwind blocks and templates (paid) |
| [Dribbble](https://dribbble.com), [Figma Community](https://www.figma.com/community) | Visual exploration (beautiful, not always buildable: check against real apps) |
| [Phosphor Icons](https://phosphoricons.com) | One consistent icon family in six weights |
| [Google Fonts](https://fonts.google.com), [Fontshare](https://www.fontshare.com) | Free, good fonts |
| [Excalidraw](https://excalidraw.com) | Hand-drawn diagrams and talk slides |

More design reading (guidelines, taste, systems) is in [resources.md](../resources.md#11-design-with-ai-references-systems-taste).

## What the product runs on

The stack behind our product: a web app, a mobile app, a desktop app, Word and Outlook add-ins, background workers, legal search across several countries.

| Layer | Service |
|---|---|
| Web app | [Next.js](https://nextjs.org) on [Vercel](https://vercel.com) |
| Monorepo | [Turborepo](https://turborepo.com) + [pnpm](https://pnpm.io) |
| Database | Postgres on [Neon](https://neon.com), with [pgvector](https://github.com/pgvector/pgvector) and [Drizzle ORM](https://orm.drizzle.team) |
| Vector search (big corpora) | [Turbopuffer](https://turbopuffer.com) |
| File storage | [Cloudflare R2](https://www.cloudflare.com/developer-platform/products/r2/) |
| Cache, rate limits | [Upstash Redis](https://upstash.com) |
| Auth | [Better Auth](https://www.better-auth.com) |
| Payments | [Stripe](https://stripe.com) |
| Email | [Resend](https://resend.com) + [React Email](https://react.email) |
| Product analytics | [PostHog](https://posthog.com) |
| Background jobs | [Trigger.dev](https://trigger.dev) |
| Long-running scrapers | [Railway](https://railway.com) |
| AI in the app | [Vercel AI SDK](https://ai-sdk.dev) + [AI Gateway](https://vercel.com/ai-gateway); some providers called directly (below) |
| Models | Claude via [AWS Bedrock](https://aws.amazon.com/bedrock/), Gemini via [Google Vertex AI](https://cloud.google.com/vertex-ai), [Azure AI Foundry](https://ai.azure.com), plus [DeepSeek](https://api-docs.deepseek.com), [GLM](https://docs.z.ai) and [Kimi](https://platform.moonshot.ai) for specific jobs |
| Embeddings | [Gemini embeddings](https://ai.google.dev/gemini-api/docs/embeddings) and [Voyage AI](https://www.voyageai.com) |
| Mobile | [Expo](https://expo.dev) + [EAS](https://expo.dev/eas) (build, submit, over-the-air updates) |
| Desktop | [Tauri](https://v2.tauri.app) |
| Docs site | [Fumadocs](https://www.fumadocs.dev) |
| Rich-text editing | [Tiptap](https://tiptap.dev) |
| Tests and checks | [Vitest](https://vitest.dev), [Playwright](https://playwright.dev), [Biome](https://biomejs.dev) via [Ultracite](https://www.ultracite.ai) |
| Headless browser work | [Puppeteer](https://pptr.dev) |

### Two tricks from running this

- **Use startup credits by calling the cloud directly.** [AWS Activate](https://aws.amazon.com/startups/credits), [Microsoft for Startups](https://www.microsoft.com/en-us/startups) and [Google for Startups](https://cloud.google.com/startup) give credits that only count when you call their AI services with your own account. Going through a gateway is simpler but bills someone else. We route the biggest model traffic directly, and keep the gateway as the fallback.
- **Several models, one chain.** Every AI job has a primary model and fallbacks from other vendors. When one provider is down or changes its terms, the job moves to the next one. That's also the honest answer to the investor question "what if your model vendor cuts you off?" ([fundraising.md](fundraising.md)).
