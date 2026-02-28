# Tier 1: AI Employee Build Guide ($500/month)

## Overview
- Up to 5 skills
- Single platform deployment
- Standard LLM (cost effective model)
- Full security hardening
- Monthly optimization

## Build Timeline: 2 Weeks

### Week 1: Build

#### Day 1: Environment Setup
- [ ] Provision dedicated server/container for client
- [ ] Install OpenClaw
- [ ] Configure base SOUL.md with client brand voice
- [ ] Configure USER.md with business details
- [ ] Set up AGENTS.md with operational rules
- [ ] Configure IDENTITY.md with AI employee persona

#### Day 2: Skills Configuration
- [ ] Select up to 5 skills from catalog based on discovery call
- [ ] Install and configure each skill
- [ ] Customize skill parameters for client's specific business
- [ ] Set up knowledge base with client FAQs, services, pricing rules

#### Day 3: Security Hardening
- [ ] Complete security hardening checklist (see 03-security/)
- [ ] Configure prompt injection protection
- [ ] Set data guardrails and output restrictions
- [ ] Configure identity anchoring
- [ ] Set up escalation protocols and contacts
- [ ] Define "never do" rules (no pricing discussion, no promises, etc.)
- [ ] Deploy Cynet endpoint protection on host
- [ ] Verify ransomware protection active
- [ ] Configure mobile security if applicable

#### Day 4: Platform Integration
- [ ] Deploy to selected platform (website chat, SMS, email, or Discord)
- [ ] Test integration end to end
- [ ] Verify formatting and appearance on platform
- [ ] Test escalation flow

#### Day 5: Internal Testing
- [ ] Run through 20+ test conversations covering common scenarios
- [ ] Test edge cases (angry customer, off topic, manipulation attempts)
- [ ] Test escalation triggers
- [ ] Verify AI identifies itself as AI
- [ ] Document any issues and fixes

### Week 2: Test and Deploy

#### Days 6 to 8: Client Testing
- [ ] Give client access to private test environment
- [ ] Walk client through test scenarios
- [ ] Collect feedback and adjust
- [ ] Make refinements to personality, tone, knowledge base

#### Days 9 to 10: Go Live
- [ ] Deploy to production platform
- [ ] Monitor first 24 hours closely
- [ ] Address any issues immediately
- [ ] Send "live" confirmation to client
- [ ] Schedule first monthly optimization check in

## LLM Configuration (Tier 1)
- Model: Cost effective tier (e.g., Claude Haiku, GPT 4o mini)
- Usage cap: Standard allocation (monitor monthly)
- Escalate to team if usage exceeds expected volume

## Monthly Optimization
- Review conversation logs for quality
- Identify common questions not handled well
- Update knowledge base as needed
- Check security logs for any incidents
- Send monthly report to client
