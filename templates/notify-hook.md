# Notify hook: your phone pings when an agent finishes, fails or waits

The setup behind [trick 40](../guides/tricks.md#agents-and-parallel-work). Claude Code runs a small script on three events and the script posts one line to a Telegram chat: which project, which branch, what happened. You stop checking terminals. Checked against the [hooks docs](https://code.claude.com/docs/en/hooks) on 2026-10-21.

## 1. Make a Telegram bot (two minutes)

1. In Telegram, message [@BotFather](https://core.telegram.org/bots/tutorial), send `/newbot`, pick a name. It replies with a token like `123456:ABC...`.
2. Send your new bot any message, then open `https://api.telegram.org/bot<token>/getUpdates` in a browser. The number at `"chat":{"id":` is your chat id.
3. Put both in your shell profile (`~/.zshrc` or `~/.bashrc`), not in any repo:

```bash
export TELEGRAM_BOT_TOKEN="123456:ABC..."
export TELEGRAM_CHAT_ID="987654321"
```

Open a new terminal so Claude Code starts with them.

## 2. The script

Save as `~/.claude/hooks/notify-telegram.sh`, then `chmod +x ~/.claude/hooks/notify-telegram.sh`. It needs `jq` (macOS ships it in `/usr/bin` on recent versions; otherwise `brew install jq` or `apt install jq`).

```bash
#!/bin/bash
# Claude Code hook: send one Telegram message per event. Reads the hook JSON on stdin.
# Needs TELEGRAM_BOT_TOKEN and TELEGRAM_CHAT_ID in the environment Claude Code starts from.
: "${TELEGRAM_BOT_TOKEN:?set TELEGRAM_BOT_TOKEN}" "${TELEGRAM_CHAT_ID:?set TELEGRAM_CHAT_ID}"
input=$(cat)
event=$(jq -r '.hook_event_name' <<<"$input")
dir=$(jq -r '.cwd' <<<"$input")
branch=$(git -C "$dir" branch --show-current 2>/dev/null)
case "$event" in
  Stop)         text="Done: $(jq -r '.last_assistant_message // ""' <<<"$input" | head -c 300)" ;;
  StopFailure)  text="Failed: $(jq -r '.error' <<<"$input")" ;;
  Notification) text="Waiting: $(jq -r '.message' <<<"$input")" ;;
  *)            text="$event" ;;
esac
curl -sS --fail-with-body --max-time 10 -o /dev/null \
  --data-urlencode "chat_id=$TELEGRAM_CHAT_ID" \
  --data-urlencode "text=[$(basename "$dir")${branch:+ @ $branch}] $text" \
  "https://api.telegram.org/bot$TELEGRAM_BOT_TOKEN/sendMessage"
```

Try it before wiring it up. A wrong token prints `curl: (22) ... 401` and a missing one names the variable, so it never fails quietly:

```bash
echo '{"hook_event_name":"Stop","cwd":"'"$PWD"'","last_assistant_message":"Test from my terminal"}' \
  | ~/.claude/hooks/notify-telegram.sh && echo sent
```

## 3. The hooks block

Add this to `~/.claude/settings.json` (every project) or `.claude/settings.json` (one project). If the file already has a `"hooks"` key, merge the three events into it.

```json
{
  "hooks": {
    "Stop": [
      { "hooks": [{ "type": "command", "command": "$HOME/.claude/hooks/notify-telegram.sh", "async": true }] }
    ],
    "StopFailure": [
      { "hooks": [{ "type": "command", "command": "$HOME/.claude/hooks/notify-telegram.sh", "async": true }] }
    ],
    "Notification": [
      { "matcher": "permission_prompt",
        "hooks": [{ "type": "command", "command": "$HOME/.claude/hooks/notify-telegram.sh", "async": true }] }
    ]
  }
}
```

What each one does, per the docs:

- `Stop`: Claude finished its turn. The message carries the start of its last answer (`last_assistant_message`).
- `StopFailure`: the turn ended on an API error (rate limit, overload, billing, auth). The message names the error type.
- `Notification` with `permission_prompt`: Claude is waiting for you to approve something. In a terminal it fires only after you haven't typed for about six seconds, so you get it when you are away, not while you are watching.
- `"async": true` lets Claude keep working while the message goes out; a slow network never holds up the agent.

Run `/hooks` inside Claude Code to see that all three are loaded. A broken script shows up as a `hook error` notice in the session; it never stops the agent.

## When it gets noisy

`Stop` fires at the end of every turn, so in a chat where you go back and forth it pings each answer. Two ways out: keep `Stop` only in the settings of projects where agents run long jobs, or swap it for `Notification` with matcher `idle_prompt`, which fires only when Claude finished about 60 seconds ago and you haven't typed since. Don't add more events (each tool call, each commit): after a day nobody reads them.

Other agents: if your tool can run a command when it finishes, point it at the same script and feed it JSON with `hook_event_name` and `cwd` on stdin.
