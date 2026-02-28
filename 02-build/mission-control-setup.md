# Mission Control Setup

How to set up the OpenClaw "mission control" workspace for each AI employee deployment.

Mission Control is the core workspace that gives the AI employee its identity, memory, rules, and capabilities. Every deployment starts here.

## Prerequisites

- Linux server or container (Ubuntu 22.04+ recommended)
- Node.js 20+
- OpenClaw installed (`npm install -g openclaw`)
- Cynet agent installed (see security hardening checklist)

## Step 1: Initialize Workspace

```bash
# Create workspace directory
mkdir -p ~/.openclaw/workspace
cd ~/.openclaw/workspace

# Initialize git for version control
git init
```

## Step 2: Create Core Files

Every AI employee needs these 5 files. Use the templates in `/templates/` as starting points.

### SOUL.md (Who they are)
This is the AI employee's personality, values, and behavioral rules.

**Must include:**
- Core behavior rules (always identify as AI, never discuss pricing, etc.)
- Escalation triggers and contacts
- Brand voice guidelines
- Writing rules specific to the client
- Boundaries and restrictions

**Reference:** `templates/soul-template.md`

### IDENTITY.md (Their persona)
The AI employee's name, role, communication style, and introduction scripts.

**Must include:**
- Name and title
- Personality traits
- How they introduce themselves
- How they handle "are you real?" questions
- Topics they handle vs. escalate

**Reference:** `templates/identity-template.md`

### USER.md (Who they serve)
Information about the business owner / primary contact.

**Must include:**
- Owner/contact name
- Business name and details
- Timezone
- Communication preferences
- Key context (industry, service area, etc.)

### AGENTS.md (Operating rules)
System level operating procedures.

**Must include:**
- Memory management rules
- Safety guidelines
- External vs internal action permissions
- Tool usage rules
- Heartbeat/proactive task configuration

### MEMORY.md (Long term memory)
Starts empty. The AI employee populates this over time with important facts, decisions, and learned context about the business.

**Initialize with:**
- Business name and key details
- Service list
- Location/service area
- Any critical facts from discovery call

## Step 3: Install Skills

Based on the client's tier and selected skills:

```bash
# Navigate to skills directory
mkdir -p ~/.openclaw/workspace/skills

# Install skills from ClawHub
clawhub install [skill-name]

# Or manually create skill folders
mkdir -p ~/.openclaw/workspace/skills/[skill-name]
# Add SKILL.md to each folder
```

### Tier 1 Standard: Install up to 5 skills
### Tier 2 Pro: Install all applicable skills

**Security:** Audit every skill before installation using skill-guard:
```bash
clawhub install skill-guard
# Then ask the agent: "Audit the skill at ~/.openclaw/workspace/skills/[name]"
```

## Step 4: Configure TOOLS.md

Add client specific tool configurations:

```markdown
# TOOLS.md

### Client Details
- Business: [Name]
- Website: [URL]
- CRM: [System name + credentials if needed]

### Platform Integration
- [Platform]: [Configuration details]

### API Keys (if applicable)
- [Service]: [Key reference — never store raw keys in git]
```

**Important:** Store sensitive credentials in environment variables or OpenClaw's config, not in TOOLS.md if the repo is shared.

## Step 5: Configure HEARTBEAT.md (Pro Tier)

For Pro tier clients, set up proactive monitoring:

```markdown
# HEARTBEAT.md

## Periodic Checks
- Check for new review requests to send
- Review daily performance metrics
- Check content calendar for scheduled posts
- Monitor escalation queue
```

## Step 6: Connect Platform(s)

### Discord
```bash
openclaw setup discord
# Follow prompts to add bot token
```

### Website Chat (Widget)
- Configure widget embed code
- Add to client's website
- Test in staging first

### SMS (via Twilio or CRM)
- Configure SMS provider credentials
- Set up inbound/outbound routing
- Test with internal number first

### Email
- Configure email provider
- Set up dedicated AI employee email address
- Test send/receive

## Step 7: Configure Gateway

```bash
# Start the OpenClaw gateway
openclaw gateway start

# Verify status
openclaw gateway status
```

Configure `openclaw.json` with:
- Model selection (Tier 1: cost effective, Tier 2: premium)
- Channel connections
- Heartbeat interval (Pro tier)
- Any provider specific settings

## Step 8: Version Control

```bash
# Commit all configuration
git add .
git commit -m "Initial mission control setup for [Client Name]"

# Push to private repo (one repo per client)
git remote add origin https://github.com/capitalcybernik/ai-employee-[client-slug].git
git push -u origin main
```

## Step 9: Verify

Before moving to testing phase:

- [ ] All 5 core files created and reviewed
- [ ] Skills installed and configured
- [ ] Platform integration connected and responding
- [ ] Gateway running and stable
- [ ] Cynet endpoint protection active
- [ ] Git repo initialized and pushed
- [ ] Test conversation successful
- [ ] Escalation flow tested

## Maintenance

### Updating Skills
```bash
clawhub update [skill-name]
# Always audit updates before deploying
```

### Updating Configuration
- Edit files locally
- Test changes
- Commit and push
- Restart gateway if needed: `openclaw gateway restart`

### Monitoring
- Check gateway status: `openclaw gateway status`
- Review logs: check workspace memory files
- Cynet dashboard: verify endpoint health

## Folder Structure (Complete)

```
~/.openclaw/workspace/
├── SOUL.md                  # Personality and rules
├── IDENTITY.md              # Persona and communication
├── USER.md                  # Client/business info
├── AGENTS.md                # Operating procedures
├── MEMORY.md                # Long term memory (grows over time)
├── TOOLS.md                 # Tool configurations
├── HEARTBEAT.md             # Proactive tasks (Pro tier)
├── memory/                  # Daily memory logs
│   └── YYYY-MM-DD.md
├── skills/                  # Installed skills
│   ├── skill-guard/
│   ├── location-pages/
│   ├── blog-content/
│   └── ...
└── docs/                    # OpenClaw documentation
```
