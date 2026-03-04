# OpenClaw Setup with Claude Max OAuth

## Overview
This guide walks through setting up OpenClaw gateway with Claude Max OAuth authentication instead of API keys. This is the recommended approach for production AI employee deployments.

## Prerequisites

Before starting, ensure you have:
- [ ] VSCode installed with Claude Code extension
- [ ] Claude Code extension signed into Claude Max account
- [ ] OpenClaw project folder open in VSCode
- [ ] Separate terminal window open (not Claude Code's built-in terminal)
- [ ] Telegram app open and bot conversation visible

---

## Step 1: Get the Claude Max OAuth Token (2:30 - 3:30)

### 1.1 Install Claude Code CLI (if not already installed)

```bash
sudo npm install -g @anthropic-ai/claude-code && claude setup-token
```

**Note:** Use `sudo` if the install fails with permissions errors. This installs the Claude Code CLI globally.

### 1.2 Authenticate and Copy Token

1. Browser opens automatically
2. Sign in with your Claude Max account
3. Copy the OAuth token (format: `sk-ant-oat01-...`)

**Critical:** The token must start with `sk-ant-oat01-`. If it starts with `sk-ant-api-`, that's an API key, not a Max token. Do not proceed.

---

## Step 2: Remove Old Auth and Switch to OAuth (3:30 - 5:30)

### 2.1 Nuke All Existing Anthropic Auth

This removes old API key authentication:

```bash
# Delete auth profiles entirely
rm ~/.openclaw/auth-profiles.json

# Remove API key from environment
sed -i '' '/ANTHROPIC_API_KEY/d' ~/.openclaw/.env 2>/dev/null

# Remove env section with API key from config
# (Manual check: Open ~/.openclaw/openclaw.json and remove any "env" section containing ANTHROPIC_API_KEY)
```

**Verify:** Confirm auth-profiles.json is deleted and no API key exists in .env

### 2.2 Verify Config Basics

Ensure your config is at the correct location with correct mode:

```bash
cat ~/.openclaw/openclaw.json | grep -A 5 '"gateway"'
```

**Required:** `gateway.mode` must be `"local"`

### 2.3 Add Claude Max OAuth Clean

```bash
openclaw models auth add
```

**Select:**
1. Provider: `anthropic`
2. Method: `setup-token (claude)`
3. When prompted, paste the `sk-ant-oat01-...` token from Step 1

### 2.4 Verify New Auth

```bash
# Check auth profiles - should have exactly ONE profile with type "token"
cat ~/.openclaw/auth-profiles.json

# Check config auth section
cat ~/.openclaw/openclaw.json | grep -A 10 '"auth"'

# Check model status
openclaw models status
```

**Do NOT restart the gateway yet.**

---

## Step 3: Restart Gateway and Test (5:30 - 7:00)

### 3.1 Restart OpenClaw Gateway

```bash
# Try standard restart first
openclaw gateway restart

# If that fails, use launchd
launchctl kickstart -k gui/$(id -u)/com.openclaw.gateway

# Alternative: Kill and restart manually
pkill -f openclaw; sleep 2; openclaw gateway start
```

**Note:** Use `sudo` if any command fails with permission errors.

### 3.2 Verify Gateway is Running

```bash
# Wait 15 seconds for startup
sleep 15

# Check if gateway responds
curl -s -o /dev/null -w "Gateway: %{http_code}\n" http://localhost:18789

# Check model status
openclaw models status

# Check channels
openclaw channels status --probe

# Check for errors
tail -20 /tmp/openclaw/openclaw.err.log
```

**Success indicators:**
- Gateway returns HTTP 200
- `openclaw models status` shows auth working (no TypeError)
- Telegram channel shows as connected

### 3.3 Send Test Message

1. Open Telegram bot conversation
2. Send a test message
3. Verify bot responds within 15 seconds

**Critical:** Start a NEW conversation thread. Old threads may have stale state.

---

## Step 4: Configure Claude Opus 4.6 as Default Model

### 4.1 Edit OpenClaw Configuration

Edit `~/.openclaw/openclaw.json` and add the following:

```json
{
  "models": {
    "providers": {
      "anthropic": {
        "baseUrl": "https://api.anthropic.com",
        "api": "anthropic-messages",
        "models": [
          {
            "id": "claude-opus-4-6",
            "name": "Claude Opus 4.6",
            "api": "anthropic-messages",
            "reasoning": true,
            "input": ["text", "image"],
            "cost": {
              "input": 5,
              "output": 25,
              "cacheRead": 0.5,
              "cacheWrite": 6.25
            },
            "contextWindow": 200000,
            "maxTokens": 128000
          }
        ]
      }
    }
  },
  "agents": {
    "defaults": {
      "model": {
        "primary": "anthropic/claude-opus-4-6"
      }
    }
  }
}
```

**Critical:** `baseUrl` must be `https://api.anthropic.com` without `/v1` at the end.

### 4.2 Restart and Verify

```bash
openclaw gateway restart
sleep 15
openclaw models status
```

### 4.3 Test Upgraded Model

1. Send another Telegram message
2. Ask something complex to verify the model upgrade
3. Quality difference should be noticeable

---

## Step 5: Fix macOS Sleep Issues (Optional)

If your OpenClaw gateway stops when your Mac sleeps:

### 5.1 Check Launchd Service

```bash
cat ~/Library/LaunchAgents/com.openclaw.gateway.plist | grep -A 5 KeepAlive
```

If no `KeepAlive` section exists, run:

```bash
openclaw gateway install
```

### 5.2 Check Power Management

```bash
pmset -g
```

### 5.3 Check Node.js Version

```bash
node --version
```

If Node.js 22+, add to `~/.openclaw/openclaw.json` under `channels.telegram`:

```json
"network": {
  "autoSelectFamily": false
}
```

### 5.4 Restart After Changes

```bash
openclaw gateway restart
```

---

## Nuclear Reset (Emergency Only)

If everything is broken, do a full nuclear reset:

```bash
# Kill all gateway processes
pkill -f openclaw

# Delete auth profiles
rm -f ~/.openclaw/auth-profiles.json

# Remove API key from environment
sed -i '' '/ANTHROPIC_API_KEY/d' ~/.openclaw/.env 2>/dev/null

# Remove env section from config
# (Manual: Edit ~/.openclaw/openclaw.json and remove "env" section with ANTHROPIC_API_KEY)

# Verify gateway mode
openclaw config get gateway.mode  # Should return "local"

# Re-authenticate
openclaw models auth add
# Select: anthropic → setup-token → paste sk-ant-oat01-... token

# Verify auth
cat ~/.openclaw/auth-profiles.json

# Restart
launchctl kickstart -k gui/$(id -u)/com.openclaw.gateway

# Wait and verify
sleep 15
openclaw channels status --probe
```

---

## Troubleshooting Quick Reference

| Issue | Solution |
|-------|----------|
| Token format wrong | Must be `sk-ant-oat01-...`, not `sk-ant-api-...` |
| Two auth profiles | Redo Step 2.1 to nuke all auth, then re-add |
| TypeError after restart | Check openclaw.json syntax, especially baseUrl |
| Telegram no response | Check error log, start new conversation thread |
| Gateway stops on sleep | Follow Step 5 (macOS sleep fixes) |
| Permission errors | Use `sudo` for pkill, launchctl, and npm install |

---

## Verification Checklist

- [ ] Token copied and verified (sk-ant-oat01- format)
- [ ] Old auth completely removed (no API key anywhere)
- [ ] auth-profiles.json has exactly ONE profile with type "token"
- [ ] gateway.mode is "local" in openclaw.json
- [ ] Gateway restart successful (HTTP 200)
- [ ] openclaw models status shows auth working
- [ ] Telegram bot responds to test message
- [ ] Opus 4.6 configured with correct baseUrl (no /v1)
- [ ] Test message on upgraded model shows quality improvement

---

## Next Steps

Once this setup is complete:
1. Proceed to [Mission Control Setup](mission-control-setup.md)
2. Configure [Recommended Skills](recommended-skills.md)
3. Follow the [Tier 1](tier1-standard.md) or [Tier 2](tier2-pro.md) build guide
