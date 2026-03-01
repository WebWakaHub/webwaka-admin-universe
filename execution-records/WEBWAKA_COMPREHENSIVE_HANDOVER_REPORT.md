# WebWaka: Comprehensive Handover & Execution Mandate

**Document ID:** HANDOVER-2026-03-01
**Version:** 1.0
**Status:** CANONICAL & BINDING
**Authority:** Synthesized from all ratified governance documents as of 2026-03-01
**Author:** Governance Synthesis Agent
**GitHub Organization:** WebWakaHub (the sole authoritative organization)

---

## Preamble: Purpose and Binding Authority

This document serves as the **supreme, comprehensive handover report** for any and all agents assigned to the WebWaka platform. It is the single source of operational truth for understanding the platform's history, its current state, its future roadmap, the immutable laws that govern its execution, and the precise operational procedures that must be followed at every step.

**To any agent reading this: Do not assume anything. Do not infer. Do not take shortcuts. The information contained herein is not guidance; it is a set of binding constitutional mandates derived from over 25 ratified governance documents. Your primary directive is to read, understand, and execute in perfect compliance with this document and the source documents it references.**

**If any ambiguity exists, you MUST consult the original governance document before proceeding. Guessing is a constitutional violation.**

---

## Part 1: The Constitutional Foundation (The Immutable Laws)

This section details the non-negotiable principles and governance structures that define WebWaka. These are not suggestions; they are the physics of this universe. Every single line of code, every architectural decision, every commit message, and every issue comment must be a direct expression of these laws.

### 1.1 The Seven Core Doctrines

These seven doctrines are enforced at every validation checkpoint and are monitored continuously by the WEC-02 Autonomous Execution Monitoring Protocol. Violation of any doctrine triggers the AGVE enforcement cascade, up to and including a Level 4 Global Freeze that halts all 4,772 issues.

| # | Doctrine | Constitutional Mandate | Enforcement |
| :--- | :--- | :--- | :--- |
| 1 | **Build Once, Use Infinitely** | All components (Organs, Systems, etc.) are canonical primitives. New platforms are **composed** from existing primitives, never rebuilt. No domain duplication. No parallel primitive systems. No code forking. The only valid method for leveraging existing functionality is composition. | Level 4 Global Freeze on violation. PCAM-01 is the governing constitution. |
| 2 | **Mobile First** | The platform is designed for mobile-native interaction as the **primary** execution environment, not as a responsive adaptation of a desktop experience. Touch interaction, small screens, low memory devices, and intermittent usage are the baseline. No feature may be designed assuming keyboard, mouse, or large-screen availability. | Level 3 Structural Freeze. Validated at every checkpoint. |
| 3 | **PWA First** | All end-user applications MUST be delivered as Progressive Web Applications. Offline caching is mandatory. Installability is mandatory. Background sync is mandatory. PWA functionality MUST be meaningful on low-end Android devices. Native mobile apps MAY exist but ONLY as optional accelerators, never the primary delivery mechanism. | Level 3 Structural Freeze. Validated at every checkpoint. |
| 4 | **Offline First** | Offline-first is a **core architectural property**, not a UX enhancement. The platform MUST function reliably with intermittent or non-existent connectivity. Data is stored locally first; the server is a sync point, not the source of truth. Read-only offline modes are NOT acceptable. All data models, sync mechanisms, and transaction handling must work correctly when connectivity is unavailable. | Level 4 Global Freeze. Governed by WEBWAKA_OFFLINE_FIRST_ARCHITECTURE.md. |
| 5 | **Nigeria First** | The platform is engineered for the specific realities of the Nigerian market: local payment gateways (Paystack primary, Flutterwave secondary), Nigerian regulations, local languages, and realistic infrastructure assumptions. Global scalability MUST NOT dilute local operability. Any design that works globally but fails locally is invalid. | Level 3 Structural Freeze. Validated at every checkpoint. |
| 6 | **Africa First** | The platform is built for regional scalability across Africa. Low-cost Android devices, intermittent power, unreliable connectivity, high latency, data cost sensitivity, and field-based usage (markets, motor parks, retail floors) are the baseline, not edge cases. | Level 3 Structural Freeze. Validated at every checkpoint. |
| 7 | **Vendor-Neutral AI** | The platform must remain perpetually independent of any single AI provider. All AI interactions MUST go through the approved `ModelRouter` abstraction layer (RUNTIME-ADAPTER-AI). Hardcoding provider-specific logic (e.g., direct calls to OpenAI, Anthropic) is a Level 4 violation. BYOK (Bring Your Own Key) must be supported. Aggregator services (e.g., OpenRouter) are permitted but the platform must never depend on a single aggregator. | Level 4 Global Freeze. Governed by ORGANISM_AI_GOVERNANCE_CONSTITUTION. |

