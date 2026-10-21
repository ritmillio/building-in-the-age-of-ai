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
- ChatGPT plan details (skills on Plus/Pro, custom GPT shutdown date for personal plans, ChatGPT Work by plan) could only be checked through search results, because OpenAI pages block bots. Before the event, open Plugins → Skills in a Plus account once and fix `skills/install.md` §F1 if it differs.
- `handout.pdf` (Desktop) is new and printable: skim both pages; the print count is "one per seat plus ten" because the seat count is not in any file. Its QR 404s until the repo is public.

## Health

**2026-10-21, compaction (iteration 24), branch head `3338328`, presenter folder head `03c91da` (clean tree):**
- `.loop/gates/check.sh; echo EXIT=$?` → `ok confidentiality (repo)` / `ok deck Building-in-the-Age-of-AI-v16.pptx: 40 slides, 40 notes, clean` / `ok relative links` / `GATE_EXIT=0` / `EXIT=0`.
- External links added on the branch (`git diff origin/main..HEAD`, docs/ excluded): 49 unique, 40 `curl -sIL` 200, 6 OpenAI 403 (known bot block), 3 support.google.com HEAD 404 / GET 200 (known, fine). No dead link.
- PDFs (pdfinfo): repo `workshop/slides.pdf` 40, Desktop `handout.pdf` 2, `script.pdf` 6, `rehearsal.pdf` 2, `prompt-pack.pdf` 5. No deck or HTML change since compaction 16, nothing re-rendered.
- Counts match the claims: tricks.md 73 tricks, 45 without "Fails when" (28-36, 38-73 = T22+T23); templates/ 8 files.
- Reconciled: all 16 content commits and 25 ledger commits on the branch, and all 12 presenter-folder commits (9a46874..03c91da), are in Landed or the log. No unsupported claim found; T24/T25 evidence re-checked by grep and still true.

Script time (T6, 140 wpm vs slot): Opening 230w 1.6/10 min, Perspective 674w 4.8/25, Context 301w 2.1/12, How we build 563w 4.0/15 (tightest), Raising 276w 2.0/10, Build 498w 3.6/60, Close 187w 1.3/27; total 2760w.

## Standing rules

