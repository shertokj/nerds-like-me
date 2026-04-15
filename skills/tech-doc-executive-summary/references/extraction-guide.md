# Extraction Guide

Use this reference to map content from technical documents to the 9 executive summary slides.

---

## What to Look For — By Slide

### Slide 2: Business Need
Look for:
- Problem statements, pain points, or "why we're doing this" sections
- Background or context sections
- Business objectives, goals, or OKRs
- Phrases like "current state," "challenges," "gap analysis," "motivation"

Write as: 3–5 bullets explaining the business problem in plain language.
Example: *"Current manual process creates 3–5 day delays in customer onboarding"*

---

### Slide 3: Solution Overview
Look for:
- Executive summary or abstract sections
- "Solution," "Proposed Architecture," or "Overview" sections
- High-level feature lists or capabilities
- App name, platform (web/mobile/API), and primary user group

Write as: 2–3 sentence narrative + 3–5 capability bullets.
Avoid: specific technologies, acronyms without explanation.

---

### Slide 4: System Data Flow
Look for:
- Architecture diagrams (described in text or embedded)
- Integration lists ("integrates with X, Y, Z")
- Database names and their roles
- API endpoints described in flow terms
- ETL or data pipeline descriptions
- Tables or sections titled "Integrations," "Data Sources," "External Systems"

Extract: a list of named systems/services and which ones connect to which.
Format as: `System A → System B (brief label if useful)`

Example nodes: CRM, ERP, Data Warehouse, Customer Portal, Payment Gateway, Email Service, Auth Service

---

### Slide 5: Data Governance & Security
Look for:
- Compliance requirements (HIPAA, SOC 2, GDPR, PCI-DSS, FedRAMP, etc.)
- Data classification (PII, PHI, sensitive, public)
- Access control model (RBAC, ABAC, least privilege)
- Encryption requirements (at rest, in transit)
- Audit logging, data retention, or archival policies
- Data ownership or stewardship definitions

Write as: 4–6 bullets using plain language.
Example: *"Customer PII encrypted at rest using AES-256"*

---

### Slide 6: Infrastructure Summary
Look for:
- Hosting environment (AWS, Azure, GCP, on-prem, hybrid)
- Environments listed (dev, staging, prod)
- Key services used (compute, storage, queuing, CDN, etc.)
- Scalability or availability targets (uptime SLAs, auto-scaling)
- Disaster recovery or backup strategy

Write as: 4–6 bullets. Use vendor names but avoid deep technical specs.
Example: *"Hosted on AWS (us-east-1) with multi-AZ redundancy"*

---

### Slide 7: Costs & Providers
Look for:
- Named vendors, SaaS providers, or cloud services with pricing
- Consultant names, firms, or hourly/project rates
- License costs, subscription tiers, or per-seat pricing
- One-time vs. recurring costs
- Total cost of ownership (TCO) or budget estimates
- Sections titled "Budget," "Cost Estimate," "Vendor," "Procurement"

Build a table with columns: **Provider / Consultant | Type | Cost | Frequency**

If costs are ranges, show the range. If totals can be summed, add a totals row.
Note any costs described qualitatively but without figures (e.g., "TBD," "to be negotiated").

---

### Slide 8: Key Risks & Recommendations
Look for:
- Explicit risk registers or risk sections
- "Assumptions," "Constraints," "Open Issues," "Dependencies" sections
- Anything marked TBD, TBC, or "requires decision"
- Vendor lock-in concerns or single points of failure
- Timeline risks or resource gaps
- Security or compliance gaps noted in the docs

Write as: 3–5 risk bullets, each with a short recommendation.
Format: **Risk:** [description] → **Recommendation:** [action]

---

### Slide 9: Next Steps
Look for:
- Action items, decision gates, or milestone tables
- Sections titled "Next Steps," "Open Items," "Decisions Required"
- Pending approvals or sign-offs needed
- Phases or roadmap entries not yet started

Write as: numbered list of 3–6 concrete actions with owners if named in the docs.

---

## Document Type Hints

### Word (.docx) documents typically contain:
- Narrative descriptions of the problem and solution
- Detailed governance and security requirements
- Cost breakdowns and vendor lists
- Risk registers and assumptions

### PowerPoint (.pptx) documents typically contain:
- Architecture diagrams (inspect slide images if text extraction misses them)
- High-level system overviews
- Integration maps and data flow visuals
- Timeline and roadmap slides

**If a .pptx contains embedded diagrams**, note what systems/services appear as labeled boxes or icons even if arrows aren't text-extractable. The user can confirm if needed.

---

## Tone & Language Rules

| Instead of... | Write... |
|---------------|----------|
| "Microservices architecture" | "Modular app components that scale independently" |
| "ETL pipeline" | "Automated data transfer process" |
| "RBAC" | "Role-based access controls" |
| "AES-256 encryption" | "Industry-standard encryption" |
| "99.9% SLA" | "Less than 9 hours downtime per year" |
| "Kubernetes cluster" | "Auto-scaling cloud infrastructure" |

Always define acronyms on first use if they must appear.
