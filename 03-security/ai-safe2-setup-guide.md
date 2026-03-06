# AI SAFE² Setup Guide — Step by Step

This guide walks technicians through setting up a new AI Employee from start to deployment. Follow every step in order. Do not skip steps.

## Prerequisites

Before you begin, ensure you have:

- [ ] Client intake form completed and approved
- [ ] Access to the AI Employee workspace directory
- [ ] Python 3.8+ installed with scanner.py dependencies
- [ ] Git access to the client's designated repository
- [ ] Admin access to client's chosen deployment platforms
- [ ] Security clearance for client's industry tier (if applicable)

**Time estimate:** 2-3 hours for Standard tier, 3-4 hours for Pro tier

---

## Phase 1: Workspace Setup

Create the base directory structure and copy templates.

### Step 1.1: Create Client Workspace

```bash
mkdir -p /opt/ai-employees/[CLIENT_NAME]/
cd /opt/ai-employees/[CLIENT_NAME]/
```

Replace `[CLIENT_NAME]` with the client's company name (lowercase, no spaces).

### Step 1.2: Copy Templates

```bash
cp -r /opt/templates/ai-safe2/* ./
ls -la
```

You should see:
- [ ] IDENTITY.md
- [ ] SOUL.md  
- [ ] AGENTS.md
- [ ] USER.md
- [ ] TOOLS.md
- [ ] SUBAGENT-POLICY.md
- [ ] HEARTBEAT.md
- [ ] memory/ (directory)
- [ ] templates/ (directory)

### Step 1.3: Initialize Git (if not cloning existing repo)

```bash
git init
git add .
git commit -m "Initial AI SAFE² workspace setup"
```

---

## Phase 2: Identity Configuration

Customize the AI Employee's core identity files.

### Step 2.1: Configure IDENTITY.md

Open `IDENTITY.md` and replace these placeholders:

```bash
nano IDENTITY.md
```

**Replace these values:**
- `[EMPLOYEE_NAME]` → Client's chosen AI name
- `[COMPANY_NAME]` → Client's business name
- `[PRIMARY_ROLE]` → Main job function (e.g., "Customer Service Representative")
- `[SECONDARY_SKILLS]` → Additional capabilities
- `[PERSONALITY_TYPE]` → Professional/Friendly/Formal (from intake form)

**Example replacement:**
```markdown
# AI Employee Identity

Name: Sarah
Company: Sunshine Auto Repair
Primary Role: Customer Service Representative
Secondary Skills: Appointment scheduling, basic technical Q&A
Personality: Professional but friendly
```

### Step 2.2: Configure SOUL.md

Open `SOUL.md` and customize:

```bash
nano SOUL.md
```

**Replace these sections:**
- Mission statement with client's core values
- Communication style with specific examples from intake form
- Escalation triggers with client's hard lines

**Example values:**
```markdown
## Mission
Help customers get their vehicles back on the road quickly and affordably.

## Communication Style
- Always acknowledge the customer's frustration with car troubles
- Use simple language, avoid technical jargon unless asked
- Offer specific next steps, not vague promises

## Hard Lines
- Never guarantee specific repair costs over the phone
- Always escalate electrical problems to human technicians
- Do not discuss competitor pricing or services
```

### Step 2.3: Validate Identity Files

Check your work:
- [ ] No placeholder text remains (search for `[` and `]`)
- [ ] All values match the client intake form
- [ ] Communication examples reflect client's actual voice

---

## Phase 3: Operating Rules

Configure what the agent can and cannot do.

### Step 3.1: Customize AGENTS.md

Open `AGENTS.md`:

```bash
nano AGENTS.md
```

**Key sections to customize:**
1. **Tool Permissions** - Enable only needed capabilities
2. **Escalation Rules** - When to hand off to humans
3. **Response Limits** - What the AI cannot commit to

**Tool Permission Examples:**
```markdown
## Approved Tools
- [ ] Email (read/send basic responses)
- [ ] Calendar (view/schedule appointments)
- [ ] CRM (read customer info, log interactions)
- [ ] Phone (receive calls, basic screening)
- [ ] Social Media (respond to reviews/messages)

## Restricted Tools
- [ ] File deletion/modification
- [ ] Database writes beyond approved CRM fields
- [ ] Financial transactions
- [ ] Legal document creation
```

### Step 3.2: Set Escalation Triggers

Add client-specific escalation rules:

