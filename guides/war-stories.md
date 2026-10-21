# War stories

Twelve things that went wrong while we built with AI agents, what each one cost, and the rule it left behind. Every rule in the [tricks field guide](tricks.md) that carries an incident has its story here. Nothing in this list was exotic: each one was a normal tool doing exactly what it was told.

Read them as a checklist of failure modes. If you run more than one agent, or let an agent tell you "done", you will meet most of them.

## When agents share a checkout

**1. The branch that moved under us.** We ran several agent sessions in one project folder. One session switched the folder to its own branch in the middle of another session's work, twice in one afternoon. The second session's commits landed on the wrong branch and had to be copied back by hand, and the other branch cleaned up. A few days later it happened again, even though the agent now printed the branch name before each commit: it printed the wrong name and committed anyway, because printing is not checking.
*Cost:* an hour of untangling branches, and a day of not trusting the history.
*Rule:* one worktree per agent ([trick 28](tricks.md)), and a hard branch check in the same command as the commit ([trick 29](tricks.md)): `[ "$(git branch --show-current)" = feat/x ] && git commit -m "..."`.

**2. The ten-second stash.** An agent wanted to compare a test against the last committed version, so it ran `git stash`. Several agents shared that folder. The stash took every uncommitted change out of the tree, theirs included, for about ten seconds. The stash came back cleanly, but the app on our screen was hot-reloading from that folder and showed the product with whole panels missing.
*Cost:* no lost work that time, only luck. A write by another agent during those ten seconds would have made the restore conflict.
*Rule:* never stash, `checkout --` or `reset` in a shared folder; to see the old version use `git show HEAD:path/to/file` ([trick 31](tricks.md)).

**3. The commit that took someone else's work.** Two agents shared a folder and its staging area. One had staged thirty-odd files for its next commit. The other staged its own two files and committed: all of them went in under the second agent's message, and one of the first agent's files was half overwritten, so the commit did not even build.
*Cost:* a commit that had to be split by hand, and a broken build on a branch others were reading.
*Rule:* never `git add -A`; add explicit paths, and refuse to commit when the staging area already holds anything you did not put there ([trick 32](tricks.md)): `[ -z "$(git diff --cached --name-only)" ] || { echo "index not empty"; exit 1; }`.

**4. The live app broke twice in one week.** Both times the folder an agent was editing was the one our app was running from. The first time, the agent added a new component to a file and its import a second later, in two separate writes. The dev server compiled the file in between and the window we were testing in showed a server error. The second time, the agent checked whether a merge would conflict and then merged, chained with `;`: `check && echo ok; merge`. The check failed, the `;` ran the merge anyway, and conflict markers sat in the live files for about a minute.
*Cost:* two error screens in the middle of our own testing, and the trust that goes with them.
*Rule:* write each edit in one pass when a dev server is watching ([trick 34](tricks.md)); chain checks with `&&` or `if check; then act; fi`, never `;` ([trick 30](tricks.md)); do merges in a throwaway worktree and bring over only the result ([trick 33](tricks.md)).

**5. The cleanup that killed the fleet.** A test run got stuck in watch mode. To stop it, an agent ran `pkill -f vitest`. Every long-running background job on the machine was launched with a command line that contained the word `vitest`, so the pattern matched them too: seven data builders and two evaluation runs died with the stuck test.
*Cost:* about 35 minutes of recomputation. It was only that cheap because the builders wrote their results in a way that could safely run twice.
*Rule:* kill processes by a precise pattern (`pkill -f "vitest run"`) or by process ID after looking at `ps` ([trick 38](tricks.md)). And make long jobs safe to re-run, because one day something will kill them.

## When "green" was not green

**6. Three green builds that were red.** All three on the same pull request. First, the build was run as `build 2>&1 | tail -15` to keep the output short; the pipe reported `tail`'s exit code, which is always success, so a failing build looked green. Second, once the build really passed, a missing import was still in the code: the framework's build skips type checking, and says so in one line of its output that nobody reads. Third, in a fresh worktree the build failed with a missing secret, which looked like a code bug and was only a `.env` file that git does not copy.
*Cost:* a pull request reported ready that was not, and an hour chasing a "bug" that was a missing file.
*Rule:* `cmd; echo "EXIT=$?"` instead of a pipe ([trick 43](tricks.md)); run the type checker as its own step ([trick 44](tricks.md)); copy `.env` into a new worktree before judging its build ([trick 35](tricks.md)).

