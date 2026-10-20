# Open-source projects for building with AI

The open-source projects worth knowing when you build with AI: coding agents, agent frameworks, MCP, local models, app builders, RAG, evals, browser agents and UI kits. Curated for builders, whether you write code or not. Links to articles, courses and tools that are not open source are in [resources.md](resources.md); how I start a new app from a template is in [guides/scaffolding.md](guides/scaffolding.md).

 Checked on 2026-10-20 against the GitHub API (licence file, latest push, archived flag), and licence text read where GitHub could not classify it.

**How to read the licence column**
- **OSI**: an OSI-approved open-source licence (MIT, Apache-2.0, AGPL-3.0, PostgreSQL). You can use, change and ship it, including commercially. AGPL also requires you to publish your changes if you offer the software as a network service.
- **Open core**: the main code is OSI-licensed, but some directories (`ee/`, `enterprise/`, `pro/`) are under a commercial licence.
- **NOT OSI**: the code is source-available, fair-code or carries custom restrictions. Read the licence before you build a product on it.

"Last push" is the latest push to GitHub. Stars are rounded and were counted on 2026-10-20.

---

## 1. Coding agents and CLIs

| Project | Repo | Licence | Last push | Stars | When to use it |
|---|---|---|---|---|---|
| Codex CLI (OpenAI) | https://github.com/openai/codex | Apache-2.0 (OSI) | 2026-10-20 | 130k | Terminal coding agent for people on OpenAI models or a ChatGPT plan. |
| Gemini CLI (Google) | https://github.com/google-gemini/gemini-cli | Apache-2.0 (OSI) | 2026-10-20 | 107k | Terminal agent with a generous free tier and a large context window. |
| OpenCode | https://github.com/anomalyco/opencode (formerly `sst/opencode`) | MIT (OSI) | 2026-10-20 | 219k | Provider-agnostic terminal agent (TUI plus client/server). Use it if you want any model, or a local one. |
| Qwen Code | https://github.com/QwenLM/qwen-code | Apache-2.0 (OSI) | 2026-10-20 | 29k | Terminal agent tuned for the open-weight Qwen coder models. |
| Aider | https://github.com/Aider-AI/aider | Apache-2.0 (OSI) | 2026-05-22 | 50k | Git-aware pair programming in the terminal: every edit becomes a commit. **Slowing down**: last commit five months ago. |
| Cline | https://github.com/cline/cline | Apache-2.0 (OSI) | 2026-10-20 | 71k | VS Code agent with a plan/act flow that asks before each step. Bring your own API key. |
| Kilo Code | https://github.com/Kilo-Org/kilocode | MIT (OSI) | 2026-10-20 | 28k | VS Code/JetBrains agent with modes such as architect, code and debug. The most active of the Cline/Roo family. |
| Continue | https://github.com/continuedev/continue | Apache-2.0 (OSI) | 2026-10-20 | 36k | IDE assistant plus CI checks you configure in your repo. Good for teams that want shared rules. |
| goose | https://github.com/aaif-goose/goose (formerly `block/goose`) | Apache-2.0 (OSI) | 2026-10-20 | 55k | General local agent (desktop app plus CLI) driven by MCP extensions. Not only for code. |
| OpenHands | https://github.com/OpenHands/OpenHands (formerly `All-Hands-AI/OpenHands`) | MIT (OSI) | 2026-10-20 | 91k | Autonomous agent in a sandbox that takes an issue and returns a PR. Self-hostable. |
| Crush (Charm) | https://github.com/charmbracelet/crush | **FSL-1.1-MIT: NOT OSI** (source-available; becomes MIT after 2 years) | 2026-10-20 | 29k | Polished terminal agent. You may use it, but not to build a competing product. |
| ~~Roo Code~~ | https://github.com/RooCodeInc/Roo-Code | Apache-2.0 | **ARCHIVED 2026-05-15** | 24k | **Do not start new work on it.** The team moved to its hosted product. Use Kilo Code or Cline instead. |

