# Microsoft Entra Conditional Access + MFA Lab

## Status

Complete (screenshots pending — to be added in a future update)

## Type

Hands-On Identity & Access Lab

---

## Objective

This lab demonstrates how Microsoft Entra ID Conditional Access can enforce identity-based security controls in a simulated healthcare organization.

The environment was built for a fictional healthcare company, **Harborview Health Partners**. The lab includes cloud-only test users, security groups, a break-glass account, named locations, and Conditional Access policies for MFA enforcement, legacy authentication blocking, location-based access control, and administrative role protection.

---

## Environment

- **Platform:** Microsoft Entra ID
- **License:** Microsoft Entra ID P2 Trial
- **Organization (Fictional):** Harborview Health Partners
- **Identity Type:** Cloud-only users
- **Testing Mode:** Report-only and limited enforcement testing

---

## Lab Scenario

Harborview Health Partners needed stronger identity security controls to reduce the risk of account compromise. The lab simulates how an organization can use Conditional Access to require multifactor authentication, block legacy authentication, and protect privileged access.

---

## Test Users and Groups

Test users were created to represent different roles in the organization, including regular staff, clinical staff, IT admins, HR/billing users, and a break-glass emergency admin account.

Security groups were created to scope Conditional Access policies:

- `GRP-CA-MFA-AllStaff`
- `GRP-CA-BreakGlass-Exclude`
- `GRP-CA-IT-Admins`
- `GRP-CA-ClinicalStaff`
- `GRP-CA-HR-Billing`

---

## Conditional Access Policies

The following Conditional Access policies were created and validated:

| Policy | Scope | Control | Final State |
|---|---|---|---|
| CA001 - Require MFA for All Staff | GRP-CA-MFA-AllStaff, excluding GRP-CA-BreakGlass-Exclude | Require multifactor authentication | Tested On, then returned to Report-only |
| CA002 - Block Legacy Authentication | GRP-CA-MFA-AllStaff, excluding GRP-CA-BreakGlass-Exclude | Block legacy authentication clients | Report-only |
| CA003 - Require MFA Outside Trusted Location | GRP-CA-MFA-AllStaff, excluding GRP-CA-BreakGlass-Exclude | Require MFA outside trusted network | Report-only |
| CA004 - Require MFA for Admin Roles | Selected admin roles, excluding break-glass/current admin during testing | Require multifactor authentication | Report-only |

---

## Named Location

A trusted named location was created to represent the admin home network. This was used to demonstrate location-based Conditional Access logic.

---

## Break-Glass Account Consideration

A break-glass emergency admin account was created and placed into an exclusion group. This account was excluded from Conditional Access policies to reduce the risk of tenant lockout during policy testing.

---

## Testing and Validation

Policy behavior was validated using:

- Report-only Conditional Access evaluation
- MFA registration prompt
- Successful MFA sign-in
- Microsoft Entra sign-in logs
- Conditional Access activity details

CA001 was temporarily enabled to validate real MFA enforcement, then returned to Report-only mode after successful testing to reduce the risk of accidental lockout.

---

## Security Takeaways

- Conditional Access policies should be tested in Report-only mode before enforcement.
- Break-glass accounts should be excluded from restrictive policies and monitored closely.
- Legacy authentication should be blocked because it cannot properly satisfy modern MFA requirements.
- MFA enforcement should be scoped carefully using groups.
- Sign-in logs are critical for validating policy behavior.

---

## What I'd Do Differently in Production

- **Phased rollout for CA001 (MFA for All Staff)** — In production, MFA enforcement would be deployed in phases (pilot group first, then department waves over 2–4 weeks) with helpdesk staffing increased during cutover and daily sign-in log review during rollout.
- **Admin-role policies first, regardless of user MFA timeline** — CA004 (Admin Roles) protects the highest-impact accounts and should be deployed before broad-user MFA rollout, not in parallel.
- **Documented break-glass procedures** — The break-glass account exclusion is necessary for tenant lockout protection, but in production it requires a documented procedure for credential storage, sign-in monitoring, and periodic review to prevent the exclusion itself becoming the attack path.
- **Conditional Access What-If tool** — Before enforcement, the What-If tool should be used to validate policy behavior against representative user/device combinations to surface unintended impacts.

---

## Screenshots

Screenshots from the original lab session are being prepared and will be added in a future update to this README.

---

## Notes

This is a self-built lab in a Microsoft Entra ID P2 trial tenant. Users, groups, and the Harborview Health Partners scenario are invented for demonstration purposes. No real user data, organizational data, or sensitive information is present.
