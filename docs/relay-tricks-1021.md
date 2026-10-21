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
- `handout.pdf` (Desktop) is new and printable: skim both pages; the print count is "one per seat plus ten" because the seat count is not in any file. Its QR 404s until the repo is public.

## Health

**2026-10-21, compaction (iteration 8), branch head `fc7cec3`, presenter folder head `84bd465` (clean tree):**
- `.loop/gates/check.sh; echo EXIT=$?` → `ok confidentiality (repo)` / `ok deck Building-in-the-Age-of-AI-v16.pptx: 37 slides, 37 notes, clean` / `ok relative links` / `GATE_EXIT=0` / `EXIT=0`.
- External links in `guides/tricks.md`, `guides/succeed.md`, `guides/war-stories.md`: 34 unique, all 34 `curl -sIL` 200.
- PDFs: `handout.pdf` 2 pages, `script.pdf` 6 pages (pdfinfo). No deck or HTML change this iteration, so nothing re-rendered.
- Counts match the claims: tricks.md 73 tricks / 10 groups, war-stories.md 12 + 1, inventory 99.

Script time (T6, 140 wpm vs slot): Opening 230w 1.6/10 min, Perspective 674w 4.8/25, Context 301w 2.1/12, How we build 563w 4.0/15 (tightest), Raising 276w 2.0/10, Build 498w 3.6/60, Close 187w 1.3/27; total 2760w.

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

- Anchor links into other repo files (`file.md#heading`) are not checked by the gate (it strips `#...`); derive GitHub anchors by hand: lowercase, drop punctuation, spaces to `-`.
- War stories exist in `guides/war-stories.md`; T6 script lines and T8 backup slides can borrow from them (stories 2, 6, 10 tell well out loud).
- The inventory is gate-excluded; scan it by hand before relying on it, and never copy a `src:` path into a public file.
- The YC Startup Library pages render client-side (WebFetch sees only the title); cite the YC YouTube video (title via `curl https://www.youtube.com/oembed?url=...`) and link the library page as secondary.
- Script word counts: count only `.say`/`.bridge` text, strip `.cue` and `.src` spans; the table at the end of `script.html` holds the per-part numbers, update it if you add lines.
- Deck v16 exists (`.deck-build-v16.mjs`, notes-only over v15). Any further deck change goes into v16, not a v17. The repo's `workshop/slides.pdf` was not refreshed (slides unchanged); refresh it only if slides change.
- Every presenter-folder commit gets a log line here, including small follow-ups (`0066c04` was missed once).
- The handout's PDF and other PDFs are gitignored in the Desktop repo; commit the `.html` source and re-render. Handout must stay 2 pages: re-check `pdfinfo handout.pdf | grep Pages` after any edit.

## Backlog

Ordered by value to the mission. T1-T7 are done (see Landed).

- [ ] **T9 Role-based start paths.** README "Start here": non-technical founder / product person / developer / team lead, each 5 steps linking into tricks.md, succeed.md, war-stories.md and the existing guides. Cheapest way to make tonight's three guides findable.
- [ ] **T10 More prompts for non-builders.** `workshop/prompts.md` (+ Desktop `prompts.md`): sales follow-ups, investor update, customer interview synthesis, competitor teardown, weekly ops digest, contract first-read with "not legal advice" caveat. Same five-part brief shape as slide 13. Do not duplicate the 8 prompts in succeed.md or the 5 on the handout; link to them.
- [ ] **T13 qa.md + faq.md.** Questions the tricks will provoke (cost of running agents, which plan, data safety in tools, "is this only for developers?"), sourced answers. succeed.md's partner prompts can be borrowed.
- [ ] **T11 Templates.** `templates/`: decisions-as-options rule, PR review prompt, customer-interview synthesis, "never list" for a project. `ls templates/` first; handoff and design-rules may already exist.
- [ ] **T8 Q&A backup slides.** 3-5 slides AFTER 37 in `.deck-build-v16.mjs` (no v17), Excalidraw, no numbers: "My daily setup", "The verify loop", "Five prompts to steal", "Templates I start from". Only if they read well; otherwise drop and note why. Costs a full render + PNG check.
- [ ] **T12 Skills check.** `skills/`: each listed skill installs with `npx skills add` in a temp dir, credits present; add missing generic ones (handoff, grill, root-cause) with attribution.
- [ ] **T14 Fact sweep.** Repo guide links all re-checked 200 at compaction; what is left: links added after this point, links in Desktop `script.html` / notes / `prompt-pack.html`, and the date-sensitive vendor names (ChatGPT Work, Claude Cowork, Gems→skills, Cursor) checked against vendor pages with a date.
- [ ] **T15 Final read-through.** Run in the last iteration: README → guides as a first-time visitor, fix the three worst confusions, Desktop README up to date.

## Iteration log

- 9177a68 T3: `guides/war-stories.md`, 12 stories + 1 on model price, from memory notes + migration incident log, generalised. Gate 0; no external links; trick numbers cross-checked.
- 39767f5 T4: `guides/succeed.md`, 7 sections, 8 prompts, README row, fundraising cross-link. Gate 0; 12 links 200, claims read on page, YC titles via oEmbed, 7 anchors checked.
- Desktop 811818e (+0066c04) T5: `handout.html` 2-page A4 (first render was 4, tightened), print step in rehearsal, README row. All pages viewed; gate 0.
- Desktop 1ccdddc T6: `script.html` +7 trick lines, 3 cuts, time-check table, net +148 words. script.pdf 6 pages viewed; gate 0.
- Desktop 84bd465 T7: v16 = v15 slides + trick lines in notes of 13/18/21/22/29/32/37; 37 PDF pages pixel-identical to v15, notes diff exact. Gate 0 on v16.

## Landed

Older iteration-log entries, collapsed. The newer ones are in the Iteration log above.

- **Raw material:** `0c4263d` `docs/tricks-inventory.md`, 99 tricks in 10 groups with source and `[have] [war] [S] [product]` tags (internal, gate-excluded, scanned by hand). Ledger `a9c5472`, `40c8883`.
- **Repo guides:** `882602b` `guides/tricks.md`, 73 tricks (what / why / command / fails-when), README row, how-i-build cross-link, 22 links 200, vendor claims read on page. Skipped inventory 72, 75-76, 92, 99. Ledger `0a0e5e5`, `48f4e79`. Then `9177a68` war stories and `39767f5` succeed guide (see log); ledger `e8c4ae3`, `d51f57a`.
- **Presenter folder:** `9a46874` v15 sources imported as local history; `811818e` handout + `0066c04` three rebuttal lines on the handout rewritten as plain statements (this commit was missing from the ledger until compaction); `1ccdddc` script; `84bd465` deck v16 notes. Ledger `daa4617`, `9c4520f`, `fc7cec3`.