## 2. Agent frameworks and SDKs

| Project | Repo | Licence | Last push | Stars | When to use it |
|---|---|---|---|---|---|
| Vercel AI SDK | https://github.com/vercel/ai | Apache-2.0 (OSI) | 2026-10-20 | 27k | Default TypeScript toolkit for chat, streaming, tools and agents across any provider in Next.js/Node. |
| Claude Agent SDK (Python) | https://github.com/anthropics/claude-agent-sdk-python | MIT (OSI) | 2026-10-19 | 8k | Build on the same agent loop as Claude Code (tools, files, subagents) from Python. |
| Claude Agent SDK (TypeScript) | https://github.com/anthropics/claude-agent-sdk-typescript | **NOT OSI**: governed by Anthropic Commercial Terms (README); no OSI licence file | 2026-10-19 | 2k | Same as the Python SDK, for Node. Note the terms: this repo is not open source. |
| OpenAI Agents SDK (Python) | https://github.com/openai/openai-agents-python | MIT (OSI) | 2026-10-20 | 30k | Lightweight multi-agent handoffs, guardrails and tracing. Works with other providers too. |
| OpenAI Agents SDK (JS/TS) | https://github.com/openai/openai-agents-js | MIT (OSI) | 2026-10-19 | 4k | The TypeScript version, including voice/realtime agents. |
| LangGraph | https://github.com/langchain-ai/langgraph | MIT (OSI) | 2026-10-20 | 44k | Stateful, graph-shaped agents with checkpoints and human-in-the-loop. Use it when you need explicit control flow. |
| Mastra | https://github.com/mastra-ai/mastra | Apache-2.0, **open core** (`ee/` dirs commercial) | 2026-10-20 | 29k | TypeScript agent framework with workflows, memory, evals and a local playground. |
| Pydantic AI | https://github.com/pydantic/pydantic-ai | MIT (OSI) | 2026-10-20 | 21k | Type-safe Python agents with validated structured output. Feels like FastAPI. |
| CrewAI | https://github.com/crewAIInc/crewAI | MIT (OSI) | 2026-10-20 | 60k | Role-based teams of agents ("researcher", "writer"). Fast for multi-agent prototypes. |
| Google ADK (Python) | https://github.com/google/adk-python | Apache-2.0 (OSI) | 2026-10-20 | 22k | Google's agent kit: multi-agent setups, evals, and deployment to Vertex/Cloud Run. |
| smolagents | https://github.com/huggingface/smolagents | Apache-2.0 (OSI) | 2026-10-06 | 30k | Minimal "agents that write Python code as actions" library. Good for learning how agents work. |
| Microsoft Agent Framework | https://github.com/microsoft/agent-framework | MIT (OSI) | 2026-10-20 | 14k | Successor to Semantic Kernel and AutoGen, for .NET and Python. Good fit for Azure shops. |
| LlamaIndex | https://github.com/run-llama/llama_index | MIT (OSI) | 2026-10-20 | 53k | Agents built around your documents: ingestion, indexing, querying. |

## 3. MCP (Model Context Protocol)