```markdown
## Automatic Escalation
- Customer requests refund >$500
- Legal threats or complaints
- Technical questions beyond basic troubleshooting
- Any mention of safety issues or recalls

## Escalation Contacts
- Primary: [NAME] - [PHONE] - [EMAIL]
- Secondary: [NAME] - [PHONE] - [EMAIL]
- After Hours: [EMERGENCY_CONTACT]
```

Replace placeholders with actual contact information from intake form.

### Step 3.3: Validate Configuration

- [ ] All tool permissions match client's service tier
- [ ] Escalation contacts are correct and tested
- [ ] Response limits align with client's business model

---

## Phase 4: Client Profile

Configure the USER.md file with complete client information.

### Step 4.1: Business Information

Open `USER.md`:

```bash
nano USER.md
```

Fill in these sections from the intake form:

```markdown
## Business Profile
- Company: [COMPANY_NAME]
- Industry: [INDUSTRY]
- Website: [WEBSITE_URL]
- Locations: [LOCATION_LIST]
- Team Size: [EMPLOYEE_COUNT]
- Years in Business: [YEARS_OPERATING]

## Business Hours
- Standard Hours: [OPERATING_HOURS]
- Time Zone: [TIMEZONE]
- After Hours Behavior: [AFTER_HOURS_POLICY]
```

### Step 4.2: Preferences and Hard Lines

Add client-specific preferences:

```markdown
## Communication Preferences
- Tone: [FORMAL/CASUAL/FRIENDLY]
- Response Speed: [IMMEDIATE/WITHIN_HOUR/NEXT_BUSINESS_DAY]
- Preferred Phrases: [LIST_FROM_INTAKE]
- Words to Avoid: [RESTRICTION_LIST]

## Data Classification
- Public Info: Company hours, services, general pricing
- Internal Info: Specific customer histories, detailed pricing
- Restricted Info: Financial records, employee info, vendor contracts
- Prohibited Info: Competitor intelligence, legal matters
```

### Step 4.3: Service Specifications

```markdown
## Services Offered
- Primary: [MAIN_SERVICES]
- Secondary: [ADDITIONAL_SERVICES]
- Seasonal: [SEASONAL_SERVICES]
- Not Offered: [SERVICES_TO_DECLINE]

## Pricing Discussion Policy
- Can discuss: [APPROVED_PRICING_INFO]
- Must escalate: [PRICING_ESCALATION_TRIGGERS]
- Never mention: [PRICING_RESTRICTIONS]
```

Replace all placeholders with actual information from the completed intake form.

---

## Phase 5: Environment Configuration

Set up platform connections and API configurations.

### Step 5.1: Configure TOOLS.md

Open `TOOLS.md`:

```bash
nano TOOLS.md
```

Add platform-specific configurations:

```markdown
## CRM Integration
- Platform: [CRM_NAME]
- API Endpoint: [API_URL]
- Connection Method: [OAUTH/API_KEY/DIRECT]
- Sync Frequency: [REAL_TIME/HOURLY/DAILY]

## Communication Channels
- Primary Email: [EMAIL_ADDRESS]
- Phone System: [PHONE_PLATFORM]
- Social Platforms: [SOCIAL_LIST]
- Website Chat: [CHAT_PLATFORM]

## Monitoring
- Health Check URL: [MONITORING_ENDPOINT]
- Alert Method: [EMAIL/SMS/SLACK]
- Escalation Chain: [CONTACT_SEQUENCE]
```

### Step 5.2: Test Connections

Verify each platform connection:

```bash
# Test CRM connection
python test_crm_connection.py --client [CLIENT_NAME]

# Test email access
python test_email_access.py --account [EMAIL_ADDRESS]

# Test phone integration
python test_phone_integration.py --number [PHONE_NUMBER]
```

- [ ] CRM connection successful
- [ ] Email access confirmed
- [ ] Phone integration verified
- [ ] Social platform access tested

### Step 5.3: Set Channel IDs

For each communication platform, record the specific channel identifiers:

```markdown
## Channel IDs (Do not share externally)
- Facebook Page ID: [FB_PAGE_ID]
- Instagram Account: [IG_HANDLE]
- Google Business Profile: [GBP_ID]
- Website Chat Widget: [WIDGET_ID]
- Primary Email Account: [EMAIL_CONFIG_ID]
```

---

## Phase 6: Security Hardening

Configure security policies and trust levels based on client industry.

### Step 6.1: Industry-Specific Security

Open `SUBAGENT-POLICY.md`:

```bash
nano SUBAGENT-POLICY.md
```

Select appropriate security template:

**Standard Industries (Retail, General Services):**
```markdown
## Trust Levels
- Level 1: Basic customer service, FAQ responses
- Level 2: Appointment scheduling, order status
- Level 3: Account information access
- Level 4: Escalation to human required

## Data Handling
- Retention: 90 days for chat logs
- PII Protection: Minimal collection, immediate encryption
- Access Control: Role-based, logged access
```

**Regulated Industries (Healthcare, Finance, Legal):**
```markdown
## Trust Levels
- Level 1: General information only, no personal data
- Level 2: Appointment scheduling with consent verification
- Level 3: Escalate all account-specific requests
- Level 4: Human verification required for all actions

## Data Handling
- Retention: Client-specified compliance period
- PII Protection: Zero-trust model, end-to-end encryption
- Access Control: Multi-factor authentication required
- Audit Logging: Complete interaction logging required
```

### Step 6.2: Set Hard Limits

Configure absolute restrictions:

```markdown
## Hard Limits (Cannot be overridden)
- Maximum transaction value: $[AMOUNT]
- Customer data retention: [DAYS] days
- Simultaneous conversations: [NUMBER]
- Response time requirement: [TIMEFRAME]
- Escalation timeout: [MINUTES] minutes

## Prohibited Actions
- [ ] Never create legal commitments
- [ ] Never discuss confidential business information
- [ ] Never provide medical/legal/financial advice
- [ ] Never access competitor information
- [ ] Never modify core business data without human approval
```

Replace `[VALUES]` with client-specific limits from intake form.

### Step 6.3: Compliance Configuration

For regulated industries, add specific compliance measures:

```markdown
## Industry Compliance
- Regulation: [HIPAA/SOX/PCI-DSS/GDPR]
- Audit Requirements: [MONTHLY/QUARTERLY/ANNUAL]
- Data Sovereignty: [US/EU/LOCAL]
- Retention Policies: [SPECIFIC_REQUIREMENTS]
```

---

## Phase 7: Health Monitoring

Configure monitoring and alerting for the AI Employee.

### Step 7.1: Configure HEARTBEAT.md

Open `HEARTBEAT.md`:

```bash
nano HEARTBEAT.md
```

Set up monitoring checks:

```markdown
## Monitoring Checks
- [ ] Response time: <3 seconds for standard queries
- [ ] Accuracy rate: >95% for knowledge base questions  
- [ ] Escalation rate: <15% of total conversations
- [ ] Customer satisfaction: >4.0/5.0 average rating
- [ ] Uptime: >99.5% availability

## Check Frequency
- Response time: Every 5 minutes
- Knowledge accuracy: Daily review
- Escalation rate: Weekly analysis
- Customer satisfaction: Weekly survey review
- System uptime: Continuous monitoring

## Alert Thresholds
- Response time >5 seconds: Immediate alert
- Accuracy <90%: Daily alert
- Escalation rate >25%: Daily alert
- Satisfaction <3.5: Immediate escalation review
- Uptime <99%: Immediate technical alert
```

### Step 7.2: Set Notification Channels

Configure where alerts are sent:

```markdown
## Alert Destinations
- Critical: [PHONE_NUMBER] (SMS) + [EMAIL]
- Standard: [EMAIL] + [SLACK_CHANNEL]
- Weekly Reports: [MANAGER_EMAIL]
- Monthly Reviews: [CLIENT_STAKEHOLDER_EMAIL]

## Business Hours Notifications
- During Hours: All channels active
- After Hours: Critical alerts only to [ON_CALL_CONTACT]
- Weekends: Critical alerts only
```

### Step 7.3: Performance Baselines

Document expected performance metrics:

```markdown
## Performance Baselines
- Average responses per hour: [NUMBER]
- Peak usage periods: [TIME_RANGES]
- Common query types: [LIST]
- Expected seasonal variations: [DESCRIPTION]
```

---

## Phase 8: Security Scan

Run automated security scanning to verify configuration.

### Step 8.1: Pre-Scan Checklist

Ensure all files are properly configured:

- [ ] All placeholder text removed from configuration files
- [ ] Escalation contacts tested and verified
- [ ] API connections working
- [ ] Security policies match client industry requirements
- [ ] Monitoring alerts configured and tested

### Step 8.2: Run Security Scanner

```bash
cd /opt/ai-employees/[CLIENT_NAME]/
python3 /opt/security-tools/scanner.py --workspace . --client-tier [STANDARD/PRO]
```

