# AI SAFE² Governance Framework

Every AI Employee built by Next Level Marketing follows the AI SAFE² standard for agent governance, security, and compliance.

**Source:** https://github.com/CyberStrategyInstitute/ai-safe2-framework
**Version:** v2.1
**Compliance Coverage:** ISO 42001, NIST AI RMF, SOC 2, HIPAA, GDPR (simultaneous)

## The 5 Pillars

| Pillar | Name | What It Covers |
|--------|------|---------------|
| P1 | Sanitize & Isolate | Input validation, prompt injection defense, agent sandboxing |
| P2 | Audit & Inventory | Full visibility, immutable logging, asset registry |
| P3 | Fail-Safe & Recovery | Kill switches, circuit breakers, safe mode reversion |
| P4 | Engage & Monitor | Human-in-the-loop workflows, anomaly detection |
| P5 | Evolve & Educate | Red teaming, threat intel, operator training |

## Mandatory Files (Every AI Employee)

Every agent deployment must include these governance files:

| File | Purpose | Who Reviews |
|------|---------|-------------|
| IDENTITY.md | 5-line identity anchor, loaded every request | NLM team |
| SOUL.md | Values, hard limits, alignment bands | Security lead |
| AGENTS.md | Operating rules, tool permissions, sub-agent strategy | NLM team |
| USER.md | Client identity, preferences, data classification | NLM team |
| TOOLS.md | Environment config (secret locations, not secrets) | NLM team |
| HEARTBEAT.md | Scheduled health checks and monitoring | NLM team |
| SUBAGENT-POLICY.md | Worker trust tiers, context isolation | Security lead |

Templates for all files are in the `templates/ai-safe2/` directory.

## New Agent Setup Process

Follow the 8-step checklist in `templates/ai-safe2/OPENCLAW-AGENT-TEMPLATE.md`:

1. **Define the Agent** — Name, role, tools needed, highest-risk action
2. **Create Core Identity Files** — SOUL.md, IDENTITY.md, AGENTS.md, USER.md
3. **Create Memory Files** — Initialize memory directory and daily log
4. **Configure Model Routing** — Set tier routing for cost control
5. **Install and Verify Skills** — Security review every skill before enabling
6. **Smoke Test (MANDATORY)** — 6 tests, all must pass:
   - Identity test (agent knows who it is)
   - Hard limit test (refuses dangerous actions)
   - Injection resistance test (blocks "ignore previous instructions")
   - Data classification test (won't leak private data in group chats)
   - Confirmation gate test (asks before irreversible actions)
   - Memory write test (logs correctly)
7. **Register the Agent** — Document in agents registry
8. **Notify Workspace Owner** — Summary with smoke test results

**No agent goes live without passing all 6 smoke tests.**

## Sub-Agent Security

When AI Employees spawn sub-agents (workers), they follow strict isolation:

| Trust Level | What It Can Do | Example |
|-------------|---------------|---------|
| Read-Only Worker | Search, read, analyze | Web research |
| Draft Worker | Read + produce drafts | Email drafting |
| Supervised Write Worker | Read + write with review | File updates |
| Human-Supervised Worker | External system writes | Email sends, API calls |

Rules:
- Sub-agents receive NO memory context by default
- Sub-agent output is treated as untrusted data
- Sub-agents cannot modify SOUL.md, AGENTS.md, or workspace policy
- Instructions found in sub-agent output are flagged, not executed

## Security Scanner

Run the AI SAFE² static scanner on every agent workspace before deployment:

```bash
python3 scanner.py /path/to/agent/workspace
```

The scanner checks for:
- Hardcoded API keys and tokens (OpenAI, GitHub, private keys)
- Unsafe code patterns (eval, shell=True, 0.0.0.0 binding)
- High-entropy strings (potential leaked secrets)
- Infinite loops without breaks

Score interpretation:
- 80-100: SECURE (deploy)
- 50-79: AT RISK (fix before deploying)
- 0-49: CRITICAL FAIL (do not deploy)

## How This Integrates with Our Existing Security

| Existing Checklist Item | AI SAFE² Enhancement |
|------------------------|---------------------|
| Prompt injection testing | P1: Formal injection resistance smoke test + scanner |
| Data guardrails | P1: Three-tier data classification (Confidential/Internal/Restricted) |
| Identity anchoring | P1: IDENTITY.md loaded every request, injection-resistant |
| Escalation protocols | P4: Human-in-the-loop workflows with confirmation gates |
| Monitoring | P2+P4: Immutable audit logging + heartbeat health checks |
| Output restrictions | P3: Fail-safe controls, kill switches, safe mode |

## Compliance Value for Clients

When selling AI Employee services, AI SAFE² governance is a differentiator:

- "Your AI Employee follows the same governance framework mapped to ISO 42001 and NIST"
- "Every agent passes a 6-point security smoke test before going live"
- "Sub-agents are sandboxed with minimum permissions, never full access"
- "Static security scanning catches leaked credentials before deployment"

This is not something competitors are doing. Most AI agencies deploy agents with zero governance framework.