| Project | Repo | Licence | Last push | Stars | When to use it |
|---|---|---|---|---|---|
| Reference servers | https://github.com/modelcontextprotocol/servers | Apache-2.0 (OSI); older parts MIT (relicensing in progress) | 2026-10-19 | 91k | Official example servers (filesystem, git, fetch, memory…). The place to learn the pattern. |
| TypeScript SDK | https://github.com/modelcontextprotocol/typescript-sdk | Apache-2.0 / MIT (OSI, as above) | 2026-10-20 | 14k | Build MCP servers/clients in Node. |
| Python SDK | https://github.com/modelcontextprotocol/python-sdk | MIT (OSI) | 2026-10-17 | 25k | Build MCP servers/clients in Python. |
| MCP Inspector | https://github.com/modelcontextprotocol/inspector | Apache-2.0 / MIT (OSI, as above) | 2026-10-20 | 11k | Browser UI to connect to any MCP server and call its tools by hand. Use it for debugging. |
| MCP Registry | https://github.com/modelcontextprotocol/registry | Apache-2.0 / MIT (OSI, as above) | 2026-10-14 | 7k | Official community registry for publishing and discovering servers. |
| FastMCP | https://github.com/PrefectHQ/fastmcp (formerly `jlowin/fastmcp`) | Apache-2.0 (OSI) | 2026-10-20 | 28k | The quickest way to write a Python MCP server: decorate a function and it becomes a tool. |
| Playwright MCP | https://github.com/microsoft/playwright-mcp | Apache-2.0 (OSI) | 2026-10-19 | 38k | Lets an agent drive a real browser through accessibility snapshots instead of screenshots. |
| Chrome DevTools MCP | https://github.com/ChromeDevTools/chrome-devtools-mcp | Apache-2.0 (OSI) | 2026-10-20 | 54k | Lets an agent inspect live Chrome (console, network, performance traces). Use it to debug web apps. |
| GitHub MCP Server | https://github.com/github/github-mcp-server | MIT (OSI) | 2026-10-19 | 34k | Lets agents read and write issues, PRs, code and Actions on GitHub. |
| Context7 | https://github.com/upstash/context7 | MIT (OSI) for the server; the docs index is a hosted Upstash service | 2026-10-20 | 63k | Feeds current library docs into the agent so it stops guessing outdated APIs. |

## 4. Run models locally

| Project | Repo | Licence | Last push | Stars | When to use it |
|---|---|---|---|---|---|
| Ollama | https://github.com/ollama/ollama | MIT (OSI) | 2026-10-20 | 184k | One command to download and run open models, with an OpenAI-compatible local API. The easiest start. |
| llama.cpp | https://github.com/ggml-org/llama.cpp | MIT (OSI) | 2026-10-20 | 132k | The engine under most local tools (GGUF). Use it directly for maximum control on a CPU or Mac. |
| vLLM | https://github.com/vllm-project/vllm | Apache-2.0 (OSI) | 2026-10-20 | 94k | High-throughput serving on GPUs. Use it to host an open model for many users. |
| MLX | https://github.com/ml-explore/mlx | MIT (OSI) | 2026-10-20 | 29k | Apple's array framework for Apple Silicon. |
| mlx-lm | https://github.com/ml-explore/mlx-lm | MIT (OSI) | 2026-10-20 | 7k | Run and fine-tune LLMs on a Mac with MLX. Often the fastest option on M-series chips. |
| Jan | https://github.com/janhq/jan | Apache-2.0 (OSI) | 2026-10-20 | 45k | Offline desktop chat app (a ChatGPT-like UI) for local models. Friendly for non-engineers. |
| Open WebUI | https://github.com/open-webui/open-webui | **"Open WebUI License": NOT OSI** (BSD-3 plus a branding clause; you may not remove the branding above 50 users without permission) | 2026-10-20 | 156k | Self-hosted ChatGPT-style UI in front of Ollama or any OpenAI-compatible API. |
| LM Studio | https://lmstudio.ai | **App is proprietary (closed source, free to use)** | n/a | n/a | Polished desktop GUI for local models. Not open source. |
| LM Studio CLI `lms` / `lmstudio-js` | https://github.com/lmstudio-ai/lms · https://github.com/lmstudio-ai/lmstudio-js | MIT (OSI) | 2026-10-14 / 2026-10-16 | 5k / 2k | Script the LM Studio app. Only these pieces are open source. |

## 5. App builders and chat UIs

