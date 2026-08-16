# Business Skill Library v2.0

**312 governed skills across 12 enterprise business categories, elevated to production depth.**

Controlled by the [`chief-of-staff`](.bob/skills/chief-of-staff/SKILL.md) orchestration skill.

---

## What This Is

The IBM Business Skill Library is a complete set of atomic, governed IBM Bob skills for enterprise business operations. Every skill:

- Has a **named operator identity** — tells the model exactly who it is and what it replaces
- Contains a **domain model** with 8 explicit reasoning dimensions per business category  
- Lists **operating contexts** so depth and risk posture adapt automatically
- Defines **decision frameworks** with context-sensitive selection criteria
- Enforces an **authority boundary** (A0/A1) and **proactivity level** (P0–P2)
- Produces a **typed output packet** with evidence refs, observations, assumptions, and confidence
- Prevents **11 named anti-patterns** specific to each business category
- Routes via a **handoff table** to adjacent skills and the Chief of Staff
- Includes **11 evaluation cases** that must pass before a skill is considered production-ready

---

## Architecture

```
chief-of-staff                         ← Strategic orchestrator (NEW in v2.0)
  └─ ibm-business-category-router      ← Classifies and routes requests
       └─ Capability Directors (×48)   ← Own case lifecycle per outcome
            └─ Atomic Skills (×300)    ← Execute one bounded procedure each
```

**Foundation Skills (11)** — govern orchestration, evidence, authority, evaluation, and operations  
**Atomic Skills (300)** — one repeatable procedure, one typed artifact, one Capability Director  
**Chief of Staff (1)** — cross-domain synthesis, authority gating, library governance

---

## Business Categories

| Category | Skills | Capability Directors |
|---|---|---|
| Finance, Treasury, Accounting, and Tax | 25 | 6 |
| Procurement, Supplier Management, and Third-Party Risk | 25 | 5 |
| Sales, Account Management, Customer Success, and Revenue Operations | 25 | 6 |
| Marketing, Demand Generation, Brand, and Communications | 25 | 5 |
| Customer Service, Support Operations, and Contact Center Quality | 25 | 6 |
| Human Resources, Talent, Workforce Administration, and Learning | 25 | 5 |
| Legal Operations, Privacy, Ethics, Regulatory Compliance, and Enterprise Risk | 25 | 6 |
| Supply Chain, Manufacturing, Quality, Field Operations, and Asset Management | 25 | 5 |
| IT Service Management, Enterprise Architecture, Cloud, Application Portfolio, and FinOps | 25 | 6 |
| Software Engineering, Platform Engineering, DevSecOps, Testing, and Release Management | 25 | 6 |
| Cybersecurity, Incident Response, Resilience, EHS, and Physical Security | 25 | 6 |
| Data, Analytics, AI Governance, Product, Strategy, PMO, and Sustainability | 25 | 6 |

---

## Installation

### Option A — Install into IBM Bob workspace

```bash
# Copy .bob/ into your project root
cp -rp .bob/ ~/your-project/.bob/

# Or install directly into the global Bob skills directory
cp -rp .bob/skills/* ~/.bob/skills/
```

### Option B — Reference from IBM Capability Mode

Point `custom_modes.yaml` at this library directory and set `ibm-business-master` as your active mode.

```yaml
# Already included in .bob/custom_modes.yaml
```

---

## Usage

### Activate the Chief of Staff

```
Activate chief-of-staff skill. I need to coordinate a vendor contract review 
that involves Finance, Legal, and Procurement.
```

### Route a single-category request

```
Activate ibm-business-category-router. 
I need to classify an AP invoice match exception for a vendor overpayment.
```

### Use an atomic skill directly

```
Activate finance-ap-invoice-match-exception skill.
Case: VENDOR-2024-0892 | Requester: AP Manager | PO: PO-44821 | 
Discrepancy: $12,400 quantity mismatch
```

---

## Benchmark Depth

Every atomic skill was elevated to match the depth of the QisBob education skills and IBM Sales skills:

| Section | QisBob / IBM Sales | This Library (v2.0) |
|---|---|---|
| Operator identity ("You are…") | ✅ | ✅ |
| Domain model with reasoning dimensions | ✅ | ✅ |
| Operating contexts enumeration | ✅ | ✅ |
| Decision frameworks with selection criteria | ✅ | ✅ |
| Step-by-step procedure | ✅ | ✅ |
| Authority and tool boundary | ✅ | ✅ |
| Proactivity level declaration | ✅ | ✅ |
| Typed output contract (YAML) | ✅ | ✅ |
| Anti-patterns (11 named) | ✅ | ✅ |
| Handoff routing table | ✅ | ✅ |
| Evaluation cases (11 cases) | ✅ | ✅ |
| Tool groups | ✅ | ✅ |

---

## Governance Model

| Boundary | Rule |
|---|---|
| **Action tier** | A0 (analyze/retrieve) default; A1 (draft) where declared |
| **Proactivity** | P0 (request-only) default; P1+ requires completed proactivity profile |
| **Human decisions** | Material commitments, approvals, and exceptions always require a named human |
| **Evidence** | Conflicting sources are preserved and surfaced — never silently reconciled |
| **Authority** | A category label, tool availability, or prior success is never authorization to act |

---

## Files

| Path | Purpose |
|---|---|
| `.bob/skills/chief-of-staff/` | Cross-domain orchestrator (new in v2.0) |
| `.bob/skills/ibm-business-category-router/` | Category routing table |
| `.bob/skills/ibm-capability-orchestrator/` | Multi-skill work plan composer |
| `.bob/skills/[category]-[skill]/SKILL.md` | 300 atomic skill files |
| `.bob/custom_modes.yaml` | IBM Business Master and IBM Capability modes |
| `library/skill_catalog.yaml` | Full skill manifest with procedure, output, and guardrail fields |
| `library/capability_directors.yaml` | CD-to-skill mapping |
| `library/coverage_matrix.csv` | Category × skill coverage matrix |
| `agent_specs/` | Capability Director contract schemas |
| `references/` | Architecture documentation and integration registry |
| `scripts/elevate_skills.py` | Generator used to produce v2.0 elevated skills |
| `reports/library_coverage_summary.md` | Coverage metrics |

---

## Version History

| Version | Changes |
|---|---|
| **v2.0.0** | Added Chief of Staff skill; elevated all 300 atomic skills to QisBob/IBM Sales benchmark depth (11 sections per skill: identity, domain model, contexts, frameworks, procedure, boundary, proactivity, output, anti-patterns, handoffs, evaluation) |
| **v1.0.0** | Initial 311-skill library with governance structure (intake contract, output schema, evaluation cases) |

---

## License

IBM Internal — IBM Business Skill Library. See repository governance policy for distribution rights.

---

*Made with IBM Bob*
