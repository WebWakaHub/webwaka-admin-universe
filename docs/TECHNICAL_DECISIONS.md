# WebWaka Platform: Comprehensive Decision Document for Production Readiness

**Document Type:** Founder Decision Input  
**Date:** 28 February 2026  
**Status:** AWAITING FOUNDER DECISIONS  
**Purpose:** Identify every specific area requiring a Founder decision before detailed implementation planning can begin, incorporating the full platform vision including multi-tenancy, white-labelling, partner models, economic graph, and deployment architecture.

---

## Executive Summary

This document synthesizes findings from a thorough review of the entire WebWaka documentation corpus — the Canonical Master Context V4.3, the Multi-Tenant Data Scoping Specification, the MLAS Economic & Affiliate Graph, the Platform Federation Constitution, the Runtime Plane Constitution, the Deployment Infrastructure Specification, the Payment & Billing System Specification, the Subscription & Pricing Strategy, the Partner & Affiliate Program, and the governance documents in `webwaka-admin-universe`.

WebWaka is a **Platform-for-Platforms** with a five-level actor hierarchy (Super Admin → Partner → Tenant → Vendor → End User), full white-labelling, a non-negotiable multi-level economic graph, and 12 architectural invariants including offline-first, event-driven, and multi-tenant by default. The platform is designed for a 10-year trajectory starting with Commerce and Transportation suites.

The current state of the codebase consists of 124 biological-layer TypeScript class libraries across 50+ repositories. These are well-structured blueprints but are not deployed services — they have no REST APIs, no databases, no published packages, and no cross-layer wiring. The Super Admin Dashboard has been reset to a clean state.

**There are 12 specific decision areas** where Founder input is required before implementation can proceed. Each is presented below with options, pros, cons, and a recommendation aligned with the stated preference for GitHub + AWS + Cloudflare as the primary stack, with Nigeria-first providers for SMS and payments.

---

## Decision 1: Monorepo vs. Polyrepo Strategy

**Context:** WebWaka currently has 148 separate repositories in the WebWakaHub organization. The canonical documentation does not prescribe a specific repository strategy. The biological layer repos (organelle, cell, tissue, organ, system, organism) each exist as separate repos, but they need to share code, types, and interfaces extensively.

**Why This Matters:** The choice fundamentally affects how 42 agents collaborate, how CI/CD pipelines are structured, how packages are shared, and how deployment is orchestrated. With multi-tenancy, white-labelling, and 19+ business domain suites, the dependency graph is complex.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| **A: Nx Monorepo** | Consolidate all code into a single Nx-managed monorepo with workspace packages | Single source of truth; atomic cross-package changes; shared CI; Nx caching dramatically speeds builds; easier type sharing across biological layers | Large repo size; requires Nx expertise; all agent teams work in one repo (potential merge conflicts); GitHub Actions may need optimization for large repos |
| **B: Turborepo Monorepo** | Similar to Option A but using Turborepo instead of Nx | Simpler configuration than Nx; good caching; Vercel-backed (strong ecosystem); lighter learning curve | Less mature than Nx for large enterprise monorepos; fewer built-in generators; less sophisticated dependency graph analysis |
| **C: Federated Polyrepo with Shared Packages** | Keep separate repos but publish shared packages to GitHub Packages; use a meta-repo for orchestration | Familiar Git workflow; independent deployment per service; clear ownership boundaries per agent team; smaller repos are faster to clone | Cross-repo changes require coordinated PRs; version drift between packages; more complex CI/CD; harder to enforce architectural invariants across repos |

**Recommendation:** **Option A (Nx Monorepo)** — Given that WebWaka enforces 12 architectural invariants via Governance CI, a monorepo makes this enforcement dramatically simpler. The biological layers (organelle → cell → tissue → organ → system → organism) form a strict dependency chain that benefits from atomic changes. Nx's affected-commands feature means only changed packages are rebuilt/tested, keeping CI fast despite repo size. The 148 existing repos would be archived and their governance documents consolidated.

---

## Decision 2: Package Registry for Internal Packages

