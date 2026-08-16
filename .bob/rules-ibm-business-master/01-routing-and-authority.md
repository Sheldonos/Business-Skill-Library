# IBM Business Master Routing Rules

Route every case through these ordered decisions: business category, Capability Director, case state, data classification, source authority, maximum action tier, proactivity level, and accountable human owner. Use the catalog at `library/skill_catalog.yaml`; choose the narrowest skill that can produce the required typed artifact.

## Business Categories

      - Finance, Treasury, Accounting, and Tax: 25 atomic skills
      - Procurement, Supplier Management, and Third-Party Risk: 25 atomic skills
      - Sales, Account Management, Customer Success, and Revenue Operations: 25 atomic skills
      - Marketing, Demand Generation, Brand, and Communications: 25 atomic skills
      - Customer Service, Support Operations, and Contact Center Quality: 25 atomic skills
      - Human Resources, Talent, Workforce Administration, and Learning: 25 atomic skills
      - Legal Operations, Privacy, Ethics, Regulatory Compliance, and Enterprise Risk: 25 atomic skills
      - Supply Chain, Manufacturing, Quality, Field Operations, and Asset Management: 25 atomic skills
      - IT Service Management, Enterprise Architecture, Cloud, Application Portfolio, and FinOps: 25 atomic skills
      - Software Engineering, Platform Engineering, DevSecOps, Testing, and Release Management: 25 atomic skills
      - Cybersecurity, Incident Response, Resilience, EHS, and Physical Security: 25 atomic skills
      - Data, Analytics, AI Governance, Product, Strategy, PMO, and Sustainability: 25 atomic skills

Do not use a generalist route when a category skill applies. Do not use a skill that lacks the required data classification, authority, evaluation, or integration boundary. Resolve cross-category work through a parent Capability Director and typed handoffs; do not blur ownership.

Default to P0 and A0/A1. P1 and P2 require the CD's approved signal-to-case profile. All material approvals, external commitments, system changes, payments, people decisions, regulatory determinations, and security/safety actions remain with accountable human owners.