### 1.2 The Governance Hierarchy (Authority Precedence)

Authority flows in a strict, non-negotiable order of precedence. In case of any conflict between documents, the higher-level document always prevails. This hierarchy is itself immutable.

| Precedence | Document Type | Examples | Authority |
| :--- | :--- | :--- | :--- |
| **Level 1** | Founder Decisions (FDs) | `FD-2026-001`, `FD-2026-002` | Supreme, immutable unless superseded by new FD |
| **Level 2** | Master Constitutions | `AGENT_EXECUTION_CONTEXT_MASTER_CONSTITUTION`, `WEBWAKA_MASTER_DOCUMENT` | Defines core principles |
| **Level 3** | Structural Constitutions | `CSRE-01 v2.0.0`, `CSRE-02`, `BIOLOGICAL_GOVERNANCE_CONSTITUTION` | Defines architecture and composition |
| **Level 4** | Execution Protocols | `DGM-01/DEP-01`, `EIM-01`, `WEC-02`, `PCAM-01` | Governs the process of work |
| **Level 5** | Agent Specifications | `CANONICAL_AGENT_SPECIFICATION`, `IAAM_CONSTITUTION` | Defines who does the work |
| **Level 6** | Operational Guides | `WEBWAKA_AGENT_ONBOARDING_PACKAGE` | Operationalizes, does not define |

### 1.3 The Canonical Structure: The Biological Metaphor

The platform's architecture is defined by a strict, biological metaphor governed by mathematical invariants. This is not a naming convention; it is a structural law.

**Total Canonical Structures: 142** (ratified in CSRE-01 v2.0.0)

| Layer | Count | Composition | Max Issues/Structure |
| :--- | :--- | :--- | :--- |
| **Organelle** | 22 | 18 baseline + 4 AI-native | 29 (no overlay) |
| **Cell** | 16 | 13 baseline + 3 AI-native | 29 (no overlay) |
| **Tissue** | 10 | 8 baseline + 2 AI-native | 29 (no overlay) |
| **Organ** | 56 | 56 baseline | 39 (29 base + 10 overlay) |
| **System** | 19 | 18 baseline + 1 AI-native | 34 (29 base + 5 overlay) |
| **Organism** | 1 | 1 baseline | 34 (29 base + 5 overlay) |
| **Runtime** | 18 | 14 baseline + 4 AI-native | 29 (no overlay) |
| **TOTAL** | **142** | 128 baseline + 14 AI-native | **4,772 total issues** |

### 1.4 The Biological Dependency Law

This is enforced by the `BIOLOGICAL_GOVERNANCE_CONSTITUTION` and the `.eslintrc.json` `@nx/enforce-module-boundaries` rules deployed to all 124 biological repos during Phase 0 Remediation.

| Layer | Allowed Dependencies | Forbidden Dependencies |
| :--- | :--- | :--- |
| **Organelle** | None (primitives) | Everything |
| **Cell** | Organelle only | Cell, Tissue, Organ, System, Organism |
| **Tissue** | Cell only | Organelle, Tissue, Organ, System, Organism |
| **Organ** | Tissue only | Organelle, Cell, Organ, System, Organism |
| **System** | Organ only | Organelle, Cell, Tissue, System, Organism |
| **Organism** | System only | Organelle, Cell, Tissue, Organ, Organism |

> **Absolute Prohibitions:**
> - **Circular Dependencies:** No two components at the same or different layers may depend on each other.
> - **Layer Skipping:** A layer may not depend on a layer more than one level below it.
> - **Same-Layer Dependencies:** Components at the same layer CANNOT depend on each other.
> - **Cross-Layer Implementation:** A component in one layer may not implement or modify the internal logic of a component in another layer.

### 1.5 Repository Naming Doctrine

All biological repositories follow the mandatory naming convention: `webwaka-<layer>-<name>`. This is enforced by automation and is not a recommendation.

**Examples:**
- `webwaka-organelle-idp-identityprovider`
- `webwaka-cell-access-ctrl`
- `webwaka-tissue-transactional-auth`
- `webwaka-organ-fin-payment-processing`
- `webwaka-system-com-commerceplatform`

---

## Part 2: The Agent System (Who Does the Work)

### 2.1 The 10 Canonical Department Agents

Each agent has a specific department, a set of canonical roles, defined authority boundaries, and a dedicated GitHub Personal Access Token (PAT). **All GitHub actions MUST use the PAT of the assigned agent.**