| Project | Repo | Licence | Last push | Stars | When to use it |
|---|---|---|---|---|---|
| Vercel Chatbot (ex "ai-chatbot") | https://github.com/vercel/chatbot | Apache-2.0 (OSI) | 2026-07-08 | 21k | Next.js plus AI SDK chat template with auth, history and artifacts. A starting point for your own chat app. |
| LibreChat | https://github.com/LibreChat-AI/LibreChat (formerly `danny-avila/LibreChat`) | MIT (OSI) | 2026-10-20 | 46k | Self-hosted multi-provider ChatGPT clone with agents, MCP and SSO. For a team-wide internal chat. |
| AnythingLLM | https://github.com/Mintplex-Labs/anything-llm | MIT (OSI) | 2026-10-20 | 67k | Desktop or Docker app to chat with your documents. No code; works with local models. |
| Langflow | https://github.com/langflow-ai/langflow | MIT (OSI) | 2026-10-20 | 156k | Visual drag-and-drop builder for agents and RAG flows that you can export as an API. |
| Dify | https://github.com/langgenius/dify | **Modified Apache-2.0: NOT OSI** (no multi-tenant SaaS, keep the logo, without a commercial licence) | 2026-10-20 | 159k | Visual platform for LLM apps and agents (workflows, RAG, ops). Fine for internal use. |
| n8n | https://github.com/n8n-io/n8n | **Sustainable Use License: fair-code, NOT OSI** (`.ee.` files commercial) | 2026-10-20 | 208k | Workflow automation with AI nodes, the "Zapier you host yourself". Free for internal business use. |
| bolt.diy | https://github.com/stackblitz-labs/bolt.diy | MIT (OSI) | 2026-10-14 | 20k | Prompt-to-full-stack-web-app in the browser, with any LLM. |
| Open Lovable | https://github.com/firecrawl/open-lovable | MIT (OSI) | 2026-10-09 | 29k | Clones or rebuilds a website as a React app from a URL or prompt. |
| Dyad | https://github.com/dyad-sh/dyad | Apache-2.0, **open core** (`src/pro/` commercial) | 2026-10-20 | 22k | Local desktop alternative to Lovable/v0/Bolt. Your code stays on your machine. |
| LobeHub (ex LobeChat) | https://github.com/lobehub/lobehub | **LobeHub Community License: NOT OSI** (derivative works need a commercial licence) | 2026-10-20 | 83k | Polished multi-agent chat UI. Use it as-is; do not fork it into a product. |
| ~~Flowise~~ | https://github.com/FlowiseAI/Flowise | Apache-2.0 + commercial `enterprise/` | **ARCHIVED 2026-08-13** | 56k | **Do not start new work on it** (README: "Flowise has been archived"). Use Langflow instead. |

## 6. RAG, vector stores and data ingestion

| Project | Repo | Licence | Last push | Stars | When to use it |
|---|---|---|---|---|---|
| pgvector | https://github.com/pgvector/pgvector | PostgreSQL License (OSI) | 2026-10-18 | 23k | Vector search inside the Postgres you already run. The sensible default. |
| Chroma | https://github.com/chroma-core/chroma | Apache-2.0 (OSI) | 2026-10-20 | 30k | Embedded vector DB that runs in a few lines of Python/JS. Good for prototypes and notebooks. |
| Qdrant | https://github.com/qdrant/qdrant | Apache-2.0 (OSI) | 2026-10-20 | 35k | Dedicated vector DB (Rust) with strong filtering, for production scale. |
| LanceDB | https://github.com/lancedb/lancedb | Apache-2.0 (OSI) | 2026-10-20 | 12k | Serverless, file-based vector store, a good fit for multimodal data and object storage. |
| RAGFlow | https://github.com/infiniflow/ragflow | Apache-2.0 (OSI) | 2026-10-20 | 93k | Complete RAG engine with deep document parsing and a UI. |
| Docling (IBM / LF AI) | https://github.com/docling-project/docling | MIT (OSI) | 2026-10-20 | 69k | Converts PDF/DOCX/PPTX into clean Markdown or JSON while keeping tables and layout. |
| Marker | https://github.com/datalab-to/marker | Code Apache-2.0 (OSI); **model weights modified OpenRAIL-M, NOT OSI** (free under $5M revenue/funding) | 2026-10-19 | 41k | Fast, accurate PDF to Markdown, including OCR. Check the weights licence before commercial use. |
| Unstructured | https://github.com/Unstructured-IO/unstructured | Apache-2.0 (OSI) | 2026-10-20 | 16k | Partitions many file types into elements for ingestion pipelines. |
| MarkItDown (Microsoft) | https://github.com/microsoft/markitdown | MIT (OSI) | 2026-10-04 | 191k | Turns Office files, PDFs and HTML into Markdown in one line, made for LLM input. Includes an MCP server. |
| Firecrawl | https://github.com/firecrawl/firecrawl | **AGPL-3.0** (OSI, copyleft; SDKs MIT) | 2026-10-20 | 193k | Website to clean Markdown or structured data, including crawling. AGPL obliges you to publish changes if you offer it as a hosted service. |
| Crawl4AI | https://github.com/unclecode/crawl4ai | Apache-2.0 (OSI; attribution requested) | 2026-10-20 | 86k | Self-hosted, LLM-friendly crawler and scraper in Python. |
| Mem0 | https://github.com/mem0ai/mem0 | Apache-2.0 (OSI) | 2026-10-20 | 68k | Long-term memory layer for agents (user facts across sessions). |

