# Memory (template)

> One fact per note, one line per note in this index. The agent reads the index every session and opens a note only when it is relevant, so the desk stays clean. You can read, fix and delete every note, unlike a black-box memory.

## Rules (how I want things done)
- [Ask with options](ask-with-options.md): every decision as a short list, recommendation first
- [Verify live](verify-live.md): every UI change checked in a real browser before "done"

## Project (decisions and state)
- [Pricing decision 2026-10](pricing-2026-10.md): flat price, no feature caps; why

## Reference (where things are)
- [Logs](logs.md): how to read production logs

---

Each note looks like this:

```markdown
---
name: verify-live
description: every UI change checked in a real browser before saying done
type: rule
---
Open the changed screen in a browser and click through it before reporting done.
**Why:** tests can pass while the page is broken.
**How to apply:** after any UI change, before the final report.
```
