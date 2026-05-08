# Microsoft Entra ID: IAM Configuration & Hybrid Architecture Analysis

**Lab Type:** IAM Configuration | Cloud Identity Governance  
**Environment:** Microsoft Entra ID (Free Tenant + P2 Trial)  
**Simulated Org:** Riverview Regional Medical Center (fictional healthcare environment)

---

## Overview

This project documents the configuration and analysis of Microsoft Entra ID in a simulated healthcare organization. The work covers user provisioning, group-based RBAC, password policy enforcement, Conditional Access policy configuration, and a documented architectural comparison between cloud and on-premises Active Directory identity management.

---

## What I Built

### 1. User Provisioning

Created and configured users across clinical, administrative, and IT roles within the Riverview Regional Medical Center tenant. Each user was provisioned with a defined job title, department, and user principal name scoped to the organization domain.

**Creating Dr. James Carter — Attending Physician (Clinical)**
![Creating Dr. James Carter](images/Creating_Dr__J__Carter_User.png)

**Complete User Roster — 6 users provisioned across roles**
![Complete Users](images/Complete_users_for_Riverview_Regional.png)

---

### 2. Group-Based RBAC

Organized users into security groups aligned to job function. Roles were assigned at the group level rather than to individual users, enforcing least-privilege principles and reducing administrative overhead.

**Dr. James Carter assigned to the Physicians security group**
![Physician Group](images/Dr_J__Carter-Physician_group.png)

---

### 3. Conditional Access Policies

Configured Conditional Access policies using Entra ID P2 to enforce MFA and risk-based access controls. All policies were set to **Report-only mode** following change management best practices — observing impact before pushing to enforcement.

**Granting Policy — MFA required for access to all cloud resources**
![Granting Policy](images/Granting_Policy.png)

**Require MFA for IT Admins — Sign-in risk conditions (High + Medium)**
![Sign-in Risk](images/Sign-in_Risk_for_A__Rivera.png)

**Location Condition scoped to Alex Rivera**
![Location Condition](images/Location_Condition_for_A__Rivera.png)

**Policy targeting Alex Rivera — Report-only, Users and Groups scoped**
![Policy for Rivera](images/Policy_for_A__Rivera2.png)

---

### 4. Password Policy Configuration

Configured tenant-wide password protection including custom banned passwords and lockout settings. Documented the architectural distinction between Entra ID and on-premises Active Directory password policy scoping.

**Password Protection settings — custom banned list, Audit mode enabled**
![Password Protection](images/Password_Protection_settings.png)

**Key finding:** Entra ID applies password policies uniformly at the tenant level. Unlike on-premises Active Directory, where Fine-Grained Password Policies (FGPP) can be scoped per group, Entra ID has no per-group scoping capability. This is a critical architectural consideration for organizations operating in hybrid environments.

Custom banned password list aligned to **NIST SP 800-53 IA-5 (Authenticator Management)** — preventing role-referencing and org-specific weak credentials.

Password Protection for Windows Server AD was left in **Audit mode**, not Enforced — following the principle of observing impact before production rollout.

---

### 5. Audit Logging

Reviewed audit logs to verify all user management and password policy changes were captured and traceable. All provisioning and policy update events logged with Success status under the UserManagement category.

**Audit Logs — user provisioning and password policy update events**
![Audit Logs](images/Audit_Logs_1.png)

---

## Key Findings

| Finding | Detail |
|---|---|
| Password policy scope | Entra ID applies one policy tenant-wide; on-prem AD supports per-group FGPP |
| Custom banned passwords | Populated with role/org-referencing terms to block predictable credentials |
| Password protection mode | Set to Audit — best practice before moving to Enforced |
| Conditional Access | Set to Report-only — change management best practice |
| P2 licensing dependency | Conditional Access and PIM require Entra ID P2 — documented as a platform scoping factor |
| Audit trail | All provisioning and policy changes captured in Entra audit logs with Success status |

---

## Frameworks Referenced

- NIST SP 800-53 IA-5 (Authenticator Management)
- Microsoft Zero Trust and Conditional Access best practices
- Microsoft Security Baseline for Entra ID

---

## Skills Demonstrated

`Microsoft Entra ID` `RBAC` `User Provisioning` `Group Management` `Password Policy` `Conditional Access` `MFA` `Sign-in Risk` `NIST IA-5` `Hybrid IAM` `Entra ID P2` `Audit Logging` `Identity Governance` `Change Management`