## 7. Evals and observability

| Project | Repo | Licence | Last push | Stars | When to use it |
|---|---|---|---|---|---|
| promptfoo | https://github.com/promptfoo/promptfoo | MIT (OSI); now part of OpenAI, still MIT | 2026-10-20 | 26k | Declarative prompt/model tests and red-teaming in CI. The easiest first eval. |
| Langfuse | https://github.com/langfuse/langfuse | MIT, **open core** (`ee/` dirs commercial) | 2026-10-20 | 36k | Self-hostable tracing, prompt management and evals for LLM apps. |
| Opik (Comet) | https://github.com/comet-ml/opik | Apache-2.0 (OSI) | 2026-10-20 | 23k | Tracing, evaluation and dashboards. A fully Apache alternative to Langfuse/Phoenix. |
| Arize Phoenix | https://github.com/Arize-ai/phoenix | **Elastic License 2.0: NOT OSI** (no offering it as a managed service) | 2026-10-20 | 12k | OpenTelemetry-based tracing plus evals in a local UI. Fine for internal use. |
| Inspect AI (UK AISI) | https://github.com/UKGovernmentBEIS/inspect_ai | MIT (OSI) | 2026-10-20 | 3k | Rigorous eval framework (agents, tools, sandboxes) used for frontier-model safety evals. |
| DeepEval | https://github.com/confident-ai/deepeval | Apache-2.0 (OSI) | 2026-10-19 | 19k | Pytest-style LLM unit tests with ready-made metrics (faithfulness, relevancy…). |
| autoevals (Braintrust) | https://github.com/braintrustdata/autoevals | MIT (OSI) | 2026-10-08 | 1k | Ready-made LLM-as-judge and heuristic scorers you can drop into any eval loop. |
| ~~OpenAI Evals~~ | https://github.com/openai/evals | MIT (OSI) | **2026-04-14 (stale, >6 months)** | 20k | Historical benchmark registry only; maintenance has stopped. Use promptfoo or Inspect instead. |

## 8. Browser and computer use