**Context:** Regardless of monorepo or polyrepo, internal packages (biological layers, shared types, utilities) need to be consumable. In a monorepo, this is handled by workspace references. In a polyrepo, a registry is needed.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| **A: GitHub Packages** | Publish npm packages to GitHub's built-in registry | Unified with GitHub ecosystem; free for private packages in organizations; native integration with GitHub Actions | Slower than npm registry; requires GitHub authentication for installs; less mature tooling |
| **B: Workspace References (Monorepo)** | Use Nx/Turborepo workspace references — no external registry needed | Zero overhead; instant cross-package imports; no versioning complexity; no publish step | Only works within the monorepo; external consumers (e.g., partner integrations) would need a different mechanism |
| **C: npm Private Registry** | Use npm's private registry or Verdaccio (self-hosted) | Industry standard; fast; well-tooled | Additional cost (npm) or operational overhead (Verdaccio); another platform to manage |

**Recommendation:** **Option B (Workspace References)** if monorepo is chosen. If polyrepo, **Option A (GitHub Packages)**. The monorepo approach eliminates the need for a separate registry entirely, reducing complexity.

---

## Decision 3: Backend Runtime and Framework

**Context:** The canonical documentation specifies TypeScript as the language and mentions NestJS-style patterns (modules, services, entities). The biological layer repos already use TypeScript classes with dependency injection patterns. The platform requires: event-driven architecture, multi-tenant data scoping, offline-first sync, plugin-first extensibility, and API-first design.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| **A: NestJS** | Enterprise Node.js framework with decorators, modules, DI, and built-in support for microservices, WebSockets, and GraphQL | Matches existing code patterns perfectly; built-in module system aligns with biological layers; native TypeORM/Prisma integration for multi-tenant queries; built-in event emitter and microservice transports; large ecosystem; strong typing | Heavier than alternatives; decorator-heavy syntax; learning curve for those unfamiliar with Angular-style patterns |
| **B: Fastify + Custom Architecture** | Lightweight Node.js framework with custom module/DI system | Fastest Node.js framework (benchmarks); minimal overhead; full control over architecture | Must build module system, DI, event bus, and plugin system from scratch; more code to maintain; less standardized |
| **C: Hono (Edge-First)** | Ultra-lightweight framework designed for edge computing (Cloudflare Workers) | Runs on Cloudflare Workers (edge); extremely fast cold starts; minimal bundle size; good for Africa-first latency | Very new; limited ecosystem; no built-in DI or module system; database access from edge is complex; not suitable for heavy backend logic |

**Recommendation:** **Option A (NestJS)** — The existing biological layer code already uses NestJS-compatible patterns (classes, decorators, modules). NestJS's built-in module system maps directly to the biological hierarchy (each organ/system becomes a NestJS module). Its microservice transport layer supports the event-driven architecture mandate. TypeORM or Prisma integration handles multi-tenant query interceptors. The multi-agent model benefits from NestJS's opinionated structure — it reduces architectural drift.

---

## Decision 4: Database Strategy

**Context:** The Multi-Tenant Data Scoping Specification mandates logical multi-tenancy with row-level security, support for 100,000 tenants, tenant hierarchy with materialized paths, and < 5ms scoping overhead per query. The MLAS requires immutable transaction records and complete audit trails. The platform must support offline-first with sync-on-reconnect.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| **A: AWS RDS PostgreSQL** | Managed PostgreSQL with Multi-AZ deployment | Native row-level security (RLS) for multi-tenancy; JSONB for flexible tenant config; materialized views for hierarchy; strong ACID compliance for financial transactions; mature ecosystem; AWS-managed backups and failover | Single-region by default (Multi-AZ is same region); vertical scaling has limits; connection pooling needed at scale |
| **B: AWS Aurora PostgreSQL** | AWS-enhanced PostgreSQL with serverless scaling | Auto-scaling read replicas; serverless v2 scales to zero; 5x throughput of standard PostgreSQL; global database for multi-region; storage auto-scales | Higher cost than RDS; Aurora-specific behaviors may differ from standard PostgreSQL; vendor lock-in to Aurora |
| **C: AWS Aurora PostgreSQL + DynamoDB (Hybrid)** | PostgreSQL for transactional data, DynamoDB for event store and audit logs | Best of both worlds: ACID for transactions, infinite scale for events/audit; DynamoDB streams for real-time event processing; cost-effective for high-volume writes | Two database systems to manage; increased complexity; DynamoDB's query model is limited; data consistency across systems |