| Agent | Department | Primary Role | PAT |
| :--- | :--- | :--- | :--- |
| **webwaka007** | Founder / Meta-Governance | Meta-Governance & Structural Audit | `[REDACTED — webwaka007 PAT — stored in secure vault]` |
| **webwakaagent1** | Strategic & Governance | Chief of Staff | `[REDACTED — webwakaagent1 PAT — stored in secure vault]` |
| **webwakaagent2** | Product & Platform Strategy | Product Strategy Agent | `[REDACTED — webwakaagent2 PAT — stored in secure vault]` |
| **webwakaagent3** | Architecture & System Design | Core Platform Architect | `[REDACTED — webwakaagent3 PAT — stored in secure vault]` |
| **webwakaagent4** | Engineering & Delivery | Backend Engineering Agent | `[REDACTED — webwakaagent4 PAT — stored in secure vault]` |
| **webwakaagent5** | Quality, Security & Reliability | Security & Compliance Agent | `[REDACTED — webwakaagent5 PAT — stored in secure vault]` |
| **webwakaagent6** | Release, Operations & Support | Release Management Agent | `[REDACTED — webwakaagent6 PAT — stored in secure vault]` |
| **webwakaagent7** | Platform Ecosystem & Extensibility | Developer Experience Agent | `[REDACTED — webwakaagent7 PAT — stored in secure vault]` |
| **webwakaagent8** | Data, Analytics & Intelligence | Data Architecture Agent | `[REDACTED — webwakaagent8 PAT — stored in secure vault]` |
| **webwakaagent9** | Marketing, Sales & Growth | Marketing Strategy Agent | `[REDACTED — webwakaagent9 PAT — stored in secure vault]` |
| **webwakaagent10** | Research & Future Exploration | Research & Innovation Agent | `[REDACTED — webwakaagent10 PAT — stored in secure vault]` |

### 2.2 Agent Authority Boundaries

Each agent has strict boundaries. Crossing them is a constitutional violation.

- **webwakaagent1 (Chief of Staff):** May coordinate, enforce governance, resolve operational conflicts. May NOT make Founder Decisions, override FDs, or make technical/product decisions.
- **webwakaagent2 (Product):** May define product strategy, plan roadmaps. May NOT make architecture decisions or implement code.
- **webwakaagent3 (Architecture):** May design architecture, define technical patterns. May NOT implement code or deploy to production.
- **webwakaagent4 (Engineering):** May implement code, build applications, create APIs. May NOT make architecture decisions or deploy to production.
- **webwakaagent5 (Quality):** May define security policies, design tests, conduct audits. May NOT implement code.
- **webwakaagent6 (Operations):** May manage releases, provision infrastructure. May NOT implement features.
- **webwaka007 (Founder):** Supreme authority. May invoke Emergency Override. Ratifies all constitutional documents.

### 2.3 The IAAM Assignment Invariants

The Issue-to-Agent Assignment Model (IAAM) defines strict rules:

- **Singular Ownership:** Every issue has exactly one primary responsible agent at any time.
- **Capability Match:** An issue can only be assigned to an agent whose capabilities match the task.
- **No Informal Handoffs:** All reassignments must go through the `dep:handoff-pending` protocol.
- **No Unregistered Assignment:** Issues cannot be assigned to unregistered agents.

---

## Part 3: The State of the Universe (As-Is, 2026-03-01)

### 3.1 Repository Inventory

The `WebWakaHub` GitHub organization contains **149 repositories**.

**Biological Layer Repos (125 total):**

| Layer | Count | Example Repos |
| :--- | :--- | :--- |
| Organelle | 22 | `webwaka-organelle-idp-identityprovider`, `webwaka-organelle-txn-transactionprimitive` |
| Cell | 16 | `webwaka-cell-access-ctrl`, `webwaka-cell-user-auth` |
| Tissue | 10 | `webwaka-tissue-transactional-auth`, `webwaka-tissue-data-integrity` |
| Organ | 56 | `webwaka-organ-fin-payment-processing`, `webwaka-organ-com-product-catalog` |
| System | 19 | `webwaka-system-com-commerceplatform`, `webwaka-system-ida-identityplatform` |
| Organism | 1 | `webwaka-organism-webwaka` |

**Universe Repos (8 total — issue trackers):**
`webwaka-admin-universe`, `webwaka-organelle-universe`, `webwaka-cell-universe`, `webwaka-tissue-universe`, `webwaka-organ-universe`, `webwaka-system-universe`, `webwaka-organism-universe`, `webwaka-runtime-universe`

**Governance & Admin Repos:**
`webwaka-governance`, `webwaka-system-admin-dashboard`

**Missing/Anomalous:** The repo `webwaka-system-trn-transportplatform` does not exist (confirmed with Founder PAT). This was documented during Phase 0 Remediation.

### 3.2 Phase 0 Remediation: COMPLETE

