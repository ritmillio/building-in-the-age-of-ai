# Overnight relay: every trick for building faster with AI (K&H workshop)

**Mission.** Make the K&H workshop "Building in the Age of AI" and its companion repo the most useful thing a founder or product person can take home: share every trick and good practice we use to build faster with AI, and what it takes to succeed (validate, sell, raise, stay small), each one concrete, sourced and copy-pasteable.

**Run.** Started 2026-10-21 ~01:30 on branch `feat/tricks-overnight-1021` (worktree `~/Developer/building-in-the-age-of-ai-tricks-overnight-1021`), forked from `main` @ `9bb4d58`. Draft PR: see the PR on ritmillio/building-in-the-age-of-ai (private). Time budget 7.5h. Driver: the `relay` skill.

**Two places you work in.**
1. This worktree = the companion repo (goes PUBLIC before the event, so everything here is public-grade).
2. The presenter folder `~/Desktop/building-in-the-age-of-ai` (absolute path, local git repo on `main`, no remote). Deck sources (`drawings/slides.mjs`, `drawings/scenes.mjs`, `.deck-build-v15.mjs` with NOTES + ALT), `script.html` (speaker script), `rehearsal.html`, `prompts.md`, `qa.md`, `prompt-pack.html`, `kh-email.md`. Commit there too, explicit paths: `git -C ~/Desktop/building-in-the-age-of-ai add <paths> && git -C ~/Desktop/building-in-the-age-of-ai commit -m "..."`. Never `git add -A` there either.

**In scope.** New and improved guides in the repo (tricks field guide, succeed/go-to-market guide, war stories, role-based start paths, more prompts and templates, more skills with credits), the speaker script, prompt pack / a printable handout, Q&A prep, speaker notes, and deck slides when a change clearly earns its place (a new deck version v16, never overwriting v15).

**Out of scope.** Flipping the repo public. Pushing to `main`. Merging. Sending the K&H email. Deploying anything (no `vercel`). Re-adding the cut "tricks" slide to the main flow (founder cut it 10-20; Q&A backup slides AFTER slide 37 are fine). Changing the talk's structure or timing without a founder note.

**Ends when.** The clock runs out (7.5h).

**How to read this.** `## For the founder` is your inbox, read it first. `## Health` is the current gate status. `## Landed` is what shipped. `## Backlog` is what the loop would do next if it kept running.

---

## For the founder

- `docs/tricks-inventory.md` is internal raw material (private source paths). Delete it with the ledger before going public.
- Inventory items tagged `[S]` (env var outage story, startup credit amounts) stay out of public files unless you OK a generalised version. Model vetoes and the runtime model ruling are listed under "Not for publication" there.
- Ledger file `docs/relay-tricks-1021.md` lives in the repo branch; delete it (or squash it out) before flipping the repo public.

## Health

_(no compaction iteration has run yet)_

Baseline 2026-10-21 01:30: `.loop/gates/check.sh` GATE_EXIT=0 (confidentiality clean, v15 deck 37 slides / 37 notes, relative links ok).

## Standing rules

- Findings come from running the thing, not from reading the source.
- Commit before exiting. An uncommitted change does not survive the iteration.
- **Never name**: the coding reference app (T3, t3code, pingdotgg, create-t3-app), the "mike" legal OSS project, the founder's company/product by name (no "Clausis", no "jogai"), "second brain", the founder's location (Vienna, remote, where he lives), Billingo or Billy. Say "our product", "our team".
- **The hub** (where every agent files what it did, why and how it was checked) may only appear as the team's internal practice, spoken (script/notes), never on a slide, never named as a product, never "we are building this".
- **Slides:** Excalidraw style, every text Excalifont (terminal lines Comic Shanns), NO numbers, stats or years on slides (numbers only in notes, script, repo). Native English. A new slide or changed slide means a new deck version: copy `.deck-build-v15.mjs` to `.deck-build-v16.mjs` once (OUT file `Building-in-the-Age-of-AI-v16.pptx`), keep v15 untouched. Render: `cd ~/Desktop/building-in-the-age-of-ai/drawings && node render.mjs <scene> && node render-slides.mjs <name>`, then `NODE_PATH=/private/tmp/claude-501/-Users-zoltanfodor-Developer-clausis-ai/6aaa65e6-ef45-465a-9cb7-d307bf4c4c6e/scratchpad/deps/node_modules node .deck-build-v16.mjs`, then `soffice --headless --convert-to pdf <pptx>` in that folder. Look at the changed pages as PNG (pdftoppm -r 60) before committing. If the NODE_PATH dir is gone, `npm i --prefix /tmp/kh-deps pptxgenjs sharp qrcode` and use `/tmp/kh-deps/node_modules`.
- **Tricks are real.** Every trick is something the founder actually does (source: the clausis.ai repo `AGENTS.md`, `.agents/skills/*`, `docs/reference/*`, and the memory notes in `~/.claude/projects/-Users-zoltanfodor-Developer-clausis-ai/memory/*.md`, especially `feedback-*.md`), or a vendor-documented practice with a link. Read those as source material; never copy internal names, customers, money, tickets, people or URLs out of them. Generalise ("an agent deleted production env vars" style), and flag anything that could embarrass the company under `## For the founder` instead of publishing it.
- **Every external claim gets a link** checked by opening it (curl -sIL or WebFetch). Vendor product names change monthly: check the date-sensitive ones (ChatGPT Work, Claude Cowork, Gems→skills, Cursor) against the vendor page, write the check date.
- **Tone.** Plain, concrete, first person plural, no hype, no em dash runs, no emoji. Each trick: what to do, why it works, the exact prompt/command/file, when it fails.
- Speaker script and run sheet must keep fitting 3 hours. If you add spoken lines, cut elsewhere; count words (≈140 wpm) and note the per-part estimate in `## Health`.
- Gate before every commit: `.loop/gates/check.sh; echo EXIT=$?` (never pipe it through tail). For HTML→PDF use `node /private/tmp/claude-501/-Users-zoltanfodor-Developer-clausis-ai/6aaa65e6-ef45-465a-9cb7-d307bf4c4c6e/scratchpad/pdf.mjs <abs html> <abs pdf>` (uses playwright-core from ~/Developer/clausis.ai/node_modules); look at the pages.

