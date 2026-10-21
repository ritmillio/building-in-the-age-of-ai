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

**2026-10-21, compaction (iteration 16), branch head `b315ebe`, presenter folder head `6dc3f35` (clean tree):**
- `.loop/gates/check.sh; echo EXIT=$?` → `ok confidentiality (repo)` / `ok deck Building-in-the-Age-of-AI-v16.pptx: 40 slides, 40 notes, clean` / `ok relative links` / `GATE_EXIT=0` / `EXIT=0`.
- External links added on the branch (`git diff origin/main..HEAD`, docs/ excluded): 42 unique, 39 `curl -sIL` 200, 3 support.google.com HEAD 404 / GET 200 (known, fine).
- PDFs: `handout.pdf` 2 pages, `script.pdf` 6 pages, repo `workshop/slides.pdf` 40 pages (pdfinfo). No deck or HTML change this iteration, nothing re-rendered.
- Counts match the claims: tricks.md 73 tricks / 10 groups, war-stories.md 12 + 1, templates/ 8 files, inventory 99.
- Reconciled: every branch commit and every presenter-folder commit (9a46874..6dc3f35) is in Landed or the log; no unsupported claim found.

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

## Backlog

Ordered by value to the mission. T1-T14, T16 and T18 are done.

- [ ] **T19 Inventory coverage pass.** tricks.md has 73 of the inventory's 99; skipped on purpose: 72, 75-76, 92, 99, `[S]` and "Not for publication". Diff the rest against tricks.md, war-stories.md, succeed.md and templates; add any publishable trick still missing (same what/why/command/fails-when shape, update trick counts and README role numbers if renumbered).
- [ ] **T17 Handout pointer to the new templates.** Optional: the handout's take-home list could name `templates/never-list.md` and `review-prompt.md` (not there now); only if it stays 2 pages.
- [ ] **T15 Final read-through.** Last iteration only: README → guides as a first-time visitor, fix the three worst confusions, Desktop README up to date.

## Iteration log

- 368b0ec + Desktop 13d4f1b T13: faq.md and qa.md get "The tricks, agents and selling", 8 questions (only-for-devs, cost/plans, agent data safety, verification, production, parallel agents, validate-first, model choice). claude.com/pricing, lethal-trifecta post, Claude Code security page 200 and read; 23 anchors BAD=0; banned grep empty; gate 0.
- 0916368 T11: 4 templates (never-list, ask-with-options, review-prompt, interview-notes), linked from README, AGENTS.md, trick 8, succeed §1. `/code-review` (alias `/review`) and `/security-review` read on code.claude.com commands page; 2 links 200; 7 anchors BAD=0; banned grep empty; gate 0.
- Desktop 303e32c + repo fcf2ab6 (slides.pdf) T8: v16 gets 3 Q&A backup slides after 37 (reused cut `tricks` scene; new `steal` five-prompts and `starters` six-files scenes), notes with trick numbers checked against tricks.md (#8, #28, #40), ALT text, README + script header. Pages 1-37 cmp-identical to v15, 38-40 viewed as PNG (one heading overflow fixed), script.pdf 6 pages, gate 0 (40 slides, 40 notes). Dropped "daily setup" and "verify loop": they repeat slides 21 and 22.
- 9466bc0 T12: skills README gets tested install commands (GitHub `ritmillio/building-in-the-age-of-ai` and `./skills`), worktree-janitor + memory-hygiene rows, handoff/grill-me pointer; third-party.md + install.md record the run. `npx skills add ./skills --skill '*' -a claude-code -y` in empty /tmp project → 6 SKILL.md; `--list` on 6 third-party/author repos lists every named skill; frontmatter checked; gate 0. Handoff skill is Matt Pocock's, credited, not rewritten.
- 7e3e779 + Desktop 6dc3f35 T14: 596 repo links + 2 presenter links curl-checked; non-200s were bot blocks or GET-200 on retry; Meta Rule of Two read via WebFetch. Stale claim fixed: the Gemini app has native skills and Gems convert from November 2026, so install.md §G was rewritten from Google help 17094296 + 18560919 (read 2026-10-21), plus README no-terminal line, how-i-build, context, faq, qa. Cursor skills dirs and Cowork plans + scheduling still match vendor pages. Gate 0.
- 59b2c57 T18: install.md §F: Plus/Pro skills marked unclear (help page names workspace plans only, pricing reports differ) with an in-account check; GPT retirement dated only for Enterprise (2026-12-11), no date for personal plans; migration FAQ linked (403 bot block, indexed in ~10 locales); resources.md ChatGPT Work "paid plans" claim softened (desktop reportedly on all plans). OpenAI pages 403 in WebFetch, so this was checked through WebSearch. faq/qa have no GPT claims to mirror. Gate 0.
- f6b21d4 + Desktop 341950c T16: prompt-pack.html gets "After the workshop: five more prompts" (8-12 verbatim from prompts.md, Elad Gil credited as plain text) on new pages 4-5 before "Where to start". First render orphaned a heading; wrapped each h3+prompt in `.keep` (break-inside: avoid), re-rendered: 5 pages, all viewed at -r 60, pages 1-3 unchanged. PDF copied to repo; README rows (repo + Desktop) say 5 pages. Gate 0.

## Landed

By theme; the five newest are in the Iteration log above.

- **Raw material:** `0c4263d` `docs/tricks-inventory.md`, 99 tricks in 10 groups, tagged `[have] [war] [S] [product]` (internal, gate-excluded).
- **Repo guides:** `882602b` `guides/tricks.md`, 73 tricks, 22 links 200; `9177a68` `guides/war-stories.md`, 12 stories + 1 on model price, generalised; `39767f5` `guides/succeed.md`, 7 sections, 8 prompts, 12 links 200, YC titles via oEmbed.
- **Repo entry points:** `2fa629b` README "Start here, by role" (4 roles x 5 steps, 31 links + anchors BAD=0); `03ef12d` + Desktop `f1c1b2d` prompts 8-12 (sales follow-up, investor update, competitor teardown, meeting decisions, contract first read) in both prompts.md.
- **Presenter folder:** `9a46874` v15 sources as local history; `811818e` 2-page A4 handout (+`0066c04` rebuttal lines rewritten); `1ccdddc` script +7 trick lines, 3 cuts, time table (+148 words, 6 pages); `84bd465` deck v16 notes-only, trick lines in notes of 13/18/21/22/29/32/37, pages pixel-identical to v15.
- **Ledger commits:** `a9c5472` `40c8883` `0a0e5e5` `48f4e79` `e8c4ae3` `d51f57a` `daa4617` `9c4520f` `fc7cec3` `a833257` (compaction 8) `328b1c9` `7ff9fbf` `b3beaec` `32e5ff4` `6ee46af` `b315ebe` `3fa4f93`.
