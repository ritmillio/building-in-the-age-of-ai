# Handoff prompt: start fresh without losing the thread

When a chat gets long, it gets worse (context rot). Don't argue with it for twenty more messages. Ask for a handoff, open a new chat, paste it in.

```
Write a handoff so a fresh chat can continue this work without reading this conversation.
Max 15 lines:
1. Goal, in one sentence.
2. Decisions made so far, and why (one line each).
3. What is done, what is not.
4. Open questions, and who decides them.
5. The exact next step.
6. Files, links or numbers the next chat must have.
Leave out everything we tried and dropped, unless the reason matters.
```

In Claude Code the same idea is built in: `/clear` starts fresh, `/compact` summarises the session in place, and the `handoff` skill (see `../skills/third-party.md`) writes this document for you.