**Recommendation:** **Option A (AWS RDS PostgreSQL)** for initial launch, with a clear upgrade path to **Option B (Aurora)** when scale demands it. PostgreSQL's native RLS is purpose-built for the multi-tenant scoping requirement. Starting with RDS keeps costs low (a db.t3.medium instance is ~$50/month) while Aurora can be adopted later without code changes. The MLAS audit trail can be stored in the same PostgreSQL instance initially, with a migration to DynamoDB when transaction volume warrants it.

---

## Decision 5: Multi-Tenancy Implementation Pattern

**Context:** The spec mandates logical multi-tenancy. But within that, there are sub-patterns for how tenant isolation is enforced at the database level.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| **A: Shared Schema + RLS** | All tenants share the same tables; PostgreSQL Row-Level Security policies enforce isolation | Simplest to manage; lowest cost; easiest to query across tenants (for Super Admin); schema migrations apply once | All data in one schema (perception concern for enterprise clients); RLS policies must be bulletproof; performance at extreme scale |
| **B: Schema-per-Tenant** | Each tenant gets their own PostgreSQL schema within the same database | Stronger isolation; easier data export per tenant; can drop entire schema for deprovisioning | Schema migration must run per tenant; connection management is complex; harder to query across tenants; operational overhead grows with tenant count |
| **C: Database-per-Partner, Schema-per-Tenant** | Each Partner (L2) gets their own database; Tenants within that Partner get schemas | Strongest isolation for white-labelling; Partners can have their own database credentials; true data sovereignty | Most complex to manage; cross-partner queries require federation; highest operational cost; connection pooling across databases |

**Recommendation:** **Option A (Shared Schema + RLS)** — This aligns with the Multi-Tenant Data Scoping Specification which explicitly describes a shared-table model with automatic query interceptors. PostgreSQL RLS is battle-tested for this pattern. The spec targets 100,000 tenants, which is feasible with shared schema but impractical with schema-per-tenant. For enterprise clients requiring stronger isolation guarantees, Option C can be offered as a premium tier later — but the core platform should start with Option A.

---

## Decision 6: Compute and Deployment Model

**Context:** The Deployment Infrastructure Specification mentions EC2 Auto Scaling Groups. The canonical context mandates zero-downtime deployments, < 5 minute deployment time, and 99.9% uptime. The platform needs to support multiple services (API gateway, suite services, event processor, background workers).

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| **A: AWS ECS with Fargate** | Serverless containers — no EC2 instances to manage | No server management; auto-scaling per service; pay-per-use; simpler than Kubernetes; native AWS integration (ALB, CloudWatch, Secrets Manager); good for microservices | Higher per-unit cost than EC2; cold start latency for Fargate tasks; less control than EC2; Fargate Spot can be interrupted |
| **B: AWS ECS with EC2** | Container orchestration on self-managed EC2 instances | Lower cost than Fargate at scale; full control over instance types; can use Reserved Instances for savings; no cold starts | Must manage EC2 instances (patching, scaling); more operational overhead; capacity planning required |
| **C: AWS EKS (Kubernetes)** | Managed Kubernetes on AWS | Industry standard for container orchestration; most flexible; huge ecosystem (Helm, Istio, etc.); portable across clouds | Highest complexity; requires Kubernetes expertise; EKS control plane costs $73/month; overkill for initial scale; steep learning curve for the agent teams |
| **D: AWS Lambda + API Gateway** | Fully serverless functions | Zero infrastructure management; scales to zero; pay only for invocations; fastest time-to-deploy | Cold starts problematic for Africa-first latency; 15-minute execution limit; complex for stateful operations; NestJS on Lambda requires adaptation; connection pooling challenges with RDS |

**Recommendation:** **Option A (ECS with Fargate)** — This provides the right balance of simplicity and capability. Each biological system (e-commerce, transportation, etc.) runs as a separate Fargate service, enabling independent scaling and deployment. No server management means the agent teams don't need DevOps expertise. The upgrade path to ECS with EC2 (Option B) is seamless when cost optimization becomes important. Kubernetes (Option C) can be adopted later if the platform's complexity truly demands it.

---

## Decision 7: Frontend Delivery and Hosting

