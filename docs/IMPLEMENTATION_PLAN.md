# WebWaka Platform: Comprehensive Implementation Plan

**Document Type:** Implementation Roadmap & Phasing
**Date:** 28 February 2026
**Status:** AWAITING EXECUTION
**Purpose:** Provide a detailed, phase-by-phase implementation plan for the WebWaka platform, based on the 12 approved technical decisions and the Zero-Based Reconstruction Playbook.

---

## Executive Summary

This document outlines the four-phase implementation plan to take WebWaka from its current state (124 blueprint libraries, clean-slate SAD) to a production-ready, multi-tenant, white-label Platform-for-Platforms. The plan is designed for parallel execution by 42 agent teams operating within a unified Nx monorepo, governed by strict CI/CD checks.

**The Four Phases:**

1.  **Phase 0: Foundation & Governance (1-2 weeks)** - Setup all accounts, monorepo, CI/CD, and Governance CI. This is the non-negotiable first step.
2.  **Phase 1: Core Platform Activation (4-6 weeks)** - Activate the 4 core biological systems (Identity, Billing, Notifications, Tenancy) and build the corresponding SAD modules.
3.  **Phase 2: Business Domain Activation (6-8 weeks)** - Activate the 19 business domain systems (e.g., Commerce, Transportation) and build the SAD management UIs.
4.  **Phase 3: Partner & Federation Activation (4-6 weeks)** - Activate the Partner Platform, white-labelling, MLAS economic graph, and the Organism-level event bus.

Each phase is broken down into specific epics and user stories, which will be created as issues in the `webwaka-admin-universe` repository.

---

## Phase 0: Foundation & Governance (Prerequisite)

**Goal:** Establish the technical and governance foundation for the entire project.
**Key Outcomes:** A fully configured monorepo, a working CI/CD pipeline that enforces architectural invariants, and all required cloud services provisioned.

| Epic | User Stories / Tasks | Lead Agent Account |
|---|---|---|
| **FND-01: Account & Subscription Setup** | - Procure all 10 required accounts (AWS, Cloudflare, Paystack, etc.)<br>- Securely store all API keys in AWS Secrets Manager<br>- Configure billing alerts | Founder | 
| **FND-02: Monorepo Initialization** | - Archive all 148 existing repos<br>- Initialize a new `webwaka-platform` monorepo using Nx<br>- Migrate all 124 biological layer libraries into the monorepo<br>- Configure workspace dependencies and `tsconfig.json` paths | webwakaagent1 (Architecture) |
| **FND-03: Governance CI Implementation** | - Implement GitHub Actions workflow for Governance CI<br>- Create scripts to enforce the 12 architectural invariants (e.g., no cross-layer imports, offline-first compliance, event-driven checks)<br>- Configure protected branches and required reviewers | webwakaagent5 (QA & Testing) |
| **FND-04: Cloud Infrastructure Provisioning** | - Set up AWS VPC, subnets, and security groups using Terraform/CloudFormation<br>- Configure Cloudflare DNS, WAF, and R2 buckets<br>- Provision the initial RDS PostgreSQL instance | webwakaagent2 (Infrastructure) |
| **FND-05: CI/CD Pipeline Setup** | - Create GitHub Actions workflows for build, test, and lint<br>- Configure deployment pipeline to AWS ECS Fargate<br>- Set up container registry (AWS ECR) | webwakaagent2 (Infrastructure) |

---

## Phase 1: Core Platform Activation

**Goal:** Bring the four essential backend systems online and build the core SAD functionality.
**Key Outcomes:** A live API for identity and tenancy, a functional SAD login, and the ability to create and manage tenants.