- Findings come from running the thing, not from reading the source. Commit before exiting.
- **Never name**: the coding reference app (T3, t3code, pingdotgg, create-t3-app), the "mike" legal OSS project, the founder's company/product by name (no "Clausis", no "jogai"), "second brain", the founder's location (Vienna, remote, where he lives), Billingo or Billy. Say "our product", "our team".
- **The hub** (where every agent files what it did, why and how it was checked) may only appear as the team's internal practice, spoken (script/notes), never on a slide, never named as a product, never "we are building this".
- **Slides:** Excalidraw style, every text Excalifont (terminal lines Comic Shanns), NO numbers, stats or years on slides (numbers only in notes, script, repo). Native English. All deck changes go into v16 (`.deck-build-v16.mjs`, OUT `Building-in-the-Age-of-AI-v16.pptx`), never a v17, v15 untouched; the v15 builder reads only `layout`, backup slides 38-40 come from the `backup` export in `drawings/slides.mjs`. Render: `cd ~/Desktop/building-in-the-age-of-ai/drawings && node render.mjs <scene> && node render-slides.mjs <name>`, then `NODE_PATH=/private/tmp/claude-501/-Users-zoltanfodor-Developer-clausis-ai/6aaa65e6-ef45-465a-9cb7-d307bf4c4c6e/scratchpad/deps/node_modules node .deck-build-v16.mjs` (if gone: `npm i --prefix /tmp/kh-deps pptxgenjs sharp qrcode`, use `/tmp/kh-deps/node_modules`), then `soffice --headless --convert-to pdf <pptx>`. View changed pages as PNG (pdftoppm -r 60), copy the PDF to repo `workshop/slides.pdf`, check pages 1-37 `cmp` equal to v15 at `pdftoppm -r 40`.
- **Presenter folder git:** commit `.excalidraw`, `drawings/slides/*.png` and `.html` sources; scene PNGs and all PDFs are gitignored there (re-render). Every presenter-folder commit gets a log line here, small follow-ups too (`0066c04` was missed once).
- **Tricks are real.** Every trick is something the founder actually does (source: the clausis.ai repo `AGENTS.md`, `.agents/skills/*`, `docs/reference/*`, memory notes in `~/.claude/projects/-Users-zoltanfodor-Developer-clausis-ai/memory/*.md`, especially `feedback-*.md`), or a vendor-documented practice with a link. Never copy internal names, customers, money, tickets, people or URLs; generalise, and flag anything embarrassing under `## For the founder`. The inventory is gate-excluded: scan it by hand, never copy a `src:` path into a public file.
- **Every external claim gets a link** checked by opening it. Date-sensitive vendor claims (ChatGPT Work, Claude Cowork, Gemini skills, Cursor) get checked on the vendor page with the check date written down.
- **Link checking:** mass check with `tr '\n' '\0' < list | xargs -0 -P 24 -n 1 script.sh` (plain `xargs -I{} sh -c` dies). Bot blocks, not dead links: help.openai.com, openai.com, chatgpt.com, claude.ai, carta.com, lovable.dev, lmarena.ai (403); support.google.com (HEAD 404, GET 200, bit twice); ai.meta.com (400, WebFetch reads it). OpenAI pages can't be read: name the page, don't cite a number from it; use WebSearch for their content. YC Startup Library renders client-side: cite the YC YouTube video (title via `curl https://www.youtube.com/oembed?url=...`), library page secondary.
- **Anchors:** the gate strips `#...`, so run a short python slug check (lowercase, drop chars outside `[\w\- ]`, spaces to `-`) on every `](file#anchor)` you add. README "Start here, by role" cites trick numbers (1, 8-13, 19-25, 28-39, 41-49, 50-58, 60-67) and war-stories anchors: renumbering or renaming headings means updating it.
- **Pairs edited together:** `workshop/prompts.md` ↔ Desktop `prompts.md` (differ only in header, slide cues, succeed.md link form); `workshop/faq.md` ↔ Desktop `qa.md` (plain pointers, numbers only "if asked"). A new template gets a README templates-row entry and a link from the trick it serves.
- **Tone.** Plain, concrete, first person plural, no hype, no em dash runs, no emoji. Each trick: what to do, why it works, the exact prompt/command/file, when it fails.
- **Time:** speaker script and run sheet keep fitting 3 hours. Added spoken lines mean cuts elsewhere; count only `.say`/`.bridge` text (strip `.cue`, `.src`) at ≈140 wpm and update the table at the end of `script.html` and the numbers in `## Health`.
- **Gate before every commit:** `.loop/gates/check.sh; echo EXIT=$?` (never pipe it through tail). HTML→PDF: `node /private/tmp/claude-501/-Users-zoltanfodor-Developer-clausis-ai/6aaa65e6-ef45-465a-9cb7-d307bf4c4c6e/scratchpad/pdf.mjs <abs html> <abs pdf>`, view every page. Handout stays 2 pages (`pdfinfo handout.pdf | grep Pages`).
- War stories 2, 6, 10 tell well out loud; script lines and backup slides can borrow from `guides/war-stories.md`.
- Skills repo check: `npx skills add <owner/repo> --list` in an empty `git init` dir under /tmp; it uses local git credentials, so it does not prove public access.
- Print HTML (prompt pack, handout): wrap each heading with its block in a `break-inside: avoid` div, or Chrome leaves a heading alone at the page foot. Prompt pack is 5 pages now; `README.md` (repo + Desktop) state the page count.
- Inventory coverage is complete (T19): every publishable inventory item is in tricks.md, war-stories.md or a template. New tricks from now on come from fresh sources, not the inventory. Prefer folding a small habit into an existing trick over renumbering.
- When the ledger script inserts text before a heading, anchor on `\n## Heading\n`, not the bare heading text: the "How to read this" line names every section in backticks.
- Missing "Fails when" check: `python3 - <<'E'` splitting tricks.md on `(?m)^(?=\*\*\d+\. )` and listing paragraphs without `Fails when`. Insert the clause before a trailing ` Template: ` if the paragraph has one, else at the end. A failure mode that names vendor behaviour gets its doc link.

## Backlog

Ordered by value to the mission. T1-T14 and T16-T21 are done. T15 is for the last iteration only; before then, an empty backlog means a hunt (append 3-6 evidence-backed items).

- [ ] **T22 tricks.md "Fails when", batch 2 (tricks 28-49).** Missing: 28-36, 38-49. Rule: standing rule "Missing Fails when check".
- [ ] **T23 tricks.md "Fails when", batch 3 (tricks 50-73).** Missing: every trick 50-73. Same rule; after this batch the regex must report 0 missing (or soften the intro claim for tricks with no honest failure mode).
- [ ] **T24 follow-along.md afterwards + Gemini Projects.** "Afterwards" (line 38) points only to prompt 7; add prompts 8-12, tricks.md and succeed.md. Line 8 says "in Gemini, a new chat is fine": press reports (Android Authority, dataconomy 2026-04-07) say Gemini Projects (maybe renamed Notebooks) was in limited testing; no Google announcement found by search. Check the Google help page, date it, fix the line if Projects shipped.
- [ ] **T25 Cross-links.** `guides/context.md` and `guides/scaffolding.md` never link tricks.md (grep 0): context.md §7 → tricks 1-7, scaffolding.md → trick 35 (fresh worktree has no `.env`) and 55-58. README `skills/` row (line 60) lists "Claude Code, claude.ai, ChatGPT and Gemini" but install.md also covers Codex (§D) and other agents (§E). Anchor-check every link added.
- [ ] **T15 Final read-through.** Last iteration only: README → guides as a first-time visitor, fix the three worst confusions, Desktop README up to date.

