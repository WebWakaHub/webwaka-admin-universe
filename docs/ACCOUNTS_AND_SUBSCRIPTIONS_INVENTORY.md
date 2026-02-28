# WebWaka Platform: Accounts & Subscriptions Inventory

**Document Type:** Implementation Prerequisite  
**Date:** 28 February 2026  
**Status:** ACTION REQUIRED  
**Purpose:** Detail every account and subscription that must be created before implementation can begin, based on the 12 approved technical decisions.

---

## Executive Summary

This document provides a comprehensive checklist of all external service accounts, subscriptions, and credentials required to build, deploy, and operate the WebWaka platform. It is organized into three tiers: **Core Platform Accounts** (essential for basic operation), **Financial & Communications Accounts** (for payments and messaging), and **Development & Tooling Accounts** (for the build process). For each account, the required documents, estimated costs, and responsible party (Founder) are clearly defined.

**Action Required:** The Founder must create these accounts and securely provide the necessary API keys and credentials to the development team before the implementation phases can commence.

---

## Tier 1: Core Platform Accounts (GitHub, AWS, Cloudflare)

These three platforms form the backbone of the WebWaka infrastructure. A single, unified billing and management approach is recommended.

| Service | Account/Subscription | Setup Requirements | Estimated Monthly Cost | Notes |
|---|---|---|---|---|
| **GitHub** | `WebWakaHub` Organization | Already exists | $4/user (Team Plan) | **Upgrade to Team Plan is mandatory.** This enables protected branches, code owners, and required reviewers, which are essential for the 42-agent Governance CI model. |
| **AWS** | Root Account | Email, credit card, phone number | ~$190–$250 (initial scale) | Create one root account. All services (ECS, RDS, SQS, EventBridge, ECR, SES) will be managed via IAM roles from this single account. Use AWS Cost Explorer to monitor spending. |
| **Cloudflare** | Pro Account | Email, credit card, domain name | $20/domain | A **Pro Account** is recommended for the enhanced WAF, image optimization (Polish/Mirage), and faster support. The free plan is an option but offers less security. R2 storage requires a credit card on file even for the free tier. |

---

## Tier 2: Financial & Communications Accounts (Nigeria-First)

These accounts are critical for monetization and user communication. They require Nigerian business registration documents.

| Service | Account/Subscription | Setup Requirements | Estimated Monthly Cost | Notes |
|---|---|---|---|---|
| **Paystack** | Registered Business Account | CAC Certificate, Form CAC 1.1, TIN, Director BVN & ID, Proof of Address | Variable (1.5% + ₦100 per transaction) | **This is a prerequisite.** A Registered Business account is required to use the Subaccounts and Split Payments API, which is the core of the MLAS implementation. A Starter Business account is insufficient. |
| **Flutterwave** | Business Account | CAC Certificate, Director ID & BVN, Proof of Address | Variable (1.4% per transaction) | To be used as a secondary/backup payment gateway. Requires similar documentation to Paystack. |
| **Termii** | Standard Account | Free registration | Variable (₦2.5-4 per SMS) | Primary SMS gateway for Nigeria. Sender ID must be registered with Termii to avoid messages being marked as spam. |
| **Africa's Talking** | Standard Account | Free registration | Variable (country-dependent) | Secondary SMS gateway for pan-African expansion and USSD support. |

**Prerequisite: Corporate Affairs Commission (CAC) Registration**
- To open a Paystack Registered Business or Flutterwave Business account, WebWaka must be a legally registered entity in Nigeria with the CAC.
- **Required Documents:** Certificate of Incorporation, Memorandum & Articles of Association, Form CAC 1.1.
- **Tax ID:** A Tax Identification Number (TIN) from the Federal Inland Revenue Service (FIRS) is also required.

---

## Tier 3: Development & Tooling Accounts

These accounts support the development and CI/CD process.

| Service | Account/Subscription | Setup Requirements | Estimated Monthly Cost | Notes |
|---|---|---|---|---|
| **Domain Registrar** | e.g., Namecheap, QServers | Credit card | ~$15/year (.com) or ~₦3,000/year (.com.ng) | The primary domain (e.g., `webwaka.com`) needs to be purchased. DNS will be managed by Cloudflare. |
| **Nx Cloud** | Free Tier | GitHub account | $0 (initially) | The free tier is sufficient for initial development. Can be upgraded to a paid plan later if CI performance becomes a bottleneck. |
| **Sentry.io** (Optional) | Free Tier | GitHub account | $0 (initially) | Recommended for application-level error tracking. The free tier includes 10,000 errors/month. |

---

## Summary of Actions for the Founder

1. **Ensure WebWaka is a CAC-registered entity** with a TIN.
2. **Create an AWS root account** and provide billing details.
3. **Upgrade the `WebWakaHub` GitHub organization** to the Team Plan.
4. **Create a Cloudflare Pro account** and add the primary domain.
5. **Create a Paystack Registered Business account** using CAC documents.
6. **Create a Flutterwave Business account**.
7. **Create a Termii account** and register the primary Sender ID.
8. **Create an Africa's Talking account**.
9. **Purchase the primary domain name**.
10. **Securely share all API keys, secrets, and credentials** with the lead development agent via a secure channel (e.g., GitHub repository secrets, AWS Secrets Manager).