**Context:** The canonical context mandates PWA-first, mobile-first, and offline-first. The SAD is a separate frontend from the tenant-facing applications. White-labelling requires each Partner to potentially have their own domain and branding.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| **A: Cloudflare Pages** | Static site hosting on Cloudflare's edge network | Global CDN with edge locations in Africa (Lagos, Nairobi, Johannesburg); free SSL; automatic deployments from GitHub; Workers for edge logic; excellent performance | Limited server-side rendering; build size limits; less AWS integration |
| **B: AWS Amplify Hosting** | AWS-managed frontend hosting | Native AWS integration; supports SSR with Next.js; built-in CI/CD; custom domains | Fewer African edge locations than Cloudflare; higher cost; less mature than Cloudflare Pages |
| **C: Cloudflare Pages + Workers (Edge SSR)** | Static hosting with edge-side rendering via Workers | Best of both worlds: edge CDN + dynamic rendering; ideal for white-label domain routing; Workers can handle tenant-specific branding at the edge | More complex architecture; Workers have execution limits; debugging is harder |

**Recommendation:** **Option C (Cloudflare Pages + Workers)** — The white-labelling requirement makes this the clear winner. Cloudflare Workers can intercept requests at the edge, determine the Partner/Tenant from the custom domain, inject the correct branding/theme, and serve the appropriate PWA shell — all before the request ever hits AWS. Cloudflare has edge nodes in Lagos, Nairobi, and Johannesburg, which directly serves the Africa-first mandate. The SAD itself would be a separate Cloudflare Pages deployment on a WebWaka-owned domain.

---

## Decision 8: Event Bus and Message Queue

**Context:** The canonical context mandates event-driven architecture — "all state changes must emit events." The MLAS requires real-time economic calculations and audit trails. Multi-tenant events must be scoped. The offline-first mandate requires reliable message delivery with retry.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| **A: AWS SQS + SNS** | Managed message queue (SQS) with pub/sub (SNS) | Fully managed; scales infinitely; native AWS integration; SQS guarantees at-least-once delivery; SNS supports fan-out; very low cost; FIFO queues for ordering | Not a true event streaming platform; no event replay; limited to AWS; no consumer groups |
| **B: AWS EventBridge** | Serverless event bus with schema registry and rules engine | Purpose-built for event-driven architectures; schema registry for event validation; rules engine for routing; native AWS integration; archive and replay capability | Higher cost per event than SQS/SNS; 64KB event size limit; less community tooling; AWS-specific |
| **C: AWS MSK (Managed Kafka)** | Managed Apache Kafka on AWS | True event streaming with replay; consumer groups; high throughput; industry standard; event sourcing support | Most expensive option; operational complexity; overkill for initial scale; minimum 3-broker cluster (~$500/month) |
| **D: AWS SQS + EventBridge (Hybrid)** | SQS for task queues and background jobs; EventBridge for domain events and cross-service communication | Best of both: SQS for reliable work processing, EventBridge for event routing and replay; cost-effective; schema validation for domain events | Two systems to learn; slightly more complex than pure SQS/SNS |

**Recommendation:** **Option D (SQS + EventBridge Hybrid)** — EventBridge is purpose-built for the event-driven architecture mandate. Its schema registry enforces event contracts across biological layers. Its archive-and-replay feature supports the audit trail requirement. SQS handles background work (billing cycles, data exports, sync jobs) with guaranteed delivery. This combination is cost-effective and scales well, with a clear upgrade path to Kafka (Option C) if event volume demands it.

---

## Decision 9: Payment Gateway

**Context:** The Payment & Billing System Specification mandates integration with Nigerian payment gateways (Paystack, Flutterwave) using a strategy pattern for gateway abstraction. The MLAS requires escrow management, multi-level revenue splitting, and real-time economic calculations.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| **A: Paystack (Primary) + Flutterwave (Secondary)** | Paystack as default, Flutterwave as alternative | Paystack: best developer experience in Nigeria; comprehensive API; supports subscriptions, split payments, and subaccounts (critical for MLAS); acquired by Stripe (global expansion path). Flutterwave: broader African coverage; supports more currencies | Two integrations to maintain; Paystack's split payment has limits on number of subaccounts; Flutterwave's API is less consistent |
| **B: Paystack Only** | Single gateway to reduce complexity | Simplest integration; Paystack's split payment API directly supports the MLAS revenue chain; subaccounts map to Partners/Tenants/Vendors; excellent documentation | Single point of failure; no fallback if Paystack has downtime; limited to Paystack-supported countries |
| **C: Flutterwave Only** | Single gateway with broader African coverage | Supports 150+ currencies; available in more African countries; Rave checkout is user-friendly | Less reliable API than Paystack; developer experience is weaker; split payment support is less mature |

