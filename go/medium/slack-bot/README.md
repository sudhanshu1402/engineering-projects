# Slack Bot

A placeholder stub for a Go Slack bot. Not implemented yet.

## What this is

Right now `main.go` prints a single line pointing at the library a real
implementation would use (`github.com/slack-go/slack`) and exits. There's no
event handling, no HTTP server, no Slack API calls. A working bot needs a Slack
API token and the actual wiring, neither of which is here.

Treat this as a scaffold I haven't fleshed out, not a finished project.

## Run it

```bash
go run .
```

Output:

```
Slack Bot Stub - Use 'github.com/slack-go/slack'
```

## If you want to build it out

- Add a `go.mod` and pull in `github.com/slack-go/slack`.
- Supply a bot token (`SLACK_BOT_TOKEN`) and, for events, an app token or a
  request endpoint.
- Wire up the client and an event/command handler.

## Files

- `main.go` — the stub described above.
- `.replit` — runs `go run .` on Replit.