## Iteration log

- 2f05a40 T19: all 99 inventory items mapped to tricks.md; only 43 (monorepo worktree borrowing node_modules), 50 (forgotten caffeinate) and 71 (sans for reading text) were publishable and missing. Folded into tricks 35, 39, 53 so numbering (README roles, slide notes #8/#28/#40) stays put; still 73 tricks. Wording checked against the memory notes; `caffeinate -t 1`, `-i true`, `-w <pid>` all ran EXIT 0; banned grep empty; gate 0.
- Desktop 62d0760 T17: handout back-page pointer now names templates/ (AGENTS.md starter, never list, review prompt for a fresh session). Rendered: 2 pages (pdfinfo), page 1 unchanged, page 2 viewed at -r 110, line wraps in the footer with room to spare. No repo copy of the handout, so no repo file changed. Gate 0.
- hunt (iteration 21): backlog was only T15, so hunted. Evidence: pdfinfo slides.pdf 40 pages vs README "37 slides"; rehearsal.html still "v15 (37 slides)"; tricks.md regex 63/73 without `Fails when:` against an intro that promises it; follow-along afterwards stops at prompt 7; context.md/scaffolding.md grep for tricks.md empty; Gemini Projects status via WebSearch (testing, unconfirmed). Prompts and faq/qa pairs diff clean. Gate 0. Added T20-T25.
- 58f8b6a + Desktop 03c91da T20: repo README deck row now "37 slides plus 3 Q&A backup slides" (slides.pdf is 40 pages); rehearsal.html header says v16 (37 + 3 backups) and the 2:40 Q&A row says when to show 38-40 (titles from `backup` in slides.mjs). rehearsal.pdf re-rendered, still 2 pages, both viewed at -r 70. grep for "37 slides" now only hits correct lines (README, Desktop README, script.html, rehearsal). Gate 0.
- 33cb94a T21: tricks 3, 6, 7, 9, 11-13, 16-22, 24-27 get one *Fails when:* each (18), grounded in war stories and memory notes (versions, English keys, model price). Regex now 45 missing (28-36, 38-73), exactly T22+T23. New claims sourced: git-config core.symlinks (200, anchor id present) on 19, Claude Code skills page (200, "description helps Claude decide when to load") on 24; war-stories anchor slug ok; no em dash, banned grep empty; gate 0.

## Landed

By theme; the five newest are in the Iteration log above.

- **Raw material:** `0c4263d` `docs/tricks-inventory.md`, 99 items, tagged `[have] [war] [S] [product]` (internal, gate-excluded); `2f05a40` coverage pass, every publishable item now in a public file.
- **Repo guides:** `882602b` `guides/tricks.md` (73 tricks); `9177a68` `guides/war-stories.md` (12 + 1); `39767f5` `guides/succeed.md` (7 sections, 8 prompts); `368b0ec` + Desktop `13d4f1b` faq.md / qa.md "The tricks, agents and selling", 8 questions.
- **Repo entry points, prompts, templates, skills:** `2fa629b` README "Start here, by role"; `03ef12d` + Desktop `f1c1b2d` prompts 8-12 in both prompts.md; `0916368` 4 templates (never-list, ask-with-options, review-prompt, interview-notes); `9466bc0` skills README with tested `npx skills add` commands, two more author skills.
- **Fact sweeps (vendor claims, dated 2026-10-21):** `7e3e779` + Desktop `6dc3f35` 596 links re-checked, Gemini skills / Gems conversion rewritten in install.md §G and mirrors; `59b2c57` ChatGPT §F: Plus/Pro skills unclear, GPT retirement dated for Enterprise only, Work claim softened.
- **Presenter folder:** `9a46874` v15 sources; `811818e` 2-page handout (+`0066c04`); `1ccdddc` script +7 trick lines, 3 cuts, time table; `84bd465` deck v16 notes-only; `303e32c` + repo `fcf2ab6` v16 3 Q&A backup slides (38-40), pages 1-37 identical to v15; `341950c` + repo `f6b21d4` prompt pack prompts 8-12, 5 pages.
- **Ledger commits:** `a9c5472` `40c8883` `0a0e5e5` `48f4e79` `e8c4ae3` `d51f57a` `daa4617` `9c4520f` `fc7cec3` `a833257` (compaction 8) `328b1c9` `7ff9fbf` `b3beaec` `32e5ff4` `6ee46af` `b315ebe` `19ae4ce` (compaction 16) `3fa4f93` `1fdd032` `d7c0a9b` `f2b9ed0` `8f46c14` `08c7cd6` `5205833` `3338328`.