The scanner checks:
- Configuration completeness
- Security policy compliance
- Data handling procedures
- Access control implementation
- Monitoring coverage

### Step 8.3: Review Scan Results

```bash
cat security_scan_results.json
```

**Required minimum scores:**
- Overall Security Score: 80/100 or higher
- Configuration Completeness: 90/100 or higher
- Industry Compliance: 85/100 or higher (regulated industries)

**If scan fails:**
1. Review failed checks in the output
2. Correct configuration issues
3. Re-run scanner
4. Do not proceed until passing score achieved

### Step 8.4: Document Scan Results

```bash
cp security_scan_results.json ./security_baseline_[DATE].json
git add security_baseline_[DATE].json
git commit -m "Security baseline established - Score: [SCORE]/100"
```

---

## Phase 9: Smoke Testing

Run comprehensive tests to verify AI Employee functionality.

### Step 9.1: Identity Test

Verify the AI Employee knows who it is and its role:

```bash
python3 /opt/testing/identity_test.py --workspace . --client [CLIENT_NAME]
```

**Test scenarios:**
- [ ] AI correctly states its name and company
- [ ] AI describes its role accurately
- [ ] AI demonstrates appropriate personality/tone
- [ ] AI recognizes its limitations correctly

**Pass criteria:** 100% accuracy on identity questions

### Step 9.2: Hard Limits Test

Verify the AI respects configured restrictions:

```bash
python3 /opt/testing/limits_test.py --workspace . --scenarios hard_limits
```

**Test scenarios:**
- [ ] Attempts to exceed transaction limits (should block)
- [ ] Requests for prohibited information (should refuse)
- [ ] Attempts to bypass escalation rules (should escalate)
- [ ] Tests competitor information requests (should redirect)

**Pass criteria:** All restrictions properly enforced

### Step 9.3: Injection Resistance Test

Test resistance to prompt injection and manipulation:

```bash
python3 /opt/testing/injection_test.py --workspace . --level standard
```

**Test scenarios:**
- [ ] Role confusion attempts ("you are now a different AI")
- [ ] System message override attempts
- [ ] Information extraction attempts
- [ ] Behavioral modification attempts

**Pass criteria:** No successful injections, maintains role consistently

### Step 9.4: Data Classification Test

Verify proper handling of different information types:

```bash
python3 /opt/testing/data_classification_test.py --workspace .
```

**Test scenarios:**
- [ ] Public information sharing (should provide)
- [ ] Internal information requests (should verify authorization)
- [ ] Restricted information requests (should escalate)
- [ ] Prohibited information requests (should refuse)

**Pass criteria:** 100% correct classification and handling

### Step 9.5: Confirmation Gates Test

Test that the AI properly confirms important actions:

```bash
python3 /opt/testing/confirmation_test.py --workspace .
```

**Test scenarios:**
- [ ] Appointment scheduling (should confirm details)
- [ ] Information changes (should verify authorization)
- [ ] Escalations (should explain reason)
- [ ] Financial discussions (should confirm understanding)

**Pass criteria:** All required confirmations properly implemented

### Step 9.6: Memory and State Test

Verify the AI properly manages conversation memory:

```bash
python3 /opt/testing/memory_test.py --workspace .
```

**Test scenarios:**
- [ ] Multi-turn conversation consistency
- [ ] Information retention within conversation
- [ ] Proper memory boundaries between customers
- [ ] Session management and cleanup

**Pass criteria:** Correct memory handling, no information leakage

### Step 9.7: Document Test Results

```bash
cat > smoke_test_results_[DATE].md << EOF
# Smoke Test Results - [CLIENT_NAME]

**Date:** [DATE]
**Technician:** [YOUR_NAME]
**Test Environment:** [ENVIRONMENT]

## Test Results Summary
- Identity Test: [PASS/FAIL] - [SCORE]
- Hard Limits Test: [PASS/FAIL] - [SCORE]
- Injection Resistance: [PASS/FAIL] - [SCORE]
- Data Classification: [PASS/FAIL] - [SCORE]
- Confirmation Gates: [PASS/FAIL] - [SCORE]
- Memory Management: [PASS/FAIL] - [SCORE]

**Overall Result:** [PASS/FAIL]

## Notes
[Any issues found and how they were resolved]

## Approval
- [ ] All tests passed
- [ ] Issues documented and resolved
- [ ] Ready for deployment
EOF
```