- The inventory is gate-excluded; scan it by hand before relying on it, and never copy a `src:` path into a public file.

## Backlog

- [x] **T1 Tricks inventory.** Done in 0c4263d: `docs/tricks-inventory.md`, 99 tricks in 10 groups, each with source, tags `[have]` `[war]` `[S]` `[product]`.
- [ ] **T2 `guides/tricks.md` field guide.** From T1 (skip `[S]` items, link `[have]` items to the existing repo file instead of repeating them; vendor-link the shared-agent-setup tricks 23-27 from the sources listed in the inventory): 40-60 tricks grouped (Context, Prompting, Rules & skills, Agents & parallel work, Verification, Design, Shipping & ops, Team & process, Money & tools). Each: what, why, exact prompt/command/file, when it fails, link. Link it from README "Start here".
- [ ] **T3 War stories.** Candidates are tagged `[war]` in `docs/tricks-inventory.md` (about 20). `guides/war-stories.md`: 8-12 short real incidents and the rule each produced (build piped through tail; type check skipped by build; stale dev server; agent stashing a shared checkout; `git add -A` sweeping another agent's work; schema pushed instead of migrated; a "fixed" claim never checked in the browser...). Generalised, no internal names. Anything sensitive → founder inbox, not the file.
- [ ] **T4 Succeed guide.** `guides/succeed.md`: validating with AI (interview synthesis, review mining, landing tests), pricing conversations, first ten customers, distribution through partners, staying small, metrics that matter early. Every claim sourced (YC, First Round, a16z, Lenny's, vendor docs). Cross-link fundraising.md.
- [ ] **T5 Printable handout.** `~/Desktop/building-in-the-age-of-ai/handout.html` → `handout.pdf`, 2 pages A4: the 25 best tricks + 5 prompts + the repo QR (`.assets/repo-qr.png`). Plain, legible, no numbers-as-stats. Mention in rehearsal.html's day-before list (print N copies).
- [ ] **T6 Speaker script weave.** Add the strongest 1-2 tricks per part into `script.html` as spoken lines on the slides they fit, cut weaker lines to keep time; re-render `script.pdf`. Add a word-count/time table per part at the end.
- [ ] **T7 Speaker notes sync.** Mirror the script's new lines into the deck NOTES (v16 build), rebuild, gate passes (notes == slides).
- [ ] **T8 Q&A backup slides.** 3-5 slides AFTER 37 (section "Backup"), Excalidraw, no numbers: e.g. "My daily setup", "The verify loop", "Five prompts to steal", "Templates I start from". Only if they read well; otherwise drop and note why.
- [ ] **T9 Role-based start paths.** README "Start here": non-technical founder / product person / developer / team lead, each 5 steps with links into the repo.
- [ ] **T10 More prompts for non-builders.** `workshop/prompts.md` (+ Desktop `prompts.md`): sales follow-ups, investor update, customer interview synthesis, competitor teardown, weekly ops digest, contract first-read with "not legal advice" caveat. Same five-part brief shape as slide 13.
- [ ] **T11 Templates.** `templates/`: decisions-as-options rule, review prompt for a PR, handoff (exists?), customer-interview synthesis, design-rules (exists?), "never list" for a project. Check what exists first.
- [ ] **T12 Skills check.** `skills/`: confirm each listed skill installs with `npx skills add` (run it in a temp dir), credits present, add any missing generic ones (handoff, grill, root-cause) with attribution.
- [ ] **T13 qa.md + faq.md.** Add the questions the tricks will provoke (cost of running agents, which plan, data safety in tools, "is this only for developers?"), with sourced answers.
- [ ] **T14 Link + fact sweep.** Open every external link added tonight; fix or drop dead ones; re-check the date-sensitive vendor facts in notes and repo; record dates.
- [ ] **T15 Final read-through.** Read README → guides as a first-time visitor; fix the three worst confusions; update the deck folder README (v16 if built).

## Iteration log

- 0c4263d T1: wrote `docs/tricks-inventory.md` (99 tricks, sources = product AGENTS.md, shared-agent-setup ref, skills, 38 feedback + ~20 general memory notes). Gate EXIT=0; inventory is gate-excluded by design, scanned by hand for banned words (none). No external links added.

## Landed