**Recommendation:** **Option A (Paystack Primary + Flutterwave Secondary)** — The strategy pattern in the spec already anticipates multiple gateways. Paystack's **subaccount and split payment API** is critical for implementing the MLAS — each Partner, Tenant, and Vendor can be a Paystack subaccount, and the platform can automatically split payments according to the economic graph. Flutterwave provides geographic redundancy for expansion beyond Nigeria. The gateway abstraction layer means adding more gateways later (Stripe for international, M-Pesa for East Africa) is straightforward.

---

## Decision 10: SMS Gateway

**Context:** SMS is critical for OTP verification, transaction notifications, and agent communication in the Africa-first context. Many end users rely on SMS over email. The platform must support bulk SMS, OTP, and transactional messaging.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| **A: Termii** | Nigeria-first multi-channel messaging platform (SMS, WhatsApp, Voice, Email) | Purpose-built for Nigeria; multi-channel (SMS + WhatsApp + Voice); token/OTP API; sender ID registration handled; competitive pricing (₦2.5-4 per SMS); good API documentation | Smaller company than alternatives; limited presence outside Nigeria; less mature API than Twilio |
| **B: Africa's Talking** | Pan-African communications platform (SMS, Voice, USSD, Airtime) | Covers 20+ African countries; USSD support (critical for feature phones); airtime disbursement API; well-established; good developer community | Higher per-SMS cost than Termii for Nigeria; less focused on Nigeria specifically; API can be inconsistent |
| **C: Termii (Primary) + Africa's Talking (Pan-African)** | Termii for Nigeria, Africa's Talking for rest of Africa | Best of both: lowest cost in Nigeria with Termii; broadest African coverage with Africa's Talking; USSD support for feature phones via Africa's Talking | Two integrations to maintain; different APIs and dashboards |

