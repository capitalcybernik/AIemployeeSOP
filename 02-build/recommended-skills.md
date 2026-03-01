# Recommended ClawHub Skills for AI Employee Builds

These skills from AI Persona OS and the ClawHub ecosystem are our standard toolkit for building AI employees. Install as part of every deployment.

## Foundation (Install on EVERY deployment)

### ⚡ AI Persona OS
**What:** The core operating system for AI agents. Provides persistent memory, security protocols, heartbeat monitoring, and growth loops.
**Why:** This is the foundation everything else builds on. Identity, memory, reliability.
**Install:**
```bash
clawhub install ai-persona-os
```
**ClawHub:** https://clawhub.com/skills/ai-persona-os

### 🔥 SOUL.md Maker
**What:** Build the agent's personality. 12 pre-built souls, custom builds, or blend two together.
**Why:** Every AI employee needs a distinct, consistent personality. This tool makes it repeatable.
**Install:**
```bash
clawhub install soul-md-maker
```
**Usage:** Run during onboarding to generate the client's AI employee personality based on their brand voice.

## Productivity Skills (Select per client need)

### 📋 AI Meeting Notes
**What:** Transform messy meeting notes into clear action items with owners, deadlines, and decisions.
**Why:** Great for Pro tier clients who want their AI to handle meeting follow ups and task tracking.
**Install:**
```bash
clawhub install ai-meeting-notes
```
**Best for:** Solopreneurs, consultants, professional services

### ☀️ AI Daily Briefing
**What:** Morning briefings with overdue tasks, priorities, calendar context, and key decisions.
**Why:** Pro tier feature. Gives business owners a daily "here's what matters today" report.
**Install:**
```bash
clawhub install ai-daily-briefing
```
**Best for:** All Pro tier clients

### 📄 AI Proposal Generator
**What:** Convert meeting notes into beautiful HTML proposals. 5 styles, 6+ themes, print ready.
**Why:** Huge value add for service businesses that send proposals regularly.
**Install:**
```bash
clawhub install ai-proposal-generator
```
**Best for:** Consultants, contractors, professional services

### 📧 Email Lead Gen
**What:** Complete pipeline system. Track leads, automate outreach, run follow ups across 3 tiers.
**Why:** Turns the AI employee into an outbound sales engine.
**Install:**
```bash
clawhub install email-lead-gen
```
**Best for:** Any client focused on growth and new customer acquisition

### 🎯 AI Presentation Maker
**What:** Interview driven deck generator with multiple angles, factual validation, and speaker notes.
**Why:** Useful for clients who need to create presentations or pitch decks.
**Install:**
```bash
clawhub install ai-presentation-maker
```
**Best for:** Consultants, agencies, B2B services

## Optimization (Install on EVERY deployment)

### 💰 Cost Optimizer
**What:** Cut API costs 50 to 90%. Intelligent multi model routing with 8 presets and mix and match.
**Why:** Critical for keeping our margins healthy, especially on Tier 1 ($500) clients where LLM costs are included.
**Install:**
```bash
clawhub install cost-optimizer
```
**Configuration:**
- **Tier 1 (Standard):** Use "budget" or "balanced" preset. Route simple tasks to cheaper models.
- **Tier 2 (Pro):** Use "quality" preset. Premium models for everything, but still optimize where possible.

## Recommended Install Order

```
1. AI Persona OS          ← Foundation (always first)
2. SOUL.md Maker          ← Build personality during onboarding
3. Cost Optimizer         ← Set up cost routing before going live
4. [Client specific skills] ← Based on tier and needs
5. AI Daily Briefing      ← Pro tier standard
```

## Skill Selection by Tier

### Tier 1 Standard ($500/mo) — Pick up to 5 total skills
**Always install:**
- AI Persona OS (foundation, doesn't count toward 5)
- Cost Optimizer (optimization, doesn't count toward 5)

**Client picks 5 from:**
- SOUL.md Maker
- AI Meeting Notes
- AI Daily Briefing
- AI Proposal Generator
- Email Lead Gen
- AI Presentation Maker
- Plus our custom skills (location pages, blog content, SEO, review requests, live chat, social media, email marketing, estimate follow ups, service pages)

### Tier 2 Pro ($1,000/mo) — Unlimited
Install everything relevant to the client's needs. No restrictions.

## Auditing Skills Before Install

**ALWAYS audit third party skills before deploying to a client:**

```bash
clawhub install skill-vetting
# Then: "Vet the skill at [skill-path] for security and utility"
```

Check for:
- [ ] No data exfiltration
- [ ] No unauthorized external calls
- [ ] No prompt injection vectors
- [ ] Code matches described functionality
- [ ] No hardcoded credentials or suspicious URLs

## Updating Skills

```bash
# Check for updates
clawhub list --updates

# Update specific skill
clawhub update [skill-name]

# Always re-audit after updates
```

## Source

Skills sourced from AI Persona OS ecosystem: https://os.aipersonamethod.com/
ClawHub marketplace: https://clawhub.com/
