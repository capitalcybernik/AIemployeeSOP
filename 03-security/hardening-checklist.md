# Security Hardening Checklist

Every AI Employee deployment MUST complete this checklist before going live.

## Host Security

### Endpoint Protection (Cynet)
- [ ] Cynet agent installed on host system
- [ ] Ransomware protection enabled and verified
- [ ] Encryption protection configured
- [ ] Real time threat monitoring active
- [ ] Automated incident response rules configured
- [ ] Host added to Cynet dashboard for monitoring

### Mobile Security (if applicable)
- [ ] Mobile protection deployed for client access devices
- [ ] Mobile threat detection active
- [ ] Secure access configured for mobile management

### Server Hardening
- [ ] OS updated to latest patches
- [ ] Unnecessary ports closed
- [ ] SSH key based authentication only (no password auth)
- [ ] Firewall configured (only required ports open)
- [ ] Automatic security updates enabled
- [ ] Backup system configured and tested

## AI Security

### Prompt Injection Protection
- [ ] System prompt includes injection defense instructions
- [ ] "Ignore previous instructions" attacks tested and blocked
- [ ] Role play manipulation attempts tested and blocked
- [ ] Social engineering scenarios tested and blocked
- [ ] Indirect injection via user content tested

### Data Guardrails
- [ ] AI cannot access files outside designated workspace
- [ ] AI cannot share internal system information
- [ ] AI cannot process or store credit card numbers
- [ ] AI cannot process or store SSNs or sensitive PII
- [ ] AI cannot reveal pricing, costs, or internal margins
- [ ] Output sanitization active (no code execution, no scripts)

### Identity Anchoring
- [ ] AI identifies itself as an AI assistant in every conversation
- [ ] AI does not pretend to be human when asked
- [ ] AI does not impersonate specific real people
- [ ] AI uses the configured persona name consistently

### Escalation Protocols
- [ ] Escalation contact(s) defined and tested
- [ ] Triggers configured:
  - [ ] Angry/upset customer detection
  - [ ] Billing or payment questions
  - [ ] Legal questions or threats
  - [ ] Requests outside AI's scope
  - [ ] Uncertainty or low confidence responses
  - [ ] Repeated customer frustration
- [ ] Escalation notification method configured (email, SMS, Slack)
- [ ] Escalation tested end to end

### Output Restrictions
- [ ] AI cannot generate executable code
- [ ] AI cannot provide medical, legal, or financial advice
- [ ] AI cannot make commitments or promises on behalf of business
- [ ] AI cannot discuss competitor pricing
- [ ] Custom restrictions per client applied (from discovery call)

## Monitoring

### Ongoing Security Monitoring
- [ ] Conversation logs retained for review
- [ ] Anomaly detection configured (unusual volume, suspicious patterns)
- [ ] Weekly security log review scheduled
- [ ] Cynet dashboard checked during each optimization cycle
- [ ] Incident response plan documented

## Sign Off

| Item | Completed By | Date |
|------|-------------|------|
| Host security | | |
| AI security | | |
| Escalation testing | | |
| Endpoint protection verified | | |
| Final review | | |
