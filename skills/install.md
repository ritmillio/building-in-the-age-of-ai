# How to install and use a skill (every surface)

Checked against vendor docs on **2026-10-20**. UI labels move often; each section links the page it came from. Items marked **⚠ uncertain** are where sources disagree or I could not confirm.

**A skill, in one sentence:** a folder with a `SKILL.md` file (YAML frontmatter `name` + `description`, then instructions), plus optional `scripts/`, `references/`, `assets/`. The format is an open standard, so one folder works across Claude, Codex, Cursor, Gemini CLI and others. ([Agent Skills specification](https://agentskills.io/specification))

```text
my-skill/
├── SKILL.md        # required
├── references/     # optional, read when needed
├── assets/         # optional, templates/data
└── scripts/        # optional, code the agent runs
```

```markdown
---
name: my-skill            # lowercase, digits, hyphens; ≤64 chars; must match the folder name
description: What it does AND when to use it. Include the words people will say.   # ≤1,024 chars in the spec
---
# Instructions…
```

**Before installing anyone else's skill:** read `SKILL.md` and every script. Anthropic: *"Use Skills only from trusted sources … a malicious Skill can direct Claude to invoke tools or execute code in ways that don't match the Skill's stated purpose."* ([source](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview))

---

## A. Claude Code

Docs: [Extend Claude with skills](https://code.claude.com/docs/en/skills), [Install and manage plugins](https://code.claude.com/docs/en/plugins/install)

### A1. Copy the folder (simplest)

| Scope | Put the folder here | Applies to |
|---|---|---|
| Personal | `~/.claude/skills/<skill-name>/SKILL.md` | all your projects on this machine |
| Project (commit it to git) | `.claude/skills/<skill-name>/SKILL.md` in the repo | everyone working in that repo |
| Nested | `<subdir>/.claude/skills/<skill-name>/SKILL.md` | sessions in/under that folder |
| Enterprise | `.claude/skills/…` inside the managed-settings directory | everyone on managed machines |

```bash
# example: install grill-me for yourself
git clone https://github.com/mattpocock/skills.git /tmp/mp-skills
mkdir -p ~/.claude/skills
cp -r /tmp/mp-skills/skills/productivity/grill-me ~/.claude/skills/
```

- **Use it:** type `/grill-me`, or just describe the task and Claude loads the skill when your request matches its `description`.
- **No restart needed:** *"Adding, editing, or removing a skill under `~/.claude/skills/`, `.claude/skills/` … takes effect without a restart."* If you created a top-level skills directory that didn't exist at startup, run `/reload-skills`.
- **Precedence on name clashes:** enterprise > personal > project. Plugin skills are namespaced (`/plugin-name:skill-name`) so they never clash.
- **Note:** Claude Code's skills page documents `.claude/skills/`; it does not mention reading `.agents/skills/` (the folder Codex/Cursor/Gemini use). If you share one folder across tools, symlink it into `.claude/skills/` (**⚠ uncertain** whether newer versions read `.agents/skills` directly; not documented).

### A2. Install from a plugin marketplace (one command, auto-updates for official marketplaces)

```text
/plugin                                                   # browse the Discover tab
/plugin install skill-creator@claude-plugins-official     # Anthropic's official marketplace is added automatically
/plugin marketplace add anthropics/skills                 # add any GitHub repo that has .claude-plugin/marketplace.json
/plugin install document-skills@anthropic-agent-skills
/plugin install deploy-helper --marketplace your-org/plugins   # add + install in one step (v2.1.275+)
```

From your shell (no session): `claude plugin install <name>@<marketplace> [--scope user|project|local]`, `claude plugin marketplace add owner/repo`, `claude plugin list`, `claude plugin update <name>@<marketplace>`, `claude plugin uninstall …`.
On a fresh machine where no interactive session has run yet, first: `claude plugin marketplace add anthropics/claude-plugins-official`.
Scopes: **user** (`~/.claude/settings.json`), **project** (committed `.claude/settings.json`; each teammate still installs once), **local** (`.claude/settings.local.json`).
Auto-update is **on** for `claude-plugins-official` and marketplaces added from claude.ai, **off** for third-party marketplaces.
Source: [Install and manage plugins](https://code.claude.com/docs/en/plugins/install).

Repos verified to ship a `.claude-plugin/marketplace.json` (2026-10-20): `anthropics/skills`, `mattpocock/skills`, `obra/superpowers`, `coreyhaines31/marketingskills`, `pbakaus/impeccable`, `nextlevelbuilder/ui-ux-pro-max-skill`, `squirrelscan/skills`. `mattpocock-skills` and `superpowers` are also listed in Anthropic's official marketplace, so `claude plugin install mattpocock-skills@claude-plugins-official` works without adding anything.

### A3. `npx skills` (cross-agent installer by Vercel) — **exists, verified**

Ran on 2026-10-20: `npx skills@latest --help` and `npx skills add ritmillio/skills --list` both work as shown.

```bash
npx skills add vercel-labs/agent-skills                     # pick skills + agents interactively; project scope by default
npx skills add coreyhaines31/marketingskills --skill copywriting -a claude-code   # one skill; --skill '*' for all
npx skills add ritmillio/skills --list                      # see what a repo offers without installing
npx skills add mattpocock/skills -g                         # -g = global (all projects)
npx skills find landing page                                # search the skills.sh directory
npx skills list | check | update | remove
```

- Requires Node.js 22.20+. For Claude Code it installs to `.claude/skills/` (project) or `~/.claude/skills/` (global); for Codex, Cline, Zed and others to `.agents/skills/` / `~/.agents/skills/`. Supports 79+ agents.
- Sends anonymous telemetry; disable with `DISABLE_TELEMETRY=1` or `DO_NOT_TRACK=1`.
- Source: [vercel-labs/skills README](https://github.com/vercel-labs/skills), directory at [skills.sh](https://skills.sh).
- Matt Pocock's README warns: install **either** the plugin **or** the `skills.sh` copy per agent, *"because installing both gives you every skill twice."*

### A4. Skills you added in claude.ai can sync down

If you sign in to Claude Code with the same Claude account, claude.ai skills sync one-way into `~/.claude/skills/synced/` (Claude Code v2.1.273+; not with API-key or Bedrock/Vertex sign-in; turn off with `syncClaudeAiSkills: false`). Run `/skills` to see them. ([Help Center](https://support.claude.com/en/articles/12512180-use-skills-in-claude), [Claude Code skills](https://code.claude.com/docs/en/skills))

---

## B. claude.ai (web) and the Claude desktop app

Docs: [Skills overview](https://claude.com/docs/skills/overview), [Create custom skills](https://claude.com/docs/skills/how-to), [Use skills in Claude (Help Center)](https://support.claude.com/en/articles/12512180-use-skills-in-claude), [Plugins](https://claude.com/docs/plugins/overview)

### B1. Requirements
- **Code execution must be on:** **Settings > Capabilities > "Code execution and file creation"**. On Team/Enterprise an Owner enables it (Organization settings).
- **Plans:** ⚠ **sources disagree.** The claude.com docs say *"Skills are available on Pro, Max, Team, and Enterprise plans"*; the Help Center says *"Free, Pro, Max, Team, and Enterprise plans."* Assume paid plans for a workshop; Free may or may not work on the day.

### B2. Turn on built-in skills
1. Go to **Customize > Skills** (claude.ai/customize/skills).
2. The **Your skills** tab groups skills (Created by you / From your organization / Shared with you / From Anthropic & Partners); **Discover** lists more.
3. Click **Turn on**. Anthropic's document skills (Word, Excel, PowerPoint, PDF) and `skill-creator` are already there.

### B3. Upload your own (or a third-party) skill as a ZIP
1. Make sure the folder name equals the `name` in `SKILL.md`.
2. Zip **the folder itself**, from its parent directory:
   ```bash
   zip -r my-skill.zip my-skill/
   unzip -l my-skill.zip     # every entry must start with my-skill/
   ```
   *"a `SKILL.md` sitting at the root of the ZIP isn't recognized as a skill."*
3. In **Customize > Skills**, click **+** → **+ Create skill** → **Upload a skill**, and choose the ZIP. (Help Center wording; the claude.com docs describe the same Customize > Skills page.)
4. Turn it on, then test with prompts that should trigger it. If Claude ignores it, rewrite the `description`.

**Frontmatter gotcha:** Claude Code docs: *"Outside Claude Code, such as in claude.ai uploads or the Skills API, only `name`, `description`, `license`, `compatibility`, `metadata`, and `allowed-tools` are accepted. Other keys cause a hard error."* Delete keys like `disable-model-invocation`, `argument-hint`, `user-invocable`, `version` before zipping (common in Matt Pocock's and Impeccable's skills). ([source](https://code.claude.com/docs/en/skills))

**Description length:** ⚠ the Help Center says 200 characters max ([source](https://support.claude.com/en/articles/12512198-how-to-create-custom-skills)); the claude.com docs and the spec say 1,024 ([source](https://claude.com/docs/skills/how-to)). If an upload fails, shorten the description.

**Runtime:** skill scripts run in Claude's code sandbox; network access depends on your/admin settings. Skills that need a local CLI (e.g. `audit-website` needs `squirrel`) won't work in chat.

### B4. Install a whole collection as a plugin (no zipping)
**Customize > Plugins** → **Add** → **Add marketplace** → enter `owner/repo` (e.g. `mattpocock/skills`) or a GitHub URL → add the plugin. Its skills then appear under Customize > Skills and work in chat, Cowork and (synced) Claude Code. **Add > Upload plugin** accepts a `.zip`/`.plugin` containing `.claude-plugin/plugin.json`. Directory plugins appear on Pro, Max, Team and Enterprise. ([Plugins docs](https://claude.com/docs/plugins/overview)) ⚠ Not tested end-to-end with each third-party repo.

### B5. Team / Enterprise
Owners can provision skills for everyone, restrict who may create skills, and control sharing under **Organization settings > Plugins & skills**. Members can **Share** or **Publish to org** from a skill's page. ([Help Center](https://support.claude.com/en/articles/12512180-use-skills-in-claude), [claude.com docs](https://claude.com/docs/skills/how-to))

⚠ The older platform-docs page still says custom skills are uploaded through *"Settings > Features"* and are *"individual to each user"* with no admin management ([source](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)). The newer claude.com docs and Help Center describe Customize > Skills with sharing and org provisioning; follow those.

---

## C. Claude API (Skills API)

Docs: [Using Agent Skills with the API](https://platform.claude.com/docs/en/build-with-claude/skills-guide), [Quickstart](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/quickstart)

**Status: GA.** *"The Skills API is out of beta and needs no beta header."* Old code that sends `anthropic-beta: skills-2025-10-02` / uses `client.beta.skills` keeps working but returns the old response shapes.

1. **Upload** a custom skill (zip or files; `SKILL.md` at the root or in one top folder):
   ```python
   import anthropic
   from anthropic.lib import files_from_dir

   client = anthropic.Anthropic()
   skill = client.skills.create(files=files_from_dir("financial_skill"))
   print(skill.id, skill.latest_version_id)
   ```
   REST: `POST https://api.anthropic.com/v1/skills`. List Anthropic's: `client.skills.list(source="anthropic")` → `pptx`, `xlsx`, `docx`, `pdf`.
2. **Use** it in a Messages request: put skills in `container.skills` **and** enable the code execution tool:
   ```python
   response = client.messages.create(
       model="claude-opus-5-5",
       max_tokens=16000,
       container={"skills": [
           {"type": "anthropic", "skill_id": "pptx", "version": "latest"},
           {"type": "custom", "skill_id": skill.id, "version": "latest"},
       ]},
       messages=[{"role": "user", "content": "Create a 5-slide deck on renewable energy"}],
       tools=[{"type": "code_execution_20260521", "name": "code_execution"}],  # code_execution_20250825 also works
   )
   ```
3. **Download** generated files: find the `file_id` in the `bash_code_execution_tool_result` block and call `client.files.download(file_id)`.

Limits: up to **20 skills per request**; upload **< 30 MB** uncompressed; `name` ≤ 64 chars (lowercase/digits/hyphens, no "anthropic"/"claude"); `description` ≤ 1,024 chars. The API container has **no network access and no runtime package installs**. Custom skills are **workspace-wide** (any key in the workspace can use or delete them). Pin a version ID (`skver_…`) in production. Skills are not covered by zero-data-retention.

Skills uploaded in claude.ai are **not** available in the API and vice versa; upload separately. ([overview](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview))

---

## D. OpenAI Codex (CLI, IDE, app) — **yes, Codex supports SKILL.md (verified)**

Docs: [Build skills (Codex)](https://learn.chatgpt.com/docs/build-skills), skills catalogue [openai/skills](https://github.com/openai/skills)

- Codex skills *"build on the open agent skills standard"*: same `SKILL.md` with `name` + `description`; optional `scripts/`, `references/`, `assets/`, and a Codex-specific `agents/openai.yaml` for display metadata.
- **Where Codex looks:**
  - Repository: `.agents/skills` in the current folder and every parent up to the repo root
  - User: `~/.agents/skills`
  - Admin: `/etc/codex/skills`
  - System: bundled
- **Use:** `/skills` or type `$` to mention one (e.g. `$skill-creator`); Codex also picks a skill implicitly when the task matches its description.
- **Install:**
  ```bash
  npm install -g @openai/codex                 # or: brew install --cask codex
  mkdir -p ~/.agents/skills && cp -r my-skill ~/.agents/skills/
  # or, inside Codex:
  $skill-installer linear                      # installs curated skills from openai/skills
  # or, cross-agent:
  npx skills add mattpocock/skills -a codex
  ```
- **Plugins (bundles of skills + apps):** e.g. `codex plugin marketplace add mattpocock/skills` then `codex plugin add mattpocock-skills@mattpocock` (from Matt Pocock's README, not executed). OpenAI plugin docs: [Plugin development for ChatGPT and Codex](https://developers.openai.com/plugins).
- ⚠ The Codex docs page does not mention `~/.codex/skills`; use `~/.agents/skills`.

## E. Other coding agents (bonus)

| Agent | Skill folders | Source |
|---|---|---|
| Cursor | Project `.agents/skills/`, `.cursor/skills/`; user `~/.agents/skills/`, `~/.cursor/skills/`; **also reads** `.claude/skills/`, `.codex/skills/`, `~/.claude/skills/`, `~/.codex/skills/`. Invoke with `/skill-name`. | [Cursor: Agent Skills](https://cursor.com/docs/context/skills) |
| Gemini CLI | User `~/.gemini/skills/` or `~/.agents/skills/`; workspace `.gemini/skills/` or `.agents/skills/`. `gemini skills install https://github.com/user/repo.git --consent`, `/skills list`. (Docs note Gemini CLI was replaced by Antigravity CLI for unpaid/Google One users on 2026-06-18.) | [Gemini CLI: Agent Skills](https://geminicli.com/docs/cli/skills/) |
| GitHub Copilot, OpenCode, Amp, Cline, Zed, … | Mostly `.agents/skills/` (see the `npx skills` agent table) | [vercel-labs/skills](https://github.com/vercel-labs/skills) |

---

## F. ChatGPT

Docs: [Skills in ChatGPT](https://help.openai.com/en/articles/20001066-skills-in-chatgpt), [Projects in ChatGPT](https://help.openai.com/en/articles/10169521-projects-in-chatgpt), [Creating and editing GPTs](https://help.openai.com/en/articles/8554397-creating-a-gpt)

### F1. Native skills (Business, Enterprise, Healthcare, Edu)
*"Skills are available to eligible ChatGPT Business, Enterprise, Healthcare, and Edu users, subject to workspace settings."*
1. Sidebar → **Plugins** → **Plugin Directory** → **Skills** tab.
2. **Create** → **Upload from your computer** (or **Create with chat** / **Create with editor**). Uploaded skills are scanned; some are marked **Needs Review** or **Blocked**.
3. Admins control *Enable skills*, *Enable skill uploading*, sharing and publishing under **Permissions & roles**.
ChatGPT includes `skill-creator` by default for eligible accounts.

### F2. Fallback for Free / Plus / Pro (no native skills): use a Project
⚠ **Custom GPTs are no longer an option for most people:** OpenAI's help page says *"New GPT creation and publishing are not available on personal ChatGPT accounts, including Free, Go, Plus, and Pro,"* and custom GPTs are being retired in favour of Plugins (Enterprise retirement planned for Dec 11, 2026). Existing GPTs still work.

Instead:
1. **New project** in the sidebar.
2. **••• → Project settings** → paste the body of `SKILL.md` (everything after the frontmatter) into the project instructions, adding one line on top: *"When the user asks for X (copy the description), follow these instructions."* *"Project instructions apply only within that project and override your global custom instructions."*
3. Upload the skill's `references/` and `assets/` files as project files.
4. Scripts won't run automatically; ask ChatGPT to run them in its code tool if it has one, or drop them.

Quick one-off alternative: attach the `SKILL.md` to a chat and say "follow this" (the elayadesign README suggests the same for claude.ai without a terminal).

## G. Gemini app (gemini.google.com)

No native SKILL.md support in the Gemini **app** was found (the Gems help page doesn't mention skills; Gemini **CLI** does support them, see section E). Fallback: a **Gem**.
1. gemini.google.com → **Explore Gems** → **New Gem**.
2. Name it; paste the `SKILL.md` body into **Instructions** (Google suggests persona / task / context / format).
3. Under **Knowledge**, **Add files** for the skill's reference files (or from Google Drive).
4. **Save** (the preview does not save).
Source: [Tips for creating custom Gems](https://support.google.com/gemini/answer/15235603). ⚠ The page does not state which plans can create Gems or the file limits.

---

## H. Which surface for which audience member

| Person | Easiest path |
|---|---|
| Non-coder on Claude Pro/Max/Team | claude.ai → Customize > Skills (turn on Anthropic's) → upload ZIPs or add a marketplace under Customize > Plugins |
| Non-coder on ChatGPT Plus | A Project with the SKILL.md pasted into instructions |
| Non-coder on ChatGPT Business/Enterprise | Plugins → Skills → Upload from your computer |
| Gemini user | A Gem with the SKILL.md as instructions |
| Builder with a terminal | Claude Code: copy to `~/.claude/skills/`, or `/plugin install …`, or `npx skills add …`; Codex: `~/.agents/skills/` or `$skill-installer` |
| Developer shipping a product | Claude Skills API (GA): `client.skills.create` + `container.skills` + code execution tool |

### What could not be verified
- Plan eligibility for claude.ai skills (Free vs paid): two Anthropic pages disagree.
- The 200 vs 1,024 description limit in claude.ai uploads: two Anthropic pages disagree.
- Whether Claude Code reads `.agents/skills/` directly (undocumented).
- Gem availability by plan and file limits.
- None of the install commands were executed; they are quoted from the official docs or the repo READMEs.
