# Microsoft Entra Access Review Lab

## Status

Complete (screenshots pending — to be added in a future update)

## Type

Hands-On Identity & Access Lab

---

## Objective

This lab demonstrates how Microsoft Entra ID Governance access reviews can be used to periodically validate group membership for privileged access.

The lab was built in a simulated healthcare organization, **Harborview Health Partners**, and focused on reviewing membership of an IT admin security group.

---

## Environment

- **Platform:** Microsoft Entra ID
- **License:** Microsoft Entra ID P2 Trial
- **Organization (Fictional):** Harborview Health Partners
- **Feature:** Microsoft Entra Access Reviews
- **Review Target:** `GRP-CA-IT-Admins`

---

## Scenario

Harborview Health Partners performs periodic access reviews to confirm that users with elevated IT access still require that access.

The `GRP-CA-IT-Admins` group was selected for review because membership in this group represents elevated administrative access in the lab environment.

---

## Access Review Configuration

| Setting | Value |
|---|---|
| Review name | AR001 - Quarterly Review of IT Admins |
| Reviewed resource | GRP-CA-IT-Admins |
| Review scope | All users |
| Reviewer | Selected admin reviewer |
| Review recurrence | One time |
| Duration | 3 days |
| Auto-apply results | Disabled for lab safety |
| Justification required | Enabled |
| Email notifications | Enabled |
| Reminders | Enabled |

---

## Review Decisions

| User | Decision | Reason |
|---|---|---|
| Mike Iverson | Approved | User still requires IT admin group access for the lab scenario |
| Kobe Manning | Denied | User no longer requires IT admin group access for the current role |

---

## Validation

The access review was validated through the My Access reviewer portal and Microsoft Entra audit logs.

Validation evidence included:

- Access review creation
- Review scope targeting GRP-CA-IT-Admins
- Pending reviewer action in My Access
- Reviewer decisions submitted for two users
- Final results showing one approved user and one denied user
- Audit logs showing create, approve, and deny actions

---

## Security Takeaways

- Privileged access should be reviewed periodically.
- Access reviews help reduce standing access and privilege creep.
- Reviewers should document approval and denial decisions.
- Recommendations should support reviewer judgment, not replace it.
- Auto-apply settings should be tested carefully before production use.
- Access reviews support least privilege and identity governance.

---

## What I'd Do Differently in Production

- **Auto-apply enabled after baseline cycles** — Auto-apply was disabled for lab safety. In production, I would recommend enabling auto-apply after the first 2–3 review cycles establish baseline reviewer reliability and the organization is comfortable that denied access removals won't disrupt legitimate work.
- **Manager notification on denied access** — Denied access in a review should trigger a notification to the user's manager, not just removal, to surface legitimate access needs that should be re-requested through the standard access request process rather than fall through the cracks.
- **Recurring rather than one-time reviews** — A one-time review is appropriate for the lab demonstration, but production should use recurring reviews (quarterly for privileged groups, annually or semi-annually for general groups) to systematically address privilege creep over time.
- **Scoped reviewer roles** — In production, reviewers should typically be the resource owner or the reviewed user's manager rather than a single admin, distributing review responsibility appropriately and avoiding rubber-stamp approvals from a single reviewer.

---

## Screenshots

Screenshots from the original lab session are being prepared and will be added in a future update to this README.

---

## Notes

This is a self-built lab in a Microsoft Entra ID P2 trial tenant. Users, groups, and the Harborview Health Partners scenario are invented for demonstration purposes. No real user data, organizational data, or sensitive information is present.