| Epic | User Stories / Tasks | Lead Agent Account |
|---|---|---|
| **CPA-01: Identity System Activation** | - Create NestJS service for the Identity Organ System<br>- Implement custom authentication (Passport.js + JWT)<br>- Implement the 5-level actor hierarchy and permissions<br>- Deploy as a Fargate service | webwakaagent4 (Identity) |
| **CPA-02: Tenancy System Activation** | - Create NestJS service for the Tenancy Organ System<br>- Implement multi-tenant data scoping using RLS in PostgreSQL<br>- Create APIs for tenant creation, configuration, and lifecycle management<br>- Deploy as a Fargate service | webwakaagent4 (Identity) |
| **CPA-03: Billing System Activation** | - Create NestJS service for the Billing Organ System<br>- Integrate with Paystack and Flutterwave using the strategy pattern<br>- Implement subscription management and invoicing<br>- Deploy as a Fargate service | webwakaagent6 (Finance) |
| **CPA-04: Notifications System Activation** | - Create NestJS service for the Notifications Organ System<br>- Integrate with Termii and Africa's Talking<br>- Implement email, SMS, and push notification templates<br>- Deploy as a Fargate service | webwakaagent7 (Comms) |
| **CPA-05: SAD Core UI Build** | - Create the SAD frontend shell (React + Vite)<br>- Build login, user management, and tenant management UIs<br>- Integrate with the live Identity and Tenancy APIs<br>- Deploy to Cloudflare Pages | webwakaagent3 (SAD UI) |

---

## Phase 2: Business Domain Activation

**Goal:** Activate the 19 business domain suites and provide management capabilities in the SAD.
**Key Outcomes:** Live APIs for all business domains, and the ability for Super Admins to manage domain-specific settings.

| Epic | User Stories / Tasks | Lead Agent Account |
|---|---|---|
| **BDA-01: Commerce Suite Activation** | - Activate the 5 systems in the Commerce Suite (e.g., Products, Orders, Inventory)<br>- Create NestJS services for each system<br>- Deploy as Fargate services | webwakaagent8 (Commerce) |
| **BDA-02: Transportation Suite Activation** | - Activate the 4 systems in the Transportation Suite (e.g., Routes, Bookings, Fleet)<br>- Create NestJS services for each system<br>- Deploy as Fargate services | webwakaagent9 (Transport) |
| **BDA-03: ... (17 more suites)** | - Repeat activation process for all remaining business domain suites (e.g., Agriculture, Healthcare, Education) | Respective Agent Teams |
| **BDA-04: SAD Domain Management UI** | - Build dynamic UI in the SAD to manage settings for each activated domain<br>- Implement feature flagging and domain-specific configuration screens | webwakaagent3 (SAD UI) |

---

## Phase 3: Partner & Federation Activation

**Goal:** Implement the white-labelling, partner management, and revenue-sharing capabilities.
**Key Outcomes:** A fully functional partner portal, automated white-label tenant onboarding, and a live MLAS economic graph.

| Epic | User Stories / Tasks | Lead Agent Account |
|---|---|---|
| **PFA-01: Partner Platform Activation** | - Activate the Partner Platform system<br>- Build APIs for partner registration, tier management, and analytics<br>- Create the Partner Portal frontend | webwakaagent10 (Partners) |
| **PFA-02: White-Labelling Engine** | - Implement Cloudflare Worker for dynamic domain routing and branding injection<br>- Build tenant-specific theme and asset management in the SAD<br>- Automate DNS and SSL certificate provisioning for custom domains | webwakaagent2 (Infrastructure) |
| **PFA-03: MLAS Economic Graph** | - Implement real-time revenue splitting logic in the Billing service<br>- Integrate with Paystack's subaccount and split payment APIs<br>- Build MLAS analytics and reporting in the SAD and Partner Portal | webwakaagent6 (Finance) |
| **PFA-04: Organism Layer Activation** | - Deploy the Organism-level event bus (EventBridge)<br>- Ensure all system-level events are published to the organism bus<br>- Implement cross-suite workflows and data federation | webwakaagent1 (Architecture) |

---

## Next Steps

1.  **Issue Creation:** Create GitHub issues for all epics and user stories in this plan within the `webwaka-admin-universe` repository.
2.  **Agent Assignment:** Assign lead agent accounts to each epic.
3.  **Commence Phase 0:** Begin with the Foundation & Governance phase immediately upon receiving the necessary accounts and credentials from the Founder.
