# Orchestrator-Centered Delivery Flow Diagram

```
                    ┌──────────────────────────────────┐
                    │         CHIEF ORCHESTRATOR        │
                    │         (Central Hub)             │
                    └──────────────┬───────────────────┘
                                   │
          ┌────────────────────────┼────────────────────────┐
          │                        │                        │
          ▼                        ▼                        ▼
   ┌─────────────┐         ┌─────────────┐         ┌─────────────┐
   │  INBOUND    │         │  OUTBOUND   │         │  FEEDBACK   │
   │  CHANNELS   │         │  CHANNELS   │         │  CHANNELS   │
   └─────────────┘         └─────────────┘         └─────────────┘
          │                        │                        │
   ┌──────┴──────┐          ┌──────┴──────┐          ┌──────┴──────┐
   │ From RDAG:  │          │ To TBEP:    │          │ From        │
   │ • Approved  │          │ • Execution │          │ Specialists:│
   │   reqs      │          │   intent    │          │ • Completion│
   │ • Validated │          │             │          │   reports   │
   │   responses │          │ To Agents:  │          │ • Blocker   │
   │             │          │ • Task      │          │   reports   │
   │ From SRL:   │          │   packets   │          │ • Clarif.   │
   │ • Active    │          │             │          │   requests  │
   │   rule ctx  │          │ To WKC:     │          │             │
   │             │          │ • Wiki      │          │ From Review │
   │ From TBEP:  │          │   update    │          │ Agents:     │
   │ • Prepared  │          │   packets   │          │ • Review    │
   │   packets   │          │             │          │   results   │
   │             │          │ To RDAG:    │          │             │
   │ From Wiki:  │          │ • Clarif.   │          │ From WKC:   │
   │ • Current   │          │   routing   │          │ • Update    │
   │   state     │          │ • User      │          │   confirm   │
   └─────────────┘          │   action    │          └─────────────┘
                            │   routing   │
                            └─────────────┘
```

# Agent Discovery Flow

```
CO INITIALIZATION
       │
       ├──► Scan AGENTS/ directory recursively
       │    └──► Read SYSTEM/agent-registry.json
       │         └──► Validate each agent file format
       │              └──► Build built-in capability map
       │
       ├──► Scan custom-agents/ directory recursively
       │    └──► Read SYSTEM/custom-agent-registry.json
       │         └──► Validate each custom agent format
       │              └──► Check for naming conflicts
       │                   └──► Register valid custom agents
       │                        └──► Log invalid agents for review
       │
       └──► Build unified agent selection index
            ├──► Index by domain
            ├──► Index by specialization
            ├──► Index by category
            └──► Index by capability
```

# Custom Agent Discovery and Registration Flow

```
┌─────────────────────────────────────────────────────────┐
│              CUSTOM AGENT DISCOVERY                       │
└─────────────────────────────────────────────────────────┘

  CO scans custom-agents/
       │
       ├──► by-application/
       │    ├── web/        → web-specific custom agents
       │    ├── mobile/     → mobile-specific custom agents
       │    ├── desktop/    → desktop-specific custom agents
       │    ├── saas/       → SaaS-specific custom agents
       │    ├── ecommerce/  → ecommerce-specific custom agents
       │    ├── analytics/  → analytics-specific custom agents
       │    └── enterprise/ → enterprise-specific custom agents
       │
       ├──► by-domain/
       │    ├── payments/   → payment domain custom agents
       │    ├── security/   → security domain custom agents
       │    ├── ai/         → AI domain custom agents
       │    ├── blockchain/ → blockchain domain custom agents
       │    ├── bigdata/    → big data domain custom agents
       │    ├── realtime/   → realtime domain custom agents
       │    ├── mcp/        → MCP domain custom agents
       │    ├── n8n/        → n8n domain custom agents
       │    ├── cli/        → CLI domain custom agents
       │    ├── docker/     → Docker domain custom agents
       │    ├── dashboards/ → dashboard domain custom agents
       │    └── prompting/  → prompting domain custom agents
       │
       ├──► by-client/
       │    ├── client-a/   → client A specific agents
       │    ├── client-b/   → client B specific agents
       │    └── internal/   → internal team agents
       │
       └──► shared/         → common reusable custom agents

  FOR EACH discovered .md file:
       │
       ├──► Validate against required agent format
       │    ├── Has frontmatter (name, description, argument-hint, tools)
       │    ├── Has all required sections (Identity through Forbidden Actions)
       │    └── Follows specialist-only principle
       │
       ├──► Check for naming conflicts with built-in agents
       │    ├── If conflict: log warning, skip registration
       │    └── If no conflict: proceed
       │
       ├──► Register in SYSTEM/custom-agent-registry.json
       │    ├── Record path, category, domain, capabilities
       │    └── Record validation status
       │
       └──► Add to unified agent selection index
```
