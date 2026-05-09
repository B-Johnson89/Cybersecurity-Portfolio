# DocuSign Spoofing / Phishing Investigation

## Status

Complete

## Type

Sanitized Real-World Case Study

---

## Overview

This case study documents a sanitized phishing investigation involving a spoofed document-signing email that directed a user to a fraudulent login portal.

The user reported the suspicious message after interacting with the link and entering credentials. The incident was reviewed as a credential exposure event, escalated to the security team, and remediated through account containment, session revocation, password reset, MFA verification, and email security actions.

---

## My Role

As a Tier 1 service desk agent supporting this MSP client, I was the first point of contact when the affected user called to report the suspicious message after credential entry. My specific contributions were:

- Received the user's initial report and gathered details about the suspicious email and the user's interaction with it
- Reviewed the email content and screenshots provided by the user, analyzing sender domain, branding, and URL structure
- Confirmed the message was a phishing attempt using spoofed document-signing branding
- Confirmed credential entry on the fraudulent portal — the indicator that elevated this from "phishing report" to "active credential exposure"
- Documented findings, sender/domain/URL indicators, user impact, and timeline details in the ticketing system
- Executed Tier 1 containment per playbook: account disable or restriction, session revocation
- Coordinated escalation to the client security team with full documentation of indicators and the scope of credential exposure
- Communicated with the user about expected remediation steps and reactivation timeline
- Provided user guidance on phishing recognition and proper reporting channels for future suspicious messages

The client security team led broader account review, MFA verification follow-through, mailbox setting validation, sender/domain/URL escalation for blocking or filtering, and any external coordination beyond Tier 1 scope.

---

## Objective

Determine whether the reported document-signing email was legitimate or a phishing attempt, assess whether credentials were exposed, and support containment actions to reduce the risk of unauthorized account access.

---

## Environment

- **Organization Type:** Higher Education
- **Source:** User Report / Help Desk
- **Systems Involved:** Identity Management Platform, MFA Platform, Email Platform, Email Security Controls, Ticketing System
- **Data Reviewed:** User Report, Suspicious Email, Sender Domain, URL Indicators, Screenshots, Account Status, MFA Configuration, Mailbox Settings

---

## Severity

High

---

## Detection

The investigation began after a user contacted support to report a suspicious document-signing email after they had already interacted with the link and entered credentials.

### Indicators Observed

- Spoofed document-signing branding designed to mimic a legitimate service
- Suspicious sender domain inconsistent with legitimate document-signing infrastructure
- Obfuscated or misleading phishing URL
- Fraudulent login portal designed to capture credentials
- User confirmed credential entry on the portal
- Potential risk of unauthorized account access using harvested credentials

---

## Investigation Steps

1. Reviewed the user report and gathered available details about the suspicious email.
2. Remotely reviewed the email content and screenshots provided by the user.
3. Analyzed sender information, domain indicators, branding, and URL structure.
4. Determined the message was a phishing attempt using spoofed document-signing branding.
5. Confirmed that credentials had been entered into the fraudulent portal.
6. Escalated the incident to the security team for containment and remediation.
7. Supported account review, MFA verification, and mailbox setting checks.
8. Documented findings, user impact, escalation details, and remediation actions in the ticketing system.

---

## Investigation Sequence

| Step | Event |
|---|---|
| 1 | User contacted support reporting suspicious document-signing email |
| 2 | User disclosed they had clicked the link and entered credentials |
| 3 | Email content and screenshots reviewed for sender, domain, and URL indicators |
| 4 | Confirmed phishing using spoofed document-signing branding |
| 5 | Confirmed credential exposure on fraudulent portal |
| 6 | Tier 1 containment executed: account disabled or restricted, sessions revoked |
| 7 | Warm handoff to security team with documented indicators and exposure scope |
| 8 | Security team led MFA verification, mailbox review, and indicator escalation |
| 9 | Account restored after security verification; user guidance provided |
| 10 | Final disposition documented in ticketing system |

---

## Analyst Notes

A few things stood out during this investigation that informed how I prioritized response:

**Confirmed credential entry changed the urgency.** A phishing report where the user did not click is a different incident than a phishing report where the user entered credentials. The latter is an active credential exposure — by the time the user reports it, the adversary may already have the credentials and be attempting to use them. Containment timing matters in minutes, not hours.

**Spoofed branding from trusted services is high-conversion phishing.** Document-signing platforms, banking portals, and shipping services all rely on user-trust patterns that adversaries exploit. Users who would never click a generic "click here to claim your prize" email will click a "please review and sign this document" email because the cognitive shortcut to trusted-service-equals-real is hard to override. That's why these lures convert.

**The user's quick reporting limited the damage.** The user reported the click within a short window of credential entry, which gave us a meaningful chance to revoke sessions and reset the credential before adversary use. A user who clicks and doesn't report — or reports days later — leaves a much wider exposure window. The user's reporting behavior was itself a partial mitigation, and that's worth reinforcing in user awareness training.

