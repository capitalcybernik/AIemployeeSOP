# Claude Max + OpenClaw Setup Guide

Step by step guide for setting up OpenClaw with Claude Max OAuth authentication. This is the auth method we use for all AI employee deployments.

## Prerequisites

- Node.js 20+ installed
- Claude Max subscription active
- OpenClaw installed

## Step 1: Install Claude Code CLI

```bash
sudo npm install -g @anthropic-ai/claude-code
```

Use `sudo` if the install fails with permissions errors. This installs the CLI globally so the `claude` command works everywhere.

## Step 2: Get the OAuth Token

```bash
claude setup-token
```

This opens a browser. Sign in with your Claude Max account and copy the `sk-ant-oat01-...` token.

**Important:** The token format is `sk-ant-oat01-...` (OAuth token). If you see `sk-ant-api-...` that's an API key, NOT a Max token. Make sure you have the right one.

## Step 3: Clean Old Auth (If Migrating)

If switching from API key auth to Claude Max OAuth, nuke ALL existing Anthropic auth first:

```bash
# Delete old auth profiles
rm -f ~/.openclaw/auth-profiles.json

# Remove API key from env file
sed -i '/ANTHROPIC_API_KEY/d' ~/.openclaw/.env 2>/dev/null

# Check openclaw.json for any env section with ANTHROPIC_API_KEY and remove it
# Edit ~/.openclaw/openclaw.json manually if needed
```

### Verify cleanup:
- `~/.openclaw/auth-profiles.json` should not exist
- No `ANTHROPIC_API_KEY` in `~/.openclaw/.env`
- No API key references in `~/.openclaw/openclaw.json` env section

## Step 4: Add Claude Max OAuth

```bash
openclaw models auth add
```

When prompted:
1. Select: **anthropic**
2. Select: **setup-token (claude)**
3. Paste the `sk-ant-oat01-...` token when asked

### Verify:
```bash
cat ~/.openclaw/auth-profiles.json
```

Should show exactly ONE anthropic profile with `type: "token"`. If there are two profiles or the type is wrong, delete and redo.

## Step 5: Configure Claude Opus 4.6 (Recommended)

Edit `~/.openclaw/openclaw.json` to set Claude Opus 4.6 as the default model.

Under `models.providers.anthropic`, add:

```json
{
  "baseUrl": "https://api.anthropic.com",
  "api": "anthropic-messages",
  "models": [
    {
      "id": "claude-opus-4-6",
      "name": "Claude Opus 4.6",
      "api": "anthropic-messages",
      "reasoning": true,
      "input": ["text", "image"],
      "cost": { "input": 5, "output": 25, "cacheRead": 0.5, "cacheWrite": 6.25 },
      "contextWindow": 200000,
      "maxTokens": 128000
    }
  ]
}
```

Set the default model:
```json
"agents": {
  "defaults": {
    "model": {
      "primary": "anthropic/claude-opus-4-6"
    }
  }
}
```

**CRITICAL:** `baseUrl` must be `https://api.anthropic.com` with NO `/v1` at the end. Adding `/v1` will break the connection. This is the most common mistake.

## Step 6: Restart Gateway

```bash
openclaw gateway restart
```

If that doesn't work:

**macOS:**
```bash
launchctl kickstart -k gui/$(id -u)/com.openclaw.gateway
```

**Linux:**
```bash
pkill -f openclaw; sleep 2; openclaw gateway start
```

Wait 15 seconds for the gateway to start.

## Step 7: Verify Everything

```bash
# Check gateway is running
curl -s -o /dev/null -w "Gateway: %{http_code}\n" http://localhost:18789

# Check model auth
openclaw models status

# Check channel connections
openclaw channels status --probe

# Check for errors
tail -20 /tmp/openclaw/openclaw.err.log
```

**What to look for:**
- Gateway returns HTTP 200
- `models status` shows auth working, no TypeError
- Channels show connected
- No errors in the log

## Step 8: Test

Send a test message through your configured channel (Telegram, Discord, etc.). The bot should respond within 15 seconds.

**If no response:** Start a NEW conversation thread. Old threads may have stale state.

## Troubleshooting

### Gateway stops after laptop sleep (macOS)

```bash
# Check launchd service
cat ~/Library/LaunchAgents/com.openclaw.gateway.plist

# If no KeepAlive, reinstall
openclaw gateway install

# Check power management
pmset -g
```

### Node.js 22+ with Telegram issues

Add to `~/.openclaw/openclaw.json` under `channels.telegram`:
```json
"network": { "autoSelectFamily": false }
```

### Full Nuclear Reset

If nothing works, do a complete reset:

```bash
# Kill everything
pkill -f openclaw

# Nuke old auth
rm -f ~/.openclaw/auth-profiles.json
sed -i '/ANTHROPIC_API_KEY/d' ~/.openclaw/.env 2>/dev/null

# Verify config
# ~/.openclaw/openclaw.json should have gateway.mode: "local"

# Re-add auth
openclaw models auth add
# Select: anthropic → setup-token → paste token

# Restart
openclaw gateway restart
# Or: launchctl kickstart -k gui/$(id -u)/com.openclaw.gateway

# Wait and verify
sleep 15 && openclaw models status && openclaw channels status --probe
```

## Common Mistakes Checklist

| Mistake | Fix |
|---------|-----|
| `baseUrl` has `/v1` at the end | Remove `/v1`. Must be `https://api.anthropic.com` |
| Token is `sk-ant-api-...` | Wrong token type. Need `sk-ant-oat01-...` (OAuth) |
| Two auth profiles exist | Delete `auth-profiles.json` and re-add with one profile |
| Bot says "I'm using an API key" | Ignore bot self-reporting. Trust `openclaw models status` output |
| Config file is `config.json` | Wrong file. Must be `openclaw.json` |
| TypeError on models status | Config issue. Check JSON syntax in `openclaw.json` |