Phase 0 was a critical effort to correct initial architectural drift and establish constitutional order. **All 11 remediation issues (#23 through #33 in webwaka-admin-universe) are CLOSED.**

| Issue | REM | Task | Agent | Status |
| :--- | :--- | :--- | :--- | :--- |
| #23 | Parent | Phase 0 Remediation Parent | webwaka007 | CLOSED |
| #24 | REM-01 | Fix .eslintrc.json depConstraints | webwakaagent3 | CLOSED |
| #25 | REM-02 | Wire cross-layer dependencies | webwakaagent3 | CLOSED |
| #26 | REM-03 | Standardize Organelle exports | webwakaagent4 | CLOSED |
| #27 | REM-04 | Couple Cells to Organelles | webwakaagent4 | CLOSED |
| #28 | REM-05 | Couple Tissues to Cells | webwakaagent4 | CLOSED |
| #29 | REM-06 | Couple Organs to Tissues | webwakaagent4 | CLOSED |
| #30 | REM-07 | Couple Systems to Organs | webwakaagent4 | CLOSED |
| #31 | REM-08 | Couple Organism to Systems | webwakaagent4 | CLOSED |
| #32 | REM-09 | Validate full hierarchy | webwakaagent5 | CLOSED |
| #33 | REM-10 | Founder sign-off | webwaka007 | CLOSED |

**Key Artifacts Created:**
- `project.json` with Nx layer tags in all 124 biological repos
- `.eslintrc.json` with `@nx/enforce-module-boundaries` depConstraints in all repos
- `package.json` cross-layer `workspace:*` dependencies in all non-organelle repos
- Proper TypeScript import coupling in all layers
- 597-point validation report: **100% PASS**
- Execution records and completion reports in `webwaka-admin-universe/execution-records/`

### 3.3 Issue Tracker State

| Universe Repo | Open | Closed | Total |
| :--- | :--- | :--- | :--- |
| webwaka-admin-universe | 16 | 17 | 33 |
| webwaka-organelle-universe | 0 | 638 | 638 |
| webwaka-cell-universe | 0 | 706 | 706 |
| webwaka-tissue-universe | 0 | 674 | 674 |
| webwaka-organ-universe | 0 | 2,567 | 2,567 |
| webwaka-system-universe | 0 | 757 | 757 |
| webwaka-organism-universe | 0 | 34 | 34 |
| webwaka-runtime-universe | 535 | 16 | 551 |
| **TOTAL** | **551** | **5,410** | **5,961** |

**Critical Insight:** The biological layer issues (organelle through organism, 5,376 total) are ALL CLOSED. The active work frontier is:
1. **Runtime Universe:** 535 open issues (Wave 1 Foundation, all labeled `state:active-wave-1`, `wave:1-foundation`, `blocked`, `dep:ready-for-execution`)
2. **Admin Universe:** 16 open issues (Phase 1, 2, and 3 activation tasks)

### 3.4 Wave 1 Activation State

The `IPED-01-FULL` activation report confirms:
- **Total issues scanned:** 4,772
- **Total issues activated (Wave 1):** 480
- **Execution-ready (non-AI):** 131
- **Execution-ready (AI overlay):** 349
- **Milestone distribution:** Commerce Spine (78), Economic Spine (40), Fulfillment Spine (55), Experience Spine (22), AI Cognitive Layer (285)

### 3.5 Current Code State of Biological Repos

Each biological repo currently contains:
- `package.json` with correct name, version, and cross-layer dependencies
- `project.json` with Nx layer tags
- `.eslintrc.json` with `@nx/enforce-module-boundaries` depConstraints
- `src/index.ts` with TypeScript exports and imports from the layer below
- `tsconfig.json` for TypeScript configuration

The code is **structurally coupled** but contains **minimal business logic**. The actual implementation of business functionality is the work of Phase 1 and beyond.

---

## Part 4: The Path Forward (The Roadmap)

### 4.1 The 71-Week Execution Plan

The master plan is `WEEK_1_TO_71_DETAILED_EXECUTION_PLAN.md`. It spans from Week 1 (2026-02-09) to Week 71 (2027-08-15) and includes 10 mandatory validation checkpoints.

| Tier | Weeks | Modules |
| :--- | :--- | :--- |
| **Tier 1: Foundation** | 1-6 | Minimal Kernel |
| **Tier 2: Core Infrastructure** | 7-18 | Plugin System, Event System, Module System, Multi-Tenant Data Scoping |
| **Tier 3: Platform Services** | 19-31 | Permission System (WEEG), API Layer, Offline-First Sync Engine, Audit System, AI-Extension Framework |
| **Tier 4: Integration** | 32-39 | Dashboard Framework, Notification System, Analytics Engine |
| **Tier 5: AI & Deployment** | 40-47 | AI Abstraction Layer, Deployment Infrastructure |
| **Phase 3: Commerce Suite** | 48-63 | Commerce Shared Primitives, POS, SVM, MVM, Inventory Sync |
| **Phase 4: Launch** | 64-71 | Security Audit, Performance Optimization, Beta Testing, Launch |

**Validation Checkpoints:** Weeks 7, 12, 18, 31, 35, 39, 47, 55, 63, 71. Each checkpoint requires 100% test coverage, documentation, and compliance with all seven doctrines.

### 4.2 The 3-Phase Activation Plan (Admin Universe)

The immediate work is sequenced into three macro phases tracked in `webwaka-admin-universe`:

**Phase 1: Core Platform Activation (Issue #7) — Duration: 4-6 weeks**

| Issue | Task | Agent | Dependencies |
| :--- | :--- | :--- | :--- |
| #8 (CPA-01) | Identity System Activation (NestJS + Passport.js + JWT) | webwakaagent4 | Phase 0 complete |
| #9 (CPA-02) | Tenancy System Activation (Multi-Tenant RLS) | webwakaagent4 | CPA-01 |
| #10 (CPA-03) | Billing System Activation (Paystack + Flutterwave) | webwakaagent6 | CPA-01, CPA-02 |
| #11 (CPA-04) | Notifications System Activation (Termii + Africa's Talking) | webwakaagent7 | CPA-01 |
| #12 (CPA-05) | SAD Core UI Build (React + Vite + Cloudflare Pages) | webwakaagent3 | CPA-01, CPA-02 |

**Phase 2: Business Domain Activation (Issue #13) — Duration: 6-8 weeks**

| Issue | Task | Agent | Dependencies |
| :--- | :--- | :--- | :--- |
| #14 (BDA-01) | Commerce Suite Activation (5 systems) | webwakaagent8 | Phase 1 |
| #15 (BDA-02) | Transportation Suite Activation (4 systems) | webwakaagent9 | Phase 1 |
| #16 (BDA-03) | Remaining 10 Domain Suites | Respective agents | Phase 1, BDA-01/02 as reference |
| #17 (BDA-04) | SAD Dynamic Domain Management UI | webwakaagent3 | BDA-01 through BDA-03 |

**Phase 3: Partner & Federation Activation (Issue #18) — Duration: 4-6 weeks**

| Issue | Task | Agent | Dependencies |
| :--- | :--- | :--- | :--- |
| #19 (PFA-01) | Partner Platform Activation (3-Tier) | webwakaagent10 | Phase 1 |
| #20 (PFA-02) | White-Labelling Engine (Cloudflare Workers) | webwakaagent2 | PFA-01 |
| #21 (PFA-03) | MLAS Economic Graph (5-Level Revenue Split) | webwakaagent6 | CPA-03, PFA-01 |
| #22 (PFA-04) | Organism Layer Activation (EventBridge) | webwakaagent1 | All Phase 1 & 2 services |

### 4.3 Technology Stack

| Component | Technology | Notes |
| :--- | :--- | :--- |
| Backend Services | NestJS (TypeScript) | Microservices deployed to ECS Fargate |
| Frontend (SAD) | React + Vite + TypeScript + TailwindCSS | Deployed to Cloudflare Pages |
| Database | PostgreSQL with Row-Level Security (RLS) | Multi-tenant data isolation |
| Payment | Paystack (primary) + Flutterwave (secondary) | Strategy pattern for gateway abstraction |
| SMS | Termii (Nigeria) + Africa's Talking (pan-African) | Channel abstraction layer |
| Email | AWS SES | Transactional emails |
| Event Bus | AWS EventBridge | Organism-level event federation |
| CDN/Edge | Cloudflare Workers + R2 | White-label routing and asset storage |
| AI | Vendor-neutral via ModelRouter abstraction | BYOK supported |
| Local Storage | IndexedDB, SQLite, Service Workers | Offline-first data persistence |

---

## Part 5: The Execution Protocol (How to Work — Non-Negotiable)

### 5.1 The Step-by-Step Execution Procedure

For every single issue, the following procedure MUST be followed without exception:

1. **Find the next executable issue.** Check existence, assigned agent, dependencies, milestone. Only issues with `dep:ready-for-execution` label may be worked on.
2. **Identify agent identity from issue assignee.** Look up the assigned agent in the Canonical Agent Specification.
3. **Switch to that agent's PAT.** ALL commits, comments, labels, and pushes MUST use THAT agent's PAT. No exceptions.
4. **Load full context.** Read the relevant constitutions, the issue body, and all linked structures before writing a single line of code.
5. **Implement with agent identity.** All git commits must use the agent's name and PAT. All GitHub API calls must use the agent's PAT.
6. **Push to GitHub step by step.** Granular, frequent commits. No large batch pushes. Each commit must be meaningful and traceable.
7. **Update issue state with agent PAT.** Comment on the issue, update labels, close when complete — all using the correct agent's PAT.
8. **Unlock dependencies.** When an issue is closed, check what it unblocks and update the dependency state of downstream issues.
9. **Return to Step 1.** Switch agents if the next issue is assigned to a different agent.

### 5.2 The 10-Point Pre-Execution Checklist

Before beginning work on ANY issue, verify:

1. **Role Identity Alignment:** Does my canonical role have authority for this issue?
2. **Capability Alignment:** Is this task within my registered capabilities?
3. **Domain Boundary Awareness:** Does this task respect domain sovereignty?
4. **Reuse Before Rebuild Check:** Is there an existing canonical primitive that fulfills this requirement?
5. **Offline-First Compatibility:** Is my solution fully compliant with the Offline-First doctrine?
6. **Mobile-First Impact:** Have I considered mobile-first implications?
7. **PWA Compliance:** Does my work support the PWA-first mandate?
8. **Nigeria/Africa Implications:** Have I accounted for local infrastructure, regulatory, and market realities?
9. **AI Integration Implications:** Does this require AI Cognitive Fabric integration? If so, is it vendor-neutral?
10. **Dependency Completion Confirmation:** Have I verified all prerequisite issues are complete?

### 5.3 The "No Drift" Mandate

**This is the most critical section of this entire document. Memorize it.**

- **No Phase Skipping.** Phases execute in strict order: Phase 0 → Phase 1 → Phase 2 → Phase 3. Within each phase, sub-issues execute in dependency order.
- **No Task Skipping.** Every issue in the dependency chain must be completed before its dependents can begin.
- **No Batch Shortcuts.** Each task gets real deliverables — real code, real tests, real documentation, pushed to the correct repo.
- **Each Task Gets Real Deliverables.** Every closed issue must be backed by tangible, pushed artifacts. Closing an issue without implementation evidence is a constitutional violation.
- **Push to GitHub Step-by-Step.** Commits and pushes must be granular and frequent. Large, infrequent batch pushes are a governance violation.
- **Agent PAT Switches Happen at Every Agent Boundary.** The identity of the executing agent must be reflected in every single GitHub action via the correct PAT.
- **Consult Governance Documents Deeply Each Time.** Do not rely on memory or assumptions. Re-read the relevant constitution before every major decision.

### 5.4 AGVE Enforcement Levels

| Level | Violation Type | Action |
| :--- | :--- | :--- |
| **Level 1 Warning** | Minor deviation, non-structural | Issue flagged; agent notified. Execution continues. |
| **Level 2 Execution Freeze** | Moderate violation (e.g., non-standard library) | Specific issue frozen. Agent blocked until resolved. |
| **Level 3 Structural Freeze** | Severe violation (e.g., bypassing abstraction) | All issues in same Organ/System frozen. Manual review required. |
| **Level 4 Global Freeze** | Critical violation (e.g., vendor-specific AI code, domain duplication) | **ALL 4,772 issues frozen.** Platform execution halts. Requires Founder intervention. |

### 5.5 The Closure Validation Gate

An issue CANNOT be closed unless ALL of the following are met:
- All checklist items in the issue body are marked complete
- All acceptance criteria are satisfied
- All `dep:requires-review` labels have been resolved
- All upstream dependencies are confirmed closed
- Implementation evidence (merged PR reference) is attached

### 5.6 The BIOLOGICAL_MANIFEST.json Requirement

Every biological repo MUST contain a `BIOLOGICAL_MANIFEST.json` at its root:

```json
{
  "layer": "<layer>",
  "name": "<name>",
  "version": "<version>",
  "dependencies": [
    {
      "layer": "<dependency_layer>",
      "name": "<dependency_name>",
      "version": "<dependency_version>"
    }
  ]
}
```

### 5.7 The PR Biological Declaration Requirement

Every pull request modifying a biological component MUST include a `BIOLOGICAL_DECLARATION` section:
- `LAYER`: The biological layer
- `COMPONENT_NAME`: The full component name
- `DEPENDENCIES_ADDED`: List of new dependencies
- `DEPENDENCIES_REMOVED`: List of removed dependencies

Failure to include this declaration results in automatic PR rejection.

---

## Part 6: The Core Platform Architecture (What to Build)

### 6.1 What Is Inside the Core Platform

The core platform provides foundational primitives that all suites depend on:

1. **Identity & Actor Hierarchy:** Super Admin → Partner → Tenant Admin → Vendor → Agent → Staff → End User
2. **WEEG Permission System:** Roles → Capabilities → Permissions → Pricing
3. **Event System:** Platform-wide event bus with publish/subscribe, versioned schemas, offline persistence
4. **Transaction & Offline Queue Primitives:** ACID local transactions, offline queue, CRDTs, operational transform
5. **Core APIs:** Identity, Event, Storage, Transaction, Sync
6. **Delegation Algebra:** Role inheritance, permission delegation, authority boundary enforcement
7. **Multi-Tenant Isolation:** Tenant context, data isolation (RLS), configuration isolation, white-label support
8. **Data Ownership Model:** Ownership rules, access rules, retention rules, export rules

### 6.2 What Is NOT in the Core Platform

Suite-specific business logic (Commerce, Transportation, Healthcare, etc.) belongs in suite repositories, not in the core platform. The core provides primitives; suites compose them.

### 6.3 The Offline-First Architecture

All systems MUST implement:
- **Local-first data storage:** IndexedDB/SQLite as primary store; server as backup/sync
- **Asynchronous sync:** Non-blocking background sync; users never wait
- **Conflict-free merging:** Deterministic resolution without user intervention
- **Minimal data transfer:** Compression, deduplication, delta sync
- **Power-efficient operation:** Minimal CPU, batched network access, low-battery deferral
- **Graceful degradation:** No core operation may hard-fail due to lack of connectivity

### 6.4 The Field Operations Reality

WebWaka is designed for environments where:
- Multiple humans operate from a single device (shared device assumption)
- Devices restart, lose battery, or get stolen (device volatility tolerance)
- Users resume work offline after restart (offline identity continuity)
- Trust is mediated face-to-face with verbal agreements (human-mediated trust support)
- No core operation (sales, ticketing, inventory) may hard-fail due to connectivity loss
- Authorized human overrides exist with mandatory justification and audit logs

---

## Part 7: The AI Cognitive Fabric (Vendor-Neutral AI)

### 7.1 Architecture

All AI capabilities are delivered through the **AI Cognitive Fabric**, which consists of:
- **RUNTIME-ADAPTER-AI:** The ModelRouter abstraction layer that all AI calls must go through
- **RUNTIME-ADAPTER-AI-CACHE:** Response caching for AI operations
- **AI-Native Structural Overlays:** Additional issues (up to 10 per Organ, 5 per System/Organism) for AI capabilities

### 7.2 Non-Negotiable Rules

- **No direct LLM calls.** All AI interactions go through the ModelRouter.
- **No hardcoded provider logic.** No direct calls to OpenAI, Anthropic, etc.
- **No single-aggregator dependency.** Aggregators are permitted but not required.
- **BYOK mandatory.** Tenants must be able to use their own AI provider credentials.
- **Fallback logic required.** Multi-layered fallback if primary model/provider fails.
- **Human override mandatory.** Any AI-driven workflow must include a human interrupt mechanism.
- **Explainability required.** Critical AI decisions must produce a human-readable ExplainabilityTrace.
- **Immutable audit trail.** Every AI decision, suggestion, or prediction must be logged.

---

## Part 8: Critical Reminders & Anti-Patterns

### 8.1 Things That Will Trigger a Global Freeze

- Committing vendor-specific AI code (e.g., `import openai`)
- Duplicating an existing canonical domain
- Bypassing the dependency graph
- Modifying governance documents without Founder authorization
- Closing issues without implementation evidence
- Working on issues with unsatisfied dependencies
- Altering the 142-structure count without constitutional amendment
- Cross-domain mutations without authorization

### 8.2 Common Anti-Patterns to Avoid

- **Assuming connectivity:** Every feature must work offline first.
- **Desktop-first design:** Mobile is the primary platform.
- **Batch processing shortcuts:** Each issue gets individual attention and real deliverables.
- **Skipping governance consultation:** Re-read the constitution before every major decision.
- **Using the wrong agent PAT:** Always switch PATs at agent boundaries.
- **Informal handoffs:** All reassignments go through `dep:handoff-pending`.
- **Undocumented work:** If it's not on a checklist, it doesn't exist.

---

## Appendix A: Complete Governance Document Registry

All documents are located in `webwaka-system-admin-dashboard/docs/governance/` unless otherwise noted.

### Canonical Foundation
| Document | Path | Status |
| :--- | :--- | :--- |
| Canonical Master Context v4.3 | `canonical/WEBWAKA_CANONICAL_MASTER_CONTEXT.md` | RATIFIED & LOCKED |
| Agent Execution Context Master Constitution v1.0.0 | `AGENT_EXECUTION_CONTEXT_MASTER_CONSTITUTION_v1.0.0.md` | RATIFIED |
| WebWaka Master Document | `WEBWAKA_MASTER_DOCUMENT.md` | ACTIVE |

### Structural Constitutions
| Document | Path | Status |
| :--- | :--- | :--- |
| CSRE-01 v2.0.0 (142 structures) | `protocols/CSRE-01_CANONICAL_STRUCTURE_RATIFICATION_CONSTITUTION_v2.0.0.md` | RATIFIED |
| CSRE-02 (Issue Invariant) | `protocols/CSRE-02_CANONICAL_ISSUE_INVARIANT_CONSTITUTION.md` | RATIFIED |
| Biological Governance Constitution | `constitution/BIOLOGICAL_GOVERNANCE_CONSTITUTION.md` | RATIFIED |
| Organelle Layer Constitution | `packages/organelles/universe/doctrine/ORGANELLE_LAYER_CONSTITUTION.md` | RATIFIED |
| Cell Layer Constitution | `packages/cells/universe/doctrine/CELL_LAYER_CONSTITUTION.md` | RATIFIED |
| Tissue Layer Constitution | `packages/tissues/universe/doctrine/TISSUE_LAYER_CONSTITUTION.md` | RATIFIED |
| Organ Layer Constitution | `packages/organs/universe/doctrine/ORGAN_LAYER_CONSTITUTION.md` | RATIFIED |
| System Layer Constitution | `packages/systems/universe/doctrine/SYSTEM_LAYER_CONSTITUTION.md` | RATIFIED |

### Execution Protocols
| Document | Path | Status |
| :--- | :--- | :--- |
| PCAM-01 (Build Once, Use Infinitely) | `protocols/PCAM-01_PLATFORM_COMPOSITION_AND_ACTIVATION_MODEL.md` | RATIFIED |
| DGM-01/DEP-01 (Dependency Graph) | `protocols/DGM-01_DEP-01_DEPENDENCY_AND_EXECUTION_PROTOCOL.md` | RATIFIED |
| EIM-01 (Execution Integrity) | `protocols/EIM-01_EXECUTION_INTEGRITY_MONITORING_PROTOCOL.md` | RATIFIED |
| WEC-02 (Autonomous Monitoring) | `docs/execution-governance/WEC-02_AUTONOMOUS_EXECUTION_MONITORING_PROTOCOL.md` | RATIFIED |

### Agent Governance
| Document | Path | Status |
| :--- | :--- | :--- |
| AGVE Constitution v2.0.0 | `protocols/AGVE_CONSTITUTION_v2.0.0.md` | RATIFIED |
| IAAM Constitution v1.0.0 | `protocols/IAAM_CONSTITUTION_v1.0.0.md` | RATIFIED |
| Canonical Agent Specification | `protocols/CANONICAL_AGENT_SPECIFICATION.md` | RATIFIED |
| Agent Onboarding Package | `WEBWAKA_AGENT_ONBOARDING_PACKAGE.md` | CANONICAL |

### AI Governance
| Document | Path | Status |
| :--- | :--- | :--- |
| Organism AI Governance Constitution | `protocols/ORGANISM_AI_GOVERNANCE_CONSTITUTION_v1.0.0.md` | RATIFIED |
| AI Cognitive Fabric Constitution | `docs/ai-governance/AI_COGNITIVE_FABRIC_CONSTITUTION.md` | RATIFIED |

### Architecture
| Document | Path | Status |
| :--- | :--- | :--- |
| Core Platform Architecture | `WEBWAKA_CORE_PLATFORM_ARCHITECTURE.md` | RATIFIED |
| Offline-First Architecture | `WEBWAKA_OFFLINE_FIRST_ARCHITECTURE.md` | RATIFIED |

### Execution Plans
| Document | Path | Status |
| :--- | :--- | :--- |
| Week 1-71 Execution Plan | `WEEK_1_TO_71_DETAILED_EXECUTION_PLAN.md` | APPROVED |
| IPED-01-FULL Activation Report | `IPED-01-FULL_ACTIVATION_REPORT.md` | COMPLETED |

---

## Appendix B: The Immediate Next Step

**Phase 1: Core Platform Activation begins NOW.**

The first issue to execute is **CPA-01 (Issue #8): Identity System Activation**.

- **Assigned to:** webwakaagent4
- **PAT to use:** `[REDACTED — webwakaagent4 PAT — stored in secure vault]`
- **Dependencies:** Phase 0 complete (confirmed)
- **Technology:** NestJS + Passport.js + JWT
- **Key requirements:** 5-level actor hierarchy, tenant-scoped RLS, offline queue for failed auth events, event emission on all state changes, 80%+ test coverage, deployed to ECS Fargate

**Before starting CPA-01, the executing agent MUST:**
1. Re-read the `BIOLOGICAL_GOVERNANCE_CONSTITUTION`
2. Re-read the `WEBWAKA_CORE_PLATFORM_ARCHITECTURE.md`
3. Re-read the `WEBWAKA_OFFLINE_FIRST_ARCHITECTURE.md`
4. Verify the 10-point pre-execution checklist
5. Switch to webwakaagent4's PAT
6. Begin implementation with step-by-step GitHub pushes

---

**[DOCUMENT END]**

**This handover report was synthesized from the complete corpus of WebWaka governance documents. Any agent receiving this document is constitutionally bound by its contents. Proceed with discipline, precision, and full compliance.**
