# Microsoft Entra ID: IAM Configuration & Hybrid Architecture Analysis

**Project Type:** IAM Configuration | Cloud Identity Governance  
**Environment:** Microsoft Entra ID (Free Tenant + P2 Trial)  
**Simulated Org:** Riverview Medical Center (fictional healthcare environment)

---

## Overview

This project documents the configuration and analysis of Microsoft Entra ID in a simulated healthcare organization. The work covers user provisioning, group-based RBAC, password policy enforcement, and a documented architectural comparison between cloud and on-premises Active Directory identity management.

---

## What I Built

### 1. Tenant Setup & User Provisioning
- Created and configured a Microsoft Entra ID tenant scoped to a fictional hospital
- Provisioned users across clinical, administrative, and IT roles
- Organized users into security groups with defined access boundaries

### 2. Group-Based RBAC
- Assigned roles to groups rather than individual users, enforcing least-privilege principles
- Documented role assignment scope and separation of duties across job functions

### 3. Password Policy Configuration
- Configured tenant-wide password policy including lockout threshold and duration
- Implemented a custom banned password list targeting predictable, role-referencing credentials (aligned to NIST IA-5)
- Configured Password Protection in Audit mode prior to enforcement, following change management best practice

### 4. Hybrid Architecture Analysis
- Identified that Entra ID enforces password policies uniformly at the tenant level
- Compared this to on-premises Active Directory, where fine-grained password policies (FGPP) can be scoped per group
- Documented this distinction as an architectural consideration for organizations operating in hybrid environments

### 5. Licensing Observation
- Documented that Conditional Access policies and Privileged Identity Management (PIM) require Entra ID P2 licensing
- Noted this as a key scoping consideration for hybrid IAM platform decisions and budget planning

---

## Key Findings

| Finding | Detail |
|---|---|
| Password policy scope | Entra ID applies one policy tenant-wide; on-prem AD supports per-group FGPP |
| Custom banned passwords | Enabled and populated with role/org-referencing terms to block weak credentials |
| Password protection mode | Set to Audit (not Enforced) to observe impact before production rollout |
| P2 licensing dependency | Conditional Access and PIM unavailable without Entra ID P2 — documented as a platform scoping factor |

---

## Frameworks Referenced

- NIST SP 800-53 IA-5 (Authenticator Management)
- Microsoft Security Best Practices for Entra ID

---

## Skills Demonstrated

`Microsoft Entra ID` `RBAC` `Password Policy` `Hybrid IAM` `NIST IA-5` `Conditional Access` `Entra ID P2` `Identity Governance` `Change Management`
