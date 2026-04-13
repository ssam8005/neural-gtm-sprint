# Neural-GTM Sprint — System Architecture
**myAutoBots.AI | Full Technical Reference**

---

## 1. End-to-End Data Flow

```mermaid
flowchart TD
    subgraph Sources["📥 Lead Sources"]
        S1[Inbound Web Form]
        S2[Outbound Prospecting]
        S3[CRM Dead Lead Backfill]
        S4[Intent Signal Trigger]
    end

    subgraph Enrichment["🌊 Clay Waterfall Layer"]
        direction LR
        E1[Apollo.io] -->|No match| E2[ZoomInfo]
        E2 -->|No match| E3[Clearbit]
        E3 -->|No match| E4[Hunter.io]
        E4 -->|No match| E5[LinkedIn Sales Nav]
    end

    subgraph Orchestration["⚙️ n8n Orchestration Engine"]
        O1[Enrichment Trigger]
        O2[Intent Scoring Pipeline]
        O3[Routing Engine]
        O4[CRM Write-Back]
        O5[Sequence Enrollment]
        O6[HITL Approval Gate]
    end

    subgraph AI["🧠 AI Agent Layer"]
        A1[RAG Scoring Agent
LangGraph + Pinecone]
        A2[Personalization Agent
Claude + CRM Context]
        A3[Anomaly Detection]
        VDB[(Pinecone
Vector DB)]
        A1 <--> VDB
        A2 <--> VDB
    end

    subgraph CRM["📊 CRM & Activation"]
        C1[HubSpot / Salesforce]
        C2[Rep Queue]
        C3[Email Sequences]
        C4[Deal Creation]
    end

    Sources --> Enrichment --> Orchestration --> AI --> Orchestration --> CRM
```

---

## 2. Multi-Agent Orchestration

```mermaid
graph TD
    Trigger[n8n Orchestrator
Schedule / Webhook]

    Trigger --> EnrichAgent[Enrichment Agent
Clay Waterfall Coordinator]
    EnrichAgent --> ScoringAgent[Lead Scoring Agent
RAG + LangGraph]

    ScoringAgent --> RouterAgent[Routing Agent
Tier Classification]

    RouterAgent --> PersonAgent[Personalization Agent
Claude Code]
    RouterAgent --> SeqAgent[Sequence Agent
Auto-Enroll]
    RouterAgent --> NurtureAgent[Nurture Agent
Long-Cycle Queue]

    PersonAgent --> HITL{HITL Gate
Rep Approval}
    SeqAgent --> HITL
    HITL --> |Approved| CRM[CRM Write-Back]
    HITL --> |Rejected| Rep[Rep Queue]

    AnomalyAgent[Anomaly Detection
Continuous Monitor] --> Slack[Telegram / Slack Alert]

    style HITL fill:#1a2e0a,color:#c8f0a0,stroke:#4a7a2d
    style Trigger fill:#2d1b69,color:#e0e0e0,stroke:#7c3aed
```

---

## 3. RAG Lead Scoring Architecture

```mermaid
flowchart LR
    Lead[Enriched Lead Record] --> Embed[Embedding Model]
    Embed --> Query[Pinecone Query
Top-K Similar Leads]
    Query --> Context[Retrieved Context
Prior deals · objections · patterns]
    Context --> Agent[Claude Code Agent
Scoring + Reasoning]
    Lead --> Agent
    Agent --> Score[Score 0-100
+ Reasoning Memo]
    Score --> CRM[CRM Write-Back]

    subgraph VDB["Pinecone Index"]
        I1[Historical Deal Records]
        I2[ICP Pattern Library]
        I3[Objection Corpus]
        I4[Buyer Journey Signals]
    end

    VDB --> Query
```

---

## 4. HITL Approval Gate

```mermaid
sequenceDiagram
    participant Agent as AI Agent
    participant Gate as HITL Gate (n8n)
    participant Rep as Sales Rep
    participant CRM as CRM

    Agent->>Gate: Staged action (email draft / deal update)
    Gate->>Rep: Notification with preview
    Note over Rep: 4-hour approval window
    alt Approved
        Rep->>Gate: Approve
        Gate->>CRM: Execute action
    else Rejected
        Rep->>Gate: Reject + optional edit
        Gate->>Agent: Feedback signal
        Gate->>CRM: Log rejection for audit
    else Timeout
        Gate->>Rep: Escalation reminder
        Gate->>CRM: Log as pending — no automated action
    end
```

---

## 5. Clay Waterfall Cost Model

```mermaid
flowchart TD
    Lead[ICP Lead] --> T1{Apollo.io
$0.05/match}
    T1 -->|Match 58% hit rate| Done[Enriched
Avg cost: $0.05]
    T1 -->|No Match| T2{ZoomInfo
$0.15/match}
    T2 -->|Match 22% of remaining| Done
    T2 -->|No Match| T3{Clearbit
$0.12/match}
    T3 -->|Match 10% of remaining| Done
    T3 -->|No Match| T4{Hunter.io
$0.08/match}
    T4 -->|Match 5% of remaining| Done
    T4 -->|No Match| Flagged[Deprioritized]

    style Done fill:#0a2e1a,color:#90ee90,stroke:#2d7a4f
    style Flagged fill:#2e0a0a,color:#ffaaaa,stroke:#7a2d2d
```

Weighted avg cost per match: ~$0.08 vs $0.28 single-provider — **97% cost reduction at equal or higher coverage.**

---

## 6. Tech Stack Reference

| Component | Technology | Purpose |
|---|---|---|
| Enrichment | Clay (Waterfall) | Multi-provider cascade |
| Workflow Automation | n8n (50+ workflows) | End-to-end orchestration |
| Agent Framework | LangChain / LangGraph | Multi-agent coordination |
| Vector Database | Pinecone | RAG context retrieval |
| LLM | Claude (Anthropic) | Scoring, personalization, reasoning |
| CRM Integration | HubSpot / Salesforce APIs | Write-back and activation |
| Data Storage | Supabase / Airtable | Agent memory + state |
| HITL Interface | Slack / Telegram | Rep approval notifications |
| Infrastructure | Docker + Linux | Always-on execution |

---

*[Book a free 30-min discovery call](https://calendly.com/ssam8005/30min)*
