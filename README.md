# Microsoft Entra ID: Identity Lifecycle Management Governance Program

**Environment:** Microsoft Entra ID | PowerShell 7.6 | Microsoft Graph SDK  
**Simulated Organization:** Riverview Regional Medical Center  
**Scope:** 25 users | 6 enterprise applications | 5 Conditional Access policies | Full JML lifecycle  
**Framework Mapping:** NIST SP 800-53 Rev. 5  

---

## Overview

This project demonstrates end-to-end identity governance in a live Microsoft Entra ID environment built for a simulated healthcare enterprise. It covers the full identity lifecycle from provisioning through offboarding, with Privileged Identity Management, enterprise application governance, formal access reviews, and Zero Trust Conditional Access enforcement.

Every phase was automated with PowerShell and Microsoft Graph where appropriate and documented with audit-style evidence. The work reflects how IAM governance operates in regulated industries where identity controls directly impact compliance, data security, and operational continuity.

---

## Business Problem

Enterprises in regulated industries face a consistent identity governance problem: too many identities, too little process. Accounts get provisioned without owners. Privileged access never gets revoked. Contractors stay active past their end dates. Access reviews are checkbox exercises with no documented evidence.

This project builds the governance infrastructure that solves that problem: automated provisioning, just-in-time privilege, formal access reviews, and Zero Trust enforcement documented to audit standards.

---

## Environment

| Component | Details |
|---|---|
| Identity Platform | Microsoft Entra ID (Free Developer Tenant) |
| Tenant | RiverviewRegionalMedicalCen.onmicrosoft.com |
| User Population | 25 users across Clinical, Operations, IT, Cybersecurity, Contractors |
| Applications | Epic EHR, Workday, ServiceNow, Microsoft Teams, SharePoint Online, Microsoft Defender |
| Automation | PowerShell 7.6.1, Microsoft Graph SDK |

---

## Project Timeline

### Day 1 — Automated User Provisioning

Provisioned 25 users across 5 workforce segments using a PowerShell script with the Microsoft Graph SDK. Administrative Units were created first to enforce department-scoped admin permissions as a least privilege control before any users were added.

**What was built:**
- 4 Administrative Units (Clinical, IT, Operations, Contractors)
- 25 users provisioned via bulk CSV-driven script
- Role-based group assignments for all users
- Audit log review confirming all provisioning events

**NIST Mapping:** AC-2 (Account Management), IA-12 (Identity Proofing), AC-3 (Access Enforcement)

---

### Day 2 — Privileged Identity Management (PIM)

Configured Microsoft Entra PIM to enforce just-in-time access for six privileged directory roles. No privileged role is permanently assigned. All activations require MFA and written business justification and expire after 1 hour.

**What was built:**
- PIM Eligible assignments for Global Admin, Security Admin, User Admin, Compliance Admin, Privileged Role Admin, Cloud App Admin
- Activation policy: MFA required, justification required, 1-hour maximum
- Microsoft Security alert emails reviewed and documented

**NIST Mapping:** AC-6 (Least Privilege), IA-5 (Authenticator Management), AU-2 (Event Logging)

---

### Day 3 — Enterprise Application Assignment

Assigned all 25 users to 6 enterprise applications based on role requirements. A fix script first created app roles on non-gallery applications before bulk assignments ran, which is a real production pattern that most tutorials skip.

**What was built:**
- App role creation for Epic EHR, Workday, ServiceNow (custom non-gallery apps)
- Bulk user-to-app assignments via PowerShell
- Assignment validation through user portal and admin center

**NIST Mapping:** AC-2 (Account Management), AC-3 (Access Enforcement), CM-7 (Least Functionality)

---

### Day 4 — Formal Access Review Implementation

Created 5 access reviews targeting clinical, IT, security, and contractor groups. Group owners were designated as reviewers, a governance design choice that puts access decisions with business owners, not just IT. Completed the Physicians Group review as Dr. James Carter through myapps.microsoft.com to generate real audit evidence.

**What was built:**
- 5 access reviews via PowerShell (Physicians, Nursing, IT, Cybersecurity, Contractors)
- Group owner as reviewer business-driven access governance model
- Access review completed and decisions documented as audit evidence

