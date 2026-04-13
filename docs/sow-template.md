# Statement of Work — Neural-GTM Sprint
**myAutoBots.AI | Sammy Samet, Principal Technologist**
*Template — customized per engagement*

---

## Parties

| | |
|---|---|
| **Service Provider** | Sammy Samet, operating as myAutoBots.AI |
| **Client** | [Client Company Name] |
| **Effective Date** | [Date of Signature] |
| **Sprint Start Date** | [Within 5 business days of signature] |

---

## 1. Engagement Overview

This SOW governs the delivery of a **Neural-GTM Sprint** — a fixed-scope, fixed-price, 72-hour revenue automation deployment. The engagement combines a GTM stack diagnostic with production deployment of Clay Waterfall enrichment, n8n workflow orchestration, and AI reasoning agents tailored to the client's revenue motion.

All deliverables are production-grade. No proof-of-concepts, no prototypes.

---

## 2. Scope of Work

### Phase 1: Revenue Leakage Diagnostic (Hours 0–8)

| Task | Deliverable |
|---|---|
| GTM stack audit — map all tools, integrations, data flows | Stack topology diagram |
| Identify and quantify all revenue leakage points | Dollar-quantified leak map |
| Define ICP scoring criteria and lead tiering model | ICP scoring rubric |
| Document integration gaps and data quality issues | Gap analysis report |
| Prioritize automation opportunities by ROI | Implementation plan |

### Phase 2: Clay Waterfall Enrichment (Hours 8–24)

| Task | Deliverable |
|---|---|
| Design multi-provider enrichment cascade (6+ providers) | Waterfall architecture doc |
| Configure provider sequence and fallback logic | Deployed Clay Waterfall table |
| Set match-rate thresholds and cost controls | Provider routing config |
| Backfill enrichment on existing CRM records (up to 5,000) | Enriched contact export |
| Validate data quality and coverage rates | Enrichment QA report |

### Phase 3: n8n Workflow Suite (Hours 24–56)

| Workflow | Description |
|---|---|
| Lead Enrichment Trigger | Auto-enriches new leads on CRM entry via Clay Waterfall |
| Intent Scoring Pipeline | Scores leads 0–100 using enrichment data + behavioral signals |
| Lead Routing Engine | Hot (70+) → rep queue; Warm (40–69) → sequence; Cold (<40) → nurture |
| CRM Write-Back | Syncs enrichment, scores, and stage changes to HubSpot/Salesforce |
| HITL Approval Gate | Human review required for high-stakes automated actions |
| Outbound Sequence Trigger | Enrolls scored leads in appropriate sequence by tier and ICP segment |

### Phase 4: AI Reasoning Agent Layer (Hours 56–72)

| Task | Deliverable |
|---|---|
| Deploy RAG-backed lead scoring agent | Scoring agent connected to enriched CRM context |
| Configure multi-agent orchestration (LangGraph) | Agent topology diagram + deployed agents |
| Implement AI governance controls | Audit logging, output validation, escalation routing |
| Deploy personalization generation agent | Personalized email opening lines per scored lead |
| HITL integration for AI outputs | All AI-generated content requires rep approval before send |

---

## 3. Deliverables

| # | Deliverable | Acceptance Criteria |
|---|---|---|
| 1 | Revenue Leakage Report | All leaks quantified in $ · Client sign-off |
| 2 | ICP Scoring Rubric | Min 5 scoring dimensions · Client-approved |
| 3 | Clay Waterfall Config | ≥85% match rate on 100-record test set |
| 4 | n8n Workflow Suite | All 6 workflows live · End-to-end test passed |
| 5 | AI Agent Deployment | Scores returned within 10s · HITL gate active |
| 6 | Architecture Diagrams | All system components documented |
| 7 | Runbook | Step-by-step maintenance guide per workflow |
| 8 | 30-Day Support | Async response within 4 business hours |

---

## 4. Client Responsibilities

Within 24 hours of sprint start, client provides:

- [ ] Read/write API access to CRM (HubSpot or Salesforce)
- [ ] Clay account with API key (or budget ~$149/mo)
- [ ] n8n instance or approval to provision one
- [ ] Access to current outbound email tooling
- [ ] One internal POC available for questions during sprint
- [ ] Completed Discovery Questionnaire

---

## 5. Timeline

```
Day 0       SOW signed · Access credentials received
Hours 0–8   Diagnostic · Leak map delivered
Hours 8–24  Clay Waterfall built and validated
Hours 24–56 n8n workflow suite deployed
Hours 56–72 AI agents deployed · Full system test
Day 4+      30-day support window begins
```

---

## 6. Commercial Terms

| Term | Value |
|---|---|
| Engagement Type | Fixed-scope, fixed-price |
| Payment Schedule | 50% on signature · 50% on delivery acceptance |
| Acceptance Period | 3 business days post-delivery |
| Out-of-Scope Work | Quoted separately at $250/hr |
| IP Ownership | All custom code transfers to client on final payment |
| Confidentiality | Mutual NDA executed prior to credential sharing |

*Pricing provided in separate commercial proposal.*

---

## 7. Assumptions & Exclusions

**In Scope:** Configuration, deployment, testing, 30-day support, architecture docs

**Out of Scope:** Ongoing managed services · Email copywriting · CRM data migration beyond 5K records · Paid tool subscriptions (client's own accounts required)

---

*Questions before signing? [calendly.com/ssam8005/30min](https://calendly.com/ssam8005/30min)*