| Project | Repo | Licence | Last push | Stars | When to use it |
|---|---|---|---|---|---|
| Playwright | https://github.com/microsoft/playwright | Apache-2.0 (OSI) | 2026-10-20 | 98k | Deterministic browser automation and testing. Agents often generate Playwright scripts. |
| Browser Use | https://github.com/browser-use/browser-use | MIT (OSI) | 2026-10-20 | 119k | Python agent that completes tasks in a browser from a plain-language goal. |
| Stagehand | https://github.com/browserbase/stagehand | MIT (OSI) | 2026-10-20 | 26k | TypeScript mix of code and AI (`act`, `extract`, `observe`) for reliable web automation. |
| Skyvern | https://github.com/Skyvern-AI/skyvern | **AGPL-3.0** (OSI, copyleft) | 2026-10-20 | 23k | Vision-based form-filling and workflow automation across sites it has not seen. |
| Steel Browser | https://github.com/steel-dev/steel-browser | Apache-2.0 (OSI) | 2026-10-20 | 8k | Self-hosted browser sandbox/API for agents: sessions, proxies, CAPTCHA handling. |
| Cua | https://github.com/trycua/cua | MIT (OSI) | 2026-10-20 | 30k | Full computer use (desktop, not only the browser) in macOS/Linux/Windows sandboxes. |
| UI-TARS Desktop (ByteDance) | https://github.com/bytedance/UI-TARS-desktop | Apache-2.0 (OSI) | 2026-10-09 | 39k | Desktop GUI agent driven by a vision-language model. |

## 9. UI kits for AI apps

| Project | Repo | Licence | Last push | Stars | When to use it |
|---|---|---|---|---|---|
| shadcn/ui | https://github.com/shadcn-ui/ui | MIT (OSI) | 2026-10-19 | 126k | Copy-paste React components you own. The base most AI templates build on. |
| Radix Primitives | https://github.com/radix-ui/primitives | MIT (OSI) | 2026-10-14 | 19k | Unstyled, accessible React building blocks (dialogs, menus…) under shadcn. |
| Base UI | https://github.com/mui/base-ui | MIT (OSI) | 2026-10-20 | 11k | Unstyled accessible components from the Radix, Floating UI and MUI authors. Newer than Radix. |
| AI Elements (Vercel) | https://github.com/vercel/ai-elements | Apache-2.0 (OSI) | 2026-10-14 | 2k | shadcn-style chat parts (message, tool call, reasoning, sources) for the AI SDK. |
| Streamdown (Vercel) | https://github.com/vercel/streamdown | Apache-2.0 (OSI) | 2026-10-20 | 6k | Markdown renderer that stays correct while an AI response streams in. |
| assistant-ui | https://github.com/assistant-ui/assistant-ui | MIT (OSI) | 2026-10-20 | 13k | Composable React chat UI primitives. Works with the AI SDK, LangGraph and others. |
| CopilotKit | https://github.com/CopilotKit/CopilotKit | MIT (OSI) | 2026-10-20 | 38k | In-app copilots and generative UI that let an agent read and act on your app's state (AG-UI protocol). |

---

### Licence watch-list (non-OSI, copyleft or open core)
- **NOT OSI**: Crush (FSL-1.1-MIT), Claude Agent SDK TypeScript (Anthropic Commercial Terms), Open WebUI (branding clause), LM Studio app (proprietary), Dify (modified Apache), n8n (Sustainable Use / fair-code), LobeHub (Community License), Arize Phoenix (ELv2), Marker model weights (OpenRAIL-M variant).
- **Copyleft (OSI, AGPL-3.0)**: Firecrawl, Skyvern.
- **Open core (OSI core plus commercial directories)**: Mastra, Langfuse, Dyad; also Flowise (archived) and n8n.

### Archived or stale (excluded from recommendations)
- Roo Code: archived 2026-05-15.
- Flowise: archived 2026-08-13.
- OpenAI Evals: last commit 2026-04-14.
- Aider is kept but flagged: last commit 2026-05-22.

### Renamed or moved (old URLs redirect)
- `sst/opencode` → `anomalyco/opencode`
- `block/goose` → `aaif-goose/goose`
- `All-Hands-AI/OpenHands` → `OpenHands/OpenHands`
- `jlowin/fastmcp` → `PrefectHQ/fastmcp`
- `vercel/ai-chatbot` → `vercel/chatbot`
- `danny-avila/LibreChat` → `LibreChat-AI/LibreChat`
- `lobehub/lobe-chat` → `lobehub/lobehub`