**Recommendation:** **Option C (Termii + Africa's Talking)** — Termii provides the best Nigeria-first experience at the lowest cost. Africa's Talking provides the pan-African expansion path with USSD support (critical for the field operations reality — motor parks, markets, etc., where feature phones are common). Like the payment gateway, the messaging layer should use a provider abstraction pattern.

---

## Decision 11: Object Storage and File Management

**Context:** The platform needs to store product images, documents, invoices, tenant assets (logos, themes), and user uploads. White-labelling requires tenant-specific asset isolation. The offline-first mandate requires local caching of assets.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| **A: AWS S3 + CloudFront** | S3 for storage, CloudFront for CDN delivery | Industry standard; unlimited storage; fine-grained access control with bucket policies; lifecycle management; versioning; CloudFront for global delivery | CloudFront has fewer African edge locations than Cloudflare; S3 egress costs can be high |
| **B: Cloudflare R2 + Cloudflare CDN** | R2 for storage (S3-compatible), Cloudflare CDN for delivery | Zero egress fees (major cost saving); S3-compatible API; Cloudflare's superior African edge network; automatic CDN integration | Newer than S3; fewer features (no lifecycle policies yet); less mature tooling |
| **C: Cloudflare R2 (Storage) + Cloudflare CDN (Delivery) + AWS S3 (Backup)** | R2 as primary storage with S3 as backup/archive | Zero egress for serving; best African CDN performance; S3 as durable backup; S3-compatible API means easy migration between them | Two storage systems; sync complexity; slightly more operational overhead |

**Recommendation:** **Option B (Cloudflare R2)** — The zero egress fee is transformative for a platform that serves images and assets to potentially millions of end users across Africa. Cloudflare's African edge network (Lagos, Nairobi, Johannesburg, Cape Town, Mombasa, Dar es Salaam) provides superior delivery performance. The S3-compatible API means existing S3 tooling and SDKs work unchanged. For critical backups, AWS S3 can be added later via replication.

---

## Decision 12: Authentication and Identity

**Context:** The canonical context mandates a unified identity system where one human can have multiple roles across suites and tenants. Offline identity continuity is required. Shared device support is mandatory. The actor hierarchy (L1-L5) requires hierarchical permission enforcement.

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| **A: Custom Auth (NestJS + Passport.js + JWT)** | Build authentication from scratch using Passport.js strategies and JWT tokens | Full control over the complex actor hierarchy; can implement offline identity continuity exactly as specified; no external dependency; tenant-scoped tokens; hierarchical permissions built-in | Must build everything: registration, login, password reset, MFA, session management; security responsibility is entirely internal; more code to maintain |
| **B: AWS Cognito + Custom Authorization** | Cognito for authentication (registration, login, MFA, social login); custom middleware for the actor hierarchy authorization | Managed auth service; built-in MFA, social login, email/SMS verification; scales automatically; handles security best practices | Cognito's group/role model doesn't map to the 5-level actor hierarchy; custom claims are limited; offline token refresh is complex; Cognito pricing can be high at scale ($0.0055/MAU after 50K) |
| **C: Custom Auth with Cognito as Identity Provider** | Cognito handles identity verification (email/phone/social); custom system handles actor hierarchy, permissions, and tenant scoping | Best of both: Cognito handles the hard security parts (password hashing, MFA, social login); custom system handles the WebWaka-specific actor model | More complex architecture; two systems to coordinate; Cognito's limitations still apply for some flows |

**Recommendation:** **Option A (Custom Auth)** — The WebWaka identity model is too specialized for any off-the-shelf auth service. The requirements for offline identity continuity, shared device support, cross-suite contextual role binding, and the 5-level actor hierarchy with sub-roles are unique to WebWaka. Building custom auth with Passport.js and JWT gives full control. The offline-first mandate means tokens must be long-lived and locally verifiable — this is straightforward with JWT but complex with external auth providers. Security best practices (bcrypt, rate limiting, CSRF protection) are well-documented patterns in NestJS.

---

## Summary of Decisions Required

| # | Decision Area | Recommended Choice | Alternatives |
|---|---|---|---|
| 1 | Monorepo Strategy | **Nx Monorepo** | Turborepo, Federated Polyrepo |
| 2 | Package Registry | **Workspace References** (monorepo) | GitHub Packages, npm Private |
| 3 | Backend Framework | **NestJS** | Fastify, Hono |
| 4 | Database | **AWS RDS PostgreSQL** (upgrade to Aurora later) | Aurora, Aurora + DynamoDB |
| 5 | Multi-Tenancy Pattern | **Shared Schema + RLS** | Schema-per-Tenant, DB-per-Partner |
| 6 | Compute Model | **AWS ECS Fargate** | ECS EC2, EKS, Lambda |
| 7 | Frontend Hosting | **Cloudflare Pages + Workers** | AWS Amplify, Cloudflare Pages only |
| 8 | Event Bus | **SQS + EventBridge Hybrid** | SQS/SNS, EventBridge only, Kafka |
| 9 | Payment Gateway | **Paystack (primary) + Flutterwave (secondary)** | Paystack only, Flutterwave only |
| 10 | SMS Gateway | **Termii (Nigeria) + Africa's Talking (Pan-African)** | Termii only, Africa's Talking only |
| 11 | Object Storage | **Cloudflare R2** | AWS S3 + CloudFront, R2 + S3 hybrid |
| 12 | Authentication | **Custom Auth (NestJS + Passport.js + JWT)** | AWS Cognito, Cognito + Custom hybrid |

---

## Platform Stack Summary (If All Recommendations Accepted)

```
┌─────────────────────────────────────────────────────────────────┐
│                        END USERS (Mobile/PWA)                    │
└──────────────────────────┬──────────────────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────────────────┐
│                    CLOUDFLARE EDGE LAYER                          │
│  ┌─────────────┐  ┌──────────────┐  ┌────────────────────────┐  │
│  │ Cloudflare   │  │ Cloudflare   │  │ Cloudflare R2          │  │
│  │ Pages (PWA)  │  │ Workers      │  │ (Object Storage)       │  │
│  │              │  │ (White-label │  │                        │  │
│  │ - SAD        │  │  routing,    │  │ - Product images       │  │
│  │ - Tenant Apps│  │  branding,   │  │ - Tenant assets        │  │
│  │              │  │  edge logic) │  │ - Documents            │  │
│  └─────────────┘  └──────────────┘  └────────────────────────┘  │
│  ┌─────────────────────────────────────────────────────────────┐ │
│  │ Cloudflare DNS + DDoS + WAF + SSL/TLS                      │ │
│  └─────────────────────────────────────────────────────────────┘ │
└──────────────────────────┬──────────────────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────────────────┐
│                      AWS COMPUTE LAYER                            │
│  ┌─────────────────────────────────────────────────────────────┐ │
│  │              AWS ECS Fargate (NestJS Services)              │ │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐      │ │
│  │  │ Identity │ │ Commerce │ │Transport │ │ Billing  │ ...  │ │
│  │  │ Service  │ │ Service  │ │ Service  │ │ Service  │      │ │
│  │  └──────────┘ └──────────┘ └──────────┘ └──────────┘      │ │
│  └─────────────────────────────────────────────────────────────┘ │
│  ┌─────────────────────────────────────────────────────────────┐ │
│  │              AWS EventBridge + SQS                          │ │
│  │  (Domain events, tenant-scoped routing, background jobs)   │ │
│  └─────────────────────────────────────────────────────────────┘ │
└──────────────────────────┬──────────────────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────────────────┐
│                      AWS DATA LAYER                               │
│  ┌─────────────────────────────────────────────────────────────┐ │
│  │  AWS RDS PostgreSQL (Multi-AZ)                              │ │
│  │  Row-Level Security for multi-tenancy                       │ │
│  │  Materialized paths for tenant hierarchy                    │ │
│  └─────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                    EXTERNAL INTEGRATIONS                          │
│  ┌──────────┐ ┌──────────────┐ ┌──────────┐ ┌───────────────┐  │
│  │ Paystack │ │ Flutterwave  │ │ Termii   │ │ Africa's      │  │
│  │ (Payment)│ │ (Payment)    │ │ (SMS-NG) │ │ Talking (SMS) │  │
│  └──────────┘ └──────────────┘ └──────────┘ └───────────────┘  │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                    DEVELOPMENT & CI/CD                            │
│  ┌──────────────────┐  ┌──────────────────┐                     │
│  │ GitHub (Monorepo) │  │ GitHub Actions   │                     │
│  │ Nx Workspace      │  │ Governance CI    │                     │
│  │ 42 Agent Teams    │  │ Product CI       │                     │
│  └──────────────────┘  └──────────────────┘                     │
└─────────────────────────────────────────────────────────────────┘
```

---

## Estimated Monthly Cost (Initial Launch — Minimal Scale)

| Service | Specification | Estimated Monthly Cost |
|---------|--------------|----------------------|
| AWS ECS Fargate | 4 services × 0.5 vCPU / 1GB RAM | $60–$120 |
| AWS RDS PostgreSQL | db.t3.medium, Multi-AZ | $100 |
| AWS EventBridge | 1M events/month | $1 |
| AWS SQS | 1M requests/month | $0.40 |
| AWS VPC, ALB | Application Load Balancer | $25 |
| Cloudflare Pages | Free tier (unlimited sites) | $0 |
| Cloudflare Workers | Free tier (100K requests/day) | $0 |
| Cloudflare R2 | 10GB storage, 10M reads | $0.15 |
| GitHub | Team plan (per user) | $4/user |
| Paystack | Transaction fees only (1.5% + ₦100) | Variable |
| Termii | Pay-per-SMS (₦2.5-4/SMS) | Variable |
| **Total Fixed Infrastructure** | | **~$190–$250/month** |

This is a lean starting point. Costs scale with usage, not upfront commitment.

---

## Next Steps After Decisions

Once all 12 decisions are confirmed or modified:

1. **Detailed Implementation Plan** — A phase-by-phase implementation document aligned with the Zero-Based Reconstruction Playbook (Sections 17.1–17.5 of the Canonical Master Context).

2. **Issue Creation** — GitHub issues in `webwaka-admin-universe` for each implementation phase, assigned to the appropriate agent accounts per the 42-agent model.

3. **Governance CI Setup** — The first implementation task: set up Governance CI in the monorepo before any product code is written (per Section 16.4.6).

4. **Foundation Phase** — AWS account setup, Cloudflare configuration, Nx monorepo initialization, and CI/CD pipeline establishment.

---

**This document requires Founder decisions on all 12 items before implementation planning can proceed.**