**NIST Mapping:** AC-2(10) (Shared Accounts), CA-7 (Continuous Monitoring)

---

### Day 5 — Contractor Offboarding Automation

Executed a multi-user offboarding workflow for 2 contractors using a CSV-driven PowerShell script. The script handled a real-world edge case: one contractor was already in an offboarded state. Instead of failing, it logged the condition and continued — that error handling is what separates a production script from a lab script.

**What was built:**
- CSV-driven offboarding script with multi-user support
- Offboarding actions: account disable, group removal, app assignment revocation
- Graceful error handling for pre-existing offboarded accounts
- JML (Joiners/Movers/Leavers) process documented end-to-end

**NIST Mapping:** AC-2(3) (Disable Inactive Accounts), PS-4 (Personnel Termination), IA-4 (Identifier Management)

---

### Day 6 — Zero Trust Conditional Access Enforcement

Disabled security defaults and deployed 5 Conditional Access policies to enforce Zero Trust across the tenant. MFA enforcement was confirmed by live testing with a provisioned user account.

**Policies deployed:**

| Policy | Scope | Action |
|---|---|---|
| Require MFA for All Users | All users, all cloud apps | Require MFA |
| Require MFA for Privileged Roles | Global Admin, Security Admin, User Admin | Require MFA |
| Block Legacy Authentication | All users — IMAP, POP3, SMTP, Basic Auth | Block |
| Block High Risk Sign-ins | Risk level: High (Identity Protection) | Block |
| Require MFA for PIM Activation | All PIM eligible role activations | Require MFA |

MFA enforcement confirmed by testing with Diana Reyes's account. Legacy auth block validated.

**NIST Mapping:** AC-17 (Remote Access), IA-5 (Authenticator Management), SI-4 (System Monitoring)

---

## NIST SP 800-53 Control Summary

| Control | Name | Phase |
|---|---|---|
| AC-2 | Account Management | Days 1, 4, 5 |
| AC-2(3) | Disable Inactive Accounts | Day 5 |
| AC-3 | Access Enforcement | Days 1, 3 |
| AC-6 | Least Privilege | Day 2 |
| AC-17 | Remote Access | Day 6 |
| AU-2 | Event Logging | Days 2, 6 |
| CA-7 | Continuous Monitoring | Day 4 |
| CM-7 | Least Functionality | Day 3 |
| IA-4 | Identifier Management | Days 1, 5 |
| IA-5 | Authenticator Management | Days 2, 6 |
| IA-12 | Identity Proofing | Day 1 |
| PS-4 | Personnel Termination | Day 5 |
| SI-4 | System Monitoring | Day 6 |

---

## Key Scripts

| Script | Purpose | Phase |
|---|---|---|
| `provision-users.ps1` | Bulk user provisioning via Graph SDK | Day 1 |
| `configure-pim.ps1` | PIM eligible role assignments | Day 2 |
| `assign-apps.ps1` | Enterprise app role creation and bulk assignment | Day 3 |
| `create-access-reviews.ps1` | Access review creation via Graph API | Day 4 |
| `offboard-contractors.ps1` | CSV-driven multi-user offboarding with error handling | Day 5 |
| `deploy-conditional-access.ps1` | Zero Trust CA policy deployment | Day 6 |

---

## Governance Report

The full governance and security assessment report for this engagement is available in `/docs/RRMC_IAM_Governance_Report.docx`. It includes NIST control mapping, findings, recommendations, and an authentication protocol comparison.

---

## Companion Project

**Day 7 — Federation, OAuth 2.0 / OIDC, and Token Governance**  
SAML SSO federation with Salesforce, OAuth 2.0 and OIDC implementation via Microsoft Graph, JWT claims analysis, and PowerShell app registration automation.  
See: [riverview-federation-lab](https://github.com/FabCloudTech/riverview-federation-lab)

---

## Skills Demonstrated

Identity Lifecycle Management | Privileged Access Management | Zero Trust Architecture | PowerShell Automation | Microsoft Graph SDK | Access Reviews | JML Process Design | NIST SP 800-53 | Healthcare IAM Governance | Entra ID Administration

---

*Fabella Terry | IAM Governance Analyst | [fabcloudtech.github.io](https://fabcloudtech.github.io)*