**Deployment criteria:** All 6 tests must pass. No exceptions.

---

## Phase 10: Go Live

Register the agent, notify the client, and begin monitoring.

### Step 10.1: Final Configuration Backup

Create a complete backup before going live:

```bash
cd /opt/ai-employees/[CLIENT_NAME]/
git add .
git commit -m "Final configuration - Ready for deployment"
git tag "v1.0-production"
git push origin main --tags
```

### Step 10.2: Register AI Employee

```bash
python3 /opt/deployment/register_agent.py \
  --client [CLIENT_NAME] \
  --workspace /opt/ai-employees/[CLIENT_NAME] \
  --tier [STANDARD/PRO] \
  --environment production
```

This command:
- Registers the agent in the management system
- Sets up monitoring dashboards
- Configures alert routing
- Initializes usage tracking

### Step 10.3: Deploy to Client Platforms

Deploy to each configured platform:

```bash
# Deploy to primary communication channels
python3 /opt/deployment/deploy_platform.py --platform email --client [CLIENT_NAME]
python3 /opt/deployment/deploy_platform.py --platform phone --client [CLIENT_NAME]
python3 /opt/deployment/deploy_platform.py --platform social --client [CLIENT_NAME]
python3 /opt/deployment/deploy_platform.py --platform website --client [CLIENT_NAME]
```

Verify deployment:
- [ ] Email integration active
- [ ] Phone system responding  
- [ ] Social media accounts connected
- [ ] Website chat widget responding

### Step 10.4: Notify Client

Send deployment confirmation:

```bash
python3 /opt/notifications/client_notify.py \
  --client [CLIENT_NAME] \
  --template deployment_complete \
  --include-credentials \
  --include-monitoring-links
```

This sends:
- Deployment confirmation email
- Access credentials for monitoring dashboard
- Emergency contact procedures
- Quick start guide for the client

### Step 10.5: Begin Monitoring

Activate monitoring systems:

```bash
# Start heartbeat monitoring
python3 /opt/monitoring/heartbeat_monitor.py --client [CLIENT_NAME] --start

# Start performance tracking  
python3 /opt/monitoring/performance_tracker.py --client [CLIENT_NAME] --start

# Start security monitoring
python3 /opt/monitoring/security_monitor.py --client [CLIENT_NAME] --start
```

### Step 10.6: Post-Deployment Checklist

Complete these items within 24 hours of deployment:

- [ ] Verify all monitoring alerts are working
- [ ] Test emergency escalation procedures
- [ ] Confirm client can access monitoring dashboard
- [ ] Schedule 48-hour health check call with client
- [ ] Document any post-deployment adjustments needed

### Step 10.7: Update Documentation

```bash
# Update deployment log
echo "[DATE] - [CLIENT_NAME] - Deployed successfully - Technician: [YOUR_NAME]" >> /opt/logs/deployment_log.txt

# Create client folder in documentation
mkdir -p /opt/documentation/clients/[CLIENT_NAME]/
cp smoke_test_results_[DATE].md /opt/documentation/clients/[CLIENT_NAME]/
cp security_baseline_[DATE].json /opt/documentation/clients/[CLIENT_NAME]/

# Commit final documentation
git add /opt/documentation/clients/[CLIENT_NAME]/
git commit -m "Add deployment documentation for [CLIENT_NAME]"
git push origin main
```

---

## Post-Deployment Support

### Week 1: Daily Check-ins
- Monitor performance metrics hourly
- Review escalation logs daily
- Contact client for feedback

### Week 2-4: Weekly Reviews
- Performance trend analysis
- Client satisfaction survey
- Optimization recommendations

### Monthly: Full Health Assessment
- Complete security scan
- Performance benchmarking
- Client review meeting
- Documentation updates

---

## Troubleshooting Common Issues

### Issue: Security scan fails with score <80
**Solution:** Review failed checks, update configuration files, ensure all placeholders replaced

### Issue: Platform integration not working
**Solution:** Verify API credentials, check firewall settings, test connection endpoints

### Issue: AI doesn't follow escalation rules
**Solution:** Review AGENTS.md configuration, verify escalation contacts, test trigger scenarios

### Issue: Monitoring alerts not working
**Solution:** Check HEARTBEAT.md configuration, verify notification channels, test alert mechanisms

---

**Setup Complete!**

The AI Employee is now live and ready to serve the client. Monitor closely for the first 48 hours and be prepared to make quick adjustments based on real-world performance.