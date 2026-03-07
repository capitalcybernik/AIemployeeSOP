# Operating Workflows - Business Process Mapping

**Name:** Operating Workflows  
**Description:** Maps the client's key business processes including lead intake, sales, onboarding, service delivery, support escalation, and billing cycles with steps, responsibilities, tools, SLAs, and bottlenecks identified.

## What This Skill Does

The Operating Workflows skill creates a comprehensive map of how the business actually operates. This includes every major process from lead generation through service delivery to billing and support. For each workflow, it documents the specific steps, who's responsible, what tools are used, service level agreements (SLAs), and common bottlenecks or failure points.

The AI Employee uses this information to understand how the business runs, set appropriate expectations with clients, identify process improvement opportunities, and ensure all communication aligns with actual operational capabilities.

## How to Collect Information

### Discovery Questions for Client

#### Process Identification
1. What are the main workflows that drive your business (lead to cash cycle)?
2. How do leads typically enter your system?
3. What's your sales process from first contact to signed contract?
4. How do you onboard new clients after they sign up?
5. What does your typical service delivery process look like?
6. How do you handle customer support and escalations?
7. What's your billing and collection process?

#### Process Details
1. What are the specific steps in each major workflow?
2. Who is responsible for each step?
3. What tools or systems are used at each stage?
4. How long does each step typically take?
5. Where do processes commonly get stuck or delayed?
6. What triggers the next step in each workflow?

#### Quality & Standards
1. What are your service level agreements (response times, delivery times)?
2. How do you measure success for each process?
3. What are your quality standards or checklists?
4. How do you handle exceptions or special cases?
5. What happens when processes break down?

#### Tools & Systems
1. What CRM or project management tools do you use?
2. How do different systems integrate with each other?
3. Where do you store client information and project files?
4. What communication tools do you use internally and with clients?
5. How do you track and report on process performance?

## How to Structure and Store It

Create a WORKFLOWS.md file mapping all business processes:

```markdown
# Operating Workflows - [Client Name]

**Last Updated:** [Date]
**Process Count:** [Number]

## Workflow Overview

### Core Business Processes
1. **Lead Generation & Intake** - [Brief description]
2. **Sales & Closing** - [Brief description]  
3. **Client Onboarding** - [Brief description]
4. **Service Delivery** - [Brief description]
5. **Support & Account Management** - [Brief description]
6. **Billing & Collections** - [Brief description]

### Key Performance Metrics
- Lead to close rate: [Percentage]
- Average sales cycle: [Days]
- Onboarding completion time: [Days]
- First response SLA: [Hours]
- Project delivery SLA: [Days/Weeks]

---

## Detailed Workflow Maps

### 1. Lead Generation & Intake

#### Process Steps
1. **Lead Capture**
   - **Responsible:** [Person/Role]
   - **Tools:** [Website forms, CRM, etc.]
   - **SLA:** [Response time]
   - **Actions:** [What happens next]

2. **Lead Qualification**
   - **Responsible:** [Person/Role]
   - **Tools:** [Qualification framework, CRM]
   - **SLA:** [Time to qualify]
   - **Criteria:** [What makes a qualified lead]

3. **Lead Assignment**
   - **Responsible:** [Person/Role]
   - **Tools:** [CRM, assignment rules]
   - **SLA:** [Assignment time]
   - **Logic:** [How leads are distributed]

#### Success Metrics
- Form completion rate: [Percentage]
- Qualification rate: [Percentage]
- Time to first response: [Hours]

#### Common Bottlenecks
- [Bottleneck 1 and solution]
- [Bottleneck 2 and solution]

#### Exception Handling
- **High-value leads:** [Special process]
- **Referrals:** [Different handling]
- **Weekend/holiday leads:** [Protocol]

---

### 2. Sales & Closing

#### Process Steps
1. **Discovery Call**
   - **Responsible:** [Salesperson/Role]
   - **Tools:** [Calendar, call script, discovery questions]
   - **SLA:** [Scheduling within X days]
   - **Outcome:** [Qualified opportunity or disqualification]

2. **Proposal Creation**
   - **Responsible:** [Person/Role]
   - **Tools:** [Proposal templates, pricing calculator]
   - **SLA:** [Delivery within X days]
   - **Approval:** [Who reviews before sending]

3. **Follow-up & Negotiation**
   - **Responsible:** [Person/Role]
   - **Tools:** [CRM, email templates]
   - **SLA:** [Follow-up schedule]
   - **Authority:** [Discount/terms approval levels]

4. **Contract & Closing**
   - **Responsible:** [Person/Role]
   - **Tools:** [DocuSign, contract templates]
   - **SLA:** [Contract generation time]
   - **Handoff:** [To delivery team process]

#### Success Metrics
- Discovery to proposal rate: [Percentage]
- Proposal to close rate: [Percentage]
- Average deal size: $[Amount]
- Sales cycle length: [Days]

#### Common Bottlenecks
- [Bottleneck 1 and solution]
- [Bottleneck 2 and solution]

---

### 3. Client Onboarding

#### Process Steps
1. **Welcome & Kickoff**
   - **Responsible:** [Account manager/role]
   - **Tools:** [Welcome packet, onboarding checklist]
   - **SLA:** [Within X hours of signing]
   - **Deliverables:** [Welcome materials, access credentials]

2. **Information Gathering**
   - **Responsible:** [Project team]
   - **Tools:** [Intake forms, strategy questionnaire]
   - **SLA:** [Complete within X days]
   - **Requirements:** [What info is needed]

3. **Account Setup**
   - **Responsible:** [Operations/technical team]
   - **Tools:** [Project management, access portals]
   - **SLA:** [Setup complete within X days]
   - **Testing:** [Quality checks before launch]

#### Success Metrics
- Onboarding completion rate: [Percentage]
- Time to first deliverable: [Days]
- Client satisfaction score: [Rating]

---

### 4. Service Delivery

#### Process Steps
1. **Project Planning**
   - **Responsible:** [Project manager]
   - **Tools:** [Project management software]
   - **SLA:** [Plan delivery within X days]
   - **Approval:** [Client sign-off process]

2. **Work Execution**
   - **Responsible:** [Delivery team]
   - **Tools:** [Collaboration tools, templates]
   - **SLA:** [Milestone delivery schedule]
   - **Quality Control:** [Review process]

3. **Client Review & Feedback**
   - **Responsible:** [Account manager]
   - **Tools:** [Review portal, feedback forms]
   - **SLA:** [Client response time expectations]
   - **Revisions:** [How changes are handled]

4. **Delivery & Handoff**
   - **Responsible:** [Delivery team + account manager]
   - **Tools:** [File sharing, handoff documentation]
   - **SLA:** [Final delivery timeline]
   - **Training:** [How clients are educated on deliverables]

#### Success Metrics
- On-time delivery rate: [Percentage]
- Revision rate: [Average revisions per project]
- Client approval time: [Days]

---

### 5. Support & Account Management

#### Support Tiers
1. **Tier 1: General Questions**
   - **Response SLA:** [Hours]
   - **Resolution SLA:** [Days]
   - **Handled by:** [Role]

2. **Tier 2: Technical Issues**
   - **Response SLA:** [Hours]
   - **Resolution SLA:** [Days]
   - **Handled by:** [Role]

3. **Tier 3: Strategic/Complex**
   - **Response SLA:** [Hours]
   - **Resolution SLA:** [Days]
   - **Handled by:** [Senior role]

#### Escalation Process
1. [When and how to escalate]
2. [Who gets notified]
3. [Timeline for resolution]
4. [Client communication protocol]

---

### 6. Billing & Collections

#### Process Steps
1. **Invoice Generation**
   - **Responsible:** [Billing team/role]
   - **Tools:** [Accounting software]
   - **Schedule:** [When invoices go out]
   - **Approval:** [Who reviews before sending]

2. **Payment Processing**
   - **Responsible:** [Accounts receivable]
   - **Tools:** [Payment processors, banking]
   - **Terms:** [Standard payment terms]
   - **Methods:** [Accepted payment types]

3. **Collections Process**
   - **Day 1 overdue:** [Action taken]
   - **Day 15 overdue:** [Escalation]
   - **Day 30 overdue:** [Further action]
   - **Day 45+ overdue:** [Final steps]

#### Success Metrics
- Days sales outstanding (DSO): [Days]
- Collection rate: [Percentage]
- Payment method adoption: [Breakdown]

---

## Process Integration Points

### System Connections
- **CRM → Project Management:** [How data flows]
- **Project Management → Billing:** [How time/costs transfer]
- **Support → Account Management:** [How issues get elevated]

### Communication Protocols
- **Internal updates:** [How team communicates progress]
- **Client reporting:** [Frequency and format of updates]
- **Emergency communication:** [Who to contact when things go wrong]

### Data & Reporting
- **Performance tracking:** [What metrics are monitored]
- **Reporting schedule:** [When reports are generated]
- **Decision points:** [When processes get reviewed/updated]
```

## How to Use in Daily Operations

### Client Communication
1. Reference workflow timelines when setting expectations
2. Use SLAs to communicate realistic response and delivery times
3. Explain process steps when onboarding new clients
4. Update clients based on where they are in established workflows

### Process Optimization
1. Identify bottlenecks that affect client experience
2. Look for automation opportunities in repetitive steps
3. Monitor SLA performance and adjust as needed
4. Update workflows based on process improvements

### Team Management
1. Use workflows for training new team members
2. Clarify responsibilities and handoff points
3. Set performance expectations based on documented SLAs
4. Identify skill gaps or resource needs

### Problem Resolution
1. Reference standard procedures when issues arise
2. Use escalation paths for complex problems
3. Document exceptions and update processes accordingly
4. Maintain consistent quality through defined workflows

## Example Output

```markdown
# Operating Workflows - Marketing Agency

**Last Updated:** March 7, 2025
**Process Count:** 6

## Workflow Overview

### Core Business Processes
1. **Lead Generation & Intake** - From website form to qualified opportunity
2. **Sales & Closing** - Discovery through signed contract
3. **Client Onboarding** - Welcome through first deliverable
4. **Service Delivery** - Strategy through campaign launch
5. **Support & Account Management** - Ongoing optimization and support
6. **Billing & Collections** - Invoice through payment

### Key Performance Metrics
- Lead to close rate: 23%
- Average sales cycle: 14 days
- Onboarding completion time: 7 days
- First response SLA: 4 hours
- Project delivery SLA: 2-4 weeks

---

## Detailed Workflow Maps

### 1. Lead Generation & Intake

#### Process Steps
1. **Lead Capture**
   - **Responsible:** Marketing Coordinator (automated)
   - **Tools:** HubSpot forms, Zapier automation
   - **SLA:** Immediate form acknowledgment, 4-hour human response
   - **Actions:** Lead data enters HubSpot, Slack notification sent

2. **Lead Qualification**
   - **Responsible:** Business Development Rep
   - **Tools:** BANT qualification framework, HubSpot
   - **SLA:** Qualification within 24 hours
   - **Criteria:** Budget $2K+/month, authority confirmed, need identified

#### Success Metrics
- Form completion rate: 12%
- Qualification rate: 45%
- Time to first response: 2.3 hours average

#### Common Bottlenecks
- Weekend leads sit until Monday (Solution: Weekend checking rotation)
- Incomplete forms require multiple follow-ups (Solution: Progressive profiling)
```

## Success Criteria

1. Complete documentation of all critical business workflows
2. Clear responsibility assignments for each process step
3. Realistic SLAs that match actual performance capabilities
4. Identified bottlenecks with improvement plans
5. Integration points between different systems mapped
6. Exception handling procedures documented
7. Performance metrics established for continuous improvement

This workflow documentation ensures the AI Employee understands how the business actually operates and can set appropriate expectations while identifying opportunities for process optimization.