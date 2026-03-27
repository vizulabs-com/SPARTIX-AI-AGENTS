# Folder-by-Folder Explanation

## `.spartix/` — Root
The root directory of the AI operating system specification. Contains all subsystems.

## `AGENTS/` — Built-in Agent Definitions
Contains all official built-in agent definitions organized by category. Each subdirectory represents a domain category. All files are `.md` following the required agent format.

### `00_CONTROL_LAYER/` — Control Layer Agents
The five core control agents: SRL, RDAG, CO, TBEP, WKC. These govern session bootstrap, user communication, orchestration, task preparation, and wiki management.

### `01_EXECUTIVE_LEADERSHIP_AND_GOVERNANCE/` — Executive & Governance
15 agents covering program direction, product ownership, business analysis, architecture, delivery management, governance, risk, and compliance.

### `02_PRODUCT_STRATEGY_AND_PLANNING/` — Product Strategy
14 agents covering product strategy, research, benchmarking, competitive analysis, feature planning, user stories, roadmap, monetization, and validation.

### `03_UX_UI_DESIGN_AND_EXPERIENCE/` — UX/UI Design
18 agents covering UX research, flows, writing, IA, wireframing, prototyping, design systems, visual design, accessibility, and interaction design.

### `04_FRONTEND_WEB_SPECIALISTS/` — Frontend Web
29 agents covering frontend development, architecture, components, state management, performance, security, SSR, PWA, observability, and governance.

### `05_BACKEND_AND_API_SPECIALISTS/` — Backend & API
18 agents covering backend development, architecture, API design, authentication, authorization, workflows, background jobs, caching, and integration.

### `06_DATABASE_AND_DATA_FOUNDATION/` — Database & Data
18 agents covering database architecture, modeling, ERD, migrations, query optimization, indexing, integrity, backup, governance, and warehousing.

### `07_MOBILE_SPECIALISTS/` — Mobile
14 agents covering mobile architecture, development, UI/UX, performance, offline sync, notifications, device integration, and cross-platform.

### `08_DESKTOP_SPECIALISTS/` — Desktop
15 agents covering desktop development, architecture, filesystem, workspace, terminal, packaging, installers, updates, and OS integration.

### `09_AI_LLM_RAG_AND_MULTI_AGENT/` — AI/LLM/RAG
22 agents covering AI architecture, prompt engineering, LLM routing, RAG, embeddings, vector databases, guardrails, multi-agent, and observability.

### `10_QA_TESTING_AND_VALIDATION/` — QA & Testing
19 agents covering test automation, manual QA, regression, unit, integration, E2E, UAT, performance, load, stress, visual regression, and accessibility testing.

### `11_SECURITY_PRIVACY_AND_COMPLIANCE/` — Security & Privacy
17 agents covering security architecture, secure coding, vulnerability scanning, IAM, secrets, compliance, GDPR, audit trails, and threat modeling.

### `12_DEVOPS_INFRASTRUCTURE_AND_CLOUD/` — DevOps & Cloud
18 agents covering DevOps, IaC, CI/CD, deployment, containerization, monitoring, observability, SRE, disaster recovery, and FinOps.

### `13_ENTERPRISE_SAAS_AND_PLATFORM/` — Enterprise SaaS
15 agents covering multi-tenancy, billing, subscriptions, licensing, usage tracking, white-labeling, onboarding, and SLA management.

### `14_DOCUMENTATION_TRAINING_AND_COMMUNICATION/` — Documentation
14 agents covering technical documentation, wiki, release notes, knowledge base, training, onboarding, help center, and API reference.

### `15_MAINTENANCE_SUPPORT_AND_EVOLUTION/` — Maintenance
13 agents covering support, incident triage, hotfixes, refactoring, technical debt, legacy modernization, and root cause analysis.

### `16_BUSINESS_OPERATIONS_AND_MANAGEMENT/` — Business Ops
12 agents covering stakeholder reporting, KPI tracking, ROI analysis, vendor management, change management, and business continuity.

### `17_WEB3_AND_BLOCKCHAIN/` — Web3 & Blockchain
23 agents covering Web3 architecture, smart contracts (Solidity/Rust), tokenomics, wallets, DeFi, NFTs, DAOs, and blockchain infrastructure.

### `18_BIG_DATA_ANALYTICS_AND_DISTRIBUTED_DATA/` — Big Data
20 agents covering big data architecture, data lakes, streaming, batch processing, data quality, lineage, and feature stores.

### `19_REALTIME_SYSTEMS_AND_EVENT_STREAMING/` — Real-time Systems
17 agents covering real-time architecture, event-driven design, Kafka, WebSockets, stream processing, and distributed state.

### `20_MCP_ARCHITECTURE_AND_INTEGRATION/` — MCP
17 agents covering MCP architecture, servers, clients, tools, resources, prompts, security, and multi-server coordination.

### `21_N8N_AUTOMATION_AND_WORKFLOW/` — n8n Automation
16 agents covering n8n workflow architecture, automation building, AI workflows, custom nodes, and workflow governance.

### `22_PAYMENT_GATEWAY_AND_BILLING/` — Payments
14 agents covering payment architecture, gateway integration, PCI compliance, subscriptions, invoicing, fraud detection, and reconciliation.

### `23_ADVANCED_SECURITY_SPECIALISTS/` — Advanced Security
17 agents covering application security, IAM, API security, container security, zero trust, DLP, and incident response.

### `24_CLI_AND_DEVELOPER_TOOLING/` — CLI & Tooling
14 agents covering CLI architecture, UX, parsing, automation, formatting, error handling, and plugin systems.

### `25_DASHBOARD_AND_ANALYTICS_EXPERIENCE/` — Dashboards
14 agents covering dashboard architecture, UX strategy, KPI modeling, visualization, and data integrity.

### `26_AVAILABILITY_PORTS_AND_RUNTIME/` — Availability & Runtime
10 agents covering port availability, service validation, environment conflicts, health checks, and startup diagnostics.

### `27_DOCKER_CONTAINERS_AND_DEPLOYMENT/` — Docker
15 agents covering Docker architecture, Dockerfile optimization, Compose, networking, security hardening, and registry management.

### `28_PROMPT_ENGINEERING/` — Prompt Engineering
13 agents covering prompt architecture, strategy, structure, safety, testing, versioning, and tool invocation design.

### `29_PROMPT_OPTIMIZATION/` — Prompt Optimization
12 agents covering prompt optimization, efficiency, clarity, token reduction, A/B testing, and governance.

### `30_REVIEW_ONLY_SPECIALISTS/` — Review Agents
23 agents providing quality gate reviews across all domains including architecture, code, UX, security, performance, and compliance.

### `31_ENFORCEMENT_AND_GOVERNANCE_SUPPORT/` — Enforcement Agents
18 agents enforcing governance standards across file structure, API contracts, release gates, security policies, and prompt quality.

## `custom-agents/` — Custom Agent Ecosystem
User-defined agents organized by application type, domain, client, and shared. Discovered and validated by CO.

## `SKILLS/` — Built-in Skills
Skill definitions (`.md`) and metadata (`skill-index.json`). Skills are reusable capabilities invoked by agents.

## `custom-skills/` — Custom Skills
User-defined skills following the same format as built-in skills.

## `HOOKS/` — Built-in Hooks
Hook definitions (`.md`) and metadata (`hook-index.json`). Hooks are event-triggered governance mechanisms.

## `custom-hooks/` — Custom Hooks
User-defined hooks following the same format as built-in hooks.

## `RULES/` — Rules Ecosystem
Rules organized by scope: system, user, project, agents, skills, hooks, sessions, overrides. Includes `rule-priority-map.json`.

## `WIKI/` — Project Wiki
Single source of truth. Pages for requirements, decisions, tasks, blockers, milestones, reviews, changelog, and project status.

## `SYSTEM/` — System Documentation
Architecture docs, operating model, dataflow, error prevention, file type policy, agent format template, and JSON registries.

## `DIAGRAMS/` — Diagrams
All system diagrams including architecture, team structure, workflows, dataflows, and governance models.

## `PACKETS/` — Packets & Reports
Packet definitions (`.md`) and schemas (`.json`) for task packets, completion reports, wiki updates, clarification requests, and user action requests.

## `WORKFLOWS/` — Workflow Definitions
Workflow documentation for the main workflow, clarification flow, user action flow, and visibility model.