**Sender, domain, and URL indicators needed to leave Tier 1 quickly.** The phishing infrastructure used here would target other users in the same organization or other organizations the MSP supported. Escalating those indicators for blocking or filtering across the client's email security stack — and potentially flagging them for the broader MSP threat-intel feed — was as important as remediating the affected user's account.

---

## Findings

- The email was a phishing attempt using spoofed document-signing branding.
- The phishing URL led to a fraudulent login portal.
- User credentials were exposed through the phishing page.
- A single user account was confirmed as impacted at the time of investigation.
- No confirmed lateral movement was observed during the initial investigation.
- The incident created potential risk if harvested credentials were reused against other systems.
- Sender, domain, and URL indicators required blocking or additional email security review.

---

## Containment & Recovery Support

The following containment and recovery actions were supported or coordinated with the appropriate teams:

- Disabled or restricted the affected account during investigation.
- Revoked active sessions.
- Reset the user's password.
- Verified MFA devices and contact information.
- Reviewed mailbox rules, auto-forwarding, signatures, auto-replies, and reply-to settings for unauthorized changes.
- Escalated sender, domain, and URL indicators for blocking or filtering.
- Notified appropriate stakeholders for containment and follow-up.
- Restored access after security review and account recovery steps were completed.
- Documented final resolution and user guidance in the ticketing system.

---

## MITRE ATT&CK Mapping

| Technique | Description |
|---|---|
| T1566.002 - Spearphishing Link | The user received a phishing email containing a malicious link. |
| T1078 - Valid Accounts | Exposed credentials could enable unauthorized access using valid account credentials. |
| T1056.003 - Input Capture: Web Portal Capture | The spoofed login portal was used to capture credentials. |
| T1114 - Email Collection | Mailbox review was required due to possible unauthorized account access. |

---

## Outcome

The affected account was secured, active sessions were revoked, credentials were reset, MFA details were verified, mailbox settings were reviewed, and sender/domain/URL indicators were escalated for blocking or filtering.

---

## Skills Demonstrated

- Phishing Investigation
- Malicious Email Review
- Credential Exposure Assessment
- Sender and Domain Review
- URL Indicator Review
- Identity and Access Support
- MFA Verification
- Account Containment
- Security Escalation and Warm Handoff
- Incident Documentation
- MITRE ATT&CK Mapping
- User Guidance and Communication

---

## Lessons Learned

- Spoofed branding from trusted services (document-signing, banking, shipping) converts at higher rates than generic phishing because it exploits established user-trust patterns. Awareness training that specifically addresses these high-conversion lures is more effective than generic "be cautious of phishing" messaging.
- Credential entry on a phishing portal should be treated as an active exposure event with minutes-level containment urgency, not as a routine phishing report.
- The user's quick self-reporting after credential entry meaningfully reduced the exposure window. Reinforcing fast-reporting behavior in user training is itself a security control.
- Phishing investigation should produce blockable indicators (sender, domain, URL) that get pushed to email security and any shared threat intelligence quickly, since the same infrastructure is likely targeting other users.
- Account recovery after credential exposure should always include MFA device verification, mailbox setting review, and session revocation — not just password reset — because the adversary may have already used the credential to alter account state.

---

## Improvement Recommendations

If I were contributing to a post-incident review for this organization, I would recommend:

- **Display-name-spoofing detection rules** — Email security tooling can be configured to flag inbound emails using display names or sender patterns that mimic trusted services (e.g., "DocuSign," "Adobe Sign") from non-legitimate sender domains. This would have provided automated pre-delivery detection.

- **Targeted awareness training on document-signing and shipping lures** — Generic phishing awareness training under-performs compared to training that specifically addresses the high-conversion lure categories (document-signing, package delivery, banking, payroll). Training cycles refreshed against current campaign trends would close the user-recognition gap on these specific patterns.

- **Conditional access on credential-event behavior** — When a credential is reset following a confirmed exposure event, conditional access policies should be temporarily tightened on the affected account (require MFA on every sign-in, restrict to compliant devices, require sign-in from trusted locations) for a defined recovery window before relaxing back to standard policy.

- **Sender/domain/URL indicator sharing across MSP clients** — In an MSP environment, an indicator that targets one client is highly likely to target others. A shared threat-intel feed that propagates confirmed phishing indicators across client tenants would limit campaign scale across the MSP's customer base.

- **Auto-acknowledgment for users who self-report after clicking** — Users who self-report after credential exposure are doing exactly what security wants them to do, but the experience often involves an account lockout that feels punitive. A clearer communication flow — acknowledging the report, explaining the lockout is protective, providing a clear reactivation timeline — reinforces self-reporting behavior over time.

---

## Sanitization Notice

This case study is based on real-world experience and has been fully sanitized. Names, dates, departments, ticket numbers, internal identifiers, screenshots, client-specific details, domains, reporting addresses, and sensitive information have been removed or generalized. Containment and remediation actions described were executed in coordination with the client security team; investigation scope, decisions, and analyst reasoning reflect my Tier 1 contribution to the broader response.