**7. Three hours of old code.** We changed server code, committed it, and ran an evaluation of answer quality. Then another. The development server had not reloaded that server code for three and a half hours, so both rounds measured the old version. A change in a different file had reloaded fine, which made it look like everything was live. A cousin of this one: "I don't see the change" turned out to be a dev server started from a different worktree, serving different code on the same port.
*Cost:* two evaluation rounds thrown away, and conclusions drawn from them in the meantime.
*Rule:* after a server-side change, restart the dev server and confirm once that the new code is live before measuring anything ([trick 46](tricks.md)).

**8. The CI job called "test".** Continuous integration was green on a pull request that had four failing tests. The job named "test" ran the tests of three small packages. The main application's test suite, by far the largest, was not run by any CI job at all. Everyone had assumed it was.
*Cost:* red tests merged behind a green tick.
*Rule:* open the workflow file and read what CI actually runs, including the path filters that decide whether a job runs at all ([trick 47](tricks.md)).

**9. Zero differences.** We compared two large lists of records to find the stale ones. The result, twice: zero stale records. The comparison used a command-line flag that the Linux version of the tool accepts and the macOS version rejects with a usage error. Inside a pipeline the error vanished and the empty output read as "no differences". The real number was several thousand. It was caught only because a second, unrelated count disagreed.
*Cost:* a data refresh that would have been skipped, with a "verified clean" stamp on it.
*Rule:* a suspiciously clean result is probably a dead measurement; check it against a second source, and add one row you know is different so the check has to find it ([trick 48](tricks.md)).

**10. Done on green tests.** On a release night, several fixes were reported done because their tests passed. They had not been opened in a browser. Minutes later we found the bugs by clicking: a selection that did not tick, a menu cut off at the edge, a section shown as inactive.
*Cost:* a release night spent re-opening "done" work.
*Rule:* done means seen working: click the real control or re-ask the real question, report what you saw, and write "not verified live" when you could not ([tricks 41 and 42](tricks.md)). Skill: [`verify`](../skills/verify/SKILL.md).

## When the machine and the data bite back

**11. The machine is part of the system.** One evening the laptop crashed with eight agents, about eight dev servers, a phone simulator and a desktop app running. Three sessions and every agent died, and the reboot wiped the temporary folder where several agents kept their scratch scripts. The work was rebuilt from the session transcripts. A few days later the same laptop overheated in a bag during three hours of travel: a `caffeinate` command, left running for days from an earlier overnight run, kept it from sleeping with the lid closed.
*Cost:* an evening of recovery, and a very hot laptop.
*Rule:* cap how many agents and dev servers run at once, and keep scripts you need again in the repo, not in `/tmp` ([trick 39](tricks.md)). Never start `caffeinate` without a limit: `caffeinate -t 36000` or `caffeinate -w <pid>` ties it to a time or to the job it keeps awake. We now run a small guard every two minutes that, on battery with the lid closed, stops any `caffeinate` and puts the machine to sleep (`pmset sleepnow`).

**12. The column dropped by hand.** A database column was removed with a hand-written migration, meant as a cleanup. The application's schema file, and twenty-odd places in the code, still used it. Production started failing on every request that touched that table until a second migration put the column back.
*Cost:* a production outage, fixed by undoing the cleanup.
*Rule:* the schema change and its migration go in the same commit, migrations are idempotent (`IF EXISTS`, `IF NOT EXISTS`), and no agent ever touches the production database ([tricks 55 and 56](tricks.md)). The rule in our rules file carries this story in one line, which is [trick 25](tricks.md).

## One more, about money

**The cheapest model was the most expensive.** Choosing a model for a bulk extraction job, the cheapest one on the price list was a reasoning model. It billed its thinking as output: several thousand output tokens and about a minute per document, against a few hundred tokens and two seconds for the model we kept. Over the whole job it would have cost more than any other candidate. Another cheap model, at its default settings, sometimes spent its whole budget thinking and returned an empty answer that looked like a success.
*Cost:* nothing, because we measured first on real documents with known right answers.
*Rule:* measure cost per real task, not per token, and check for empty output ([tricks 65 and 66](tricks.md)).

## Write your own

Every team that builds with agents will collect a list like this. The useful habit is the format: what happened, what it cost, the rule. Put the rule in your rules file with the story in one line after it ([trick 25](tricks.md)), and the next agent will respect it without having to meet the incident itself. [templates/AGENTS.md](../templates/AGENTS.md) is a place to start.
