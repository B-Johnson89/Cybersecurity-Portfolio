# Unauthorized MFA Device / Account Compromise Investigation

## Status

Complete

## Type

Sanitized Real-World Case Study

---

## Overview

This case study documents a sanitized identity and access management investigation involving suspicious authentication activity, an unauthorized MFA device, and account compromise indicators discovered during a routine password reset request.

During the support interaction, a review of the user's MFA profile and authentication activity identified login activity inconsistent with the user's known location, along with an unrecognized phone number added as an MFA method. The findings were escalated to the security team, and containment and recovery actions were completed to secure the account.

---

## My Role

As a Tier 1 service desk agent supporting this MSP client, I was the first point of contact for what initially appeared to be a routine password reset request. My specific contributions to this investigation were:

- Verified the caller's identity using approved identity verification procedures before proceeding with any account actions
- Reviewed the user's MFA profile during the standard reset workflow and identified an unrecognized phone number enrolled as an MFA method
- Compared recent authentication activity against the user's known location and role, identifying geographic inconsistencies
- Recognized the pattern as account compromise indicators rather than a routine reset, and shifted the call from password reset to incident response
- Documented findings and timeline details in the ticketing system as the investigation evolved
- Executed Tier 1 containment per playbook: account disablement and session revocation
- Coordinated warm-handoff escalation to the client security team and provided full context on indicators and actions taken
- Communicated with the affected user about the security team takeover and expected reactivation timeline

The client security team led broader account-activity review, payroll/HR exposure assessment, and any downstream remediation beyond Tier 1 scope.

---

## Objective

Determine whether the account access issue was limited to a routine password reset or whether the user's account showed indicators of compromise requiring security escalation and remediation.

---

## Environment

- **Organization Type:** Higher Education
- **Source:** Service Desk / Security Support
- **Systems Involved:** Identity Management Platform, MFA Administration Portal, Email Platform, Payroll/HR Platform, Ticketing System
- **Data Reviewed:** MFA Device Enrollment, Authentication Activity, Login Geography, User Verification Data, Account Status, Email Account Settings

---

## Severity

High

---

## Detection

The investigation began during what was initially logged as a routine password reset request. While reviewing the user's MFA profile as part of the standard reset workflow, suspicious activity was identified.

### Indicators Observed

- Login activity from an unexpected geographic location
- Unrecognized phone number added as an MFA method on the user's account
- Authentication activity inconsistent with the user's known location and role
- User-reported concerns involving possible broader account compromise during the call
- Account had access to sensitive payroll or financial-related systems during the suspected compromise window

---

## Investigation Steps

1. Verified the user's identity using approved identity verification procedures.
2. Reviewed the user's MFA profile for enrolled devices and contact methods.
3. Identified an unauthorized MFA device associated with the account.
4. Reviewed authentication activity and compared login geography against known user context.
5. Escalated compromise indicators to the security team for validation and containment.
6. Supported review of account activity to determine whether sensitive systems were accessed.
7. Documented findings, sequence of events, user impact, and escalation notes in the ticketing system.

---

## Investigation Sequence

| Step | Event |
|---|---|
| 1 | User contacted support requesting a password reset |
| 2 | Identity verification completed per standard procedure |
| 3 | MFA profile review during reset workflow surfaced unrecognized phone number |
| 4 | Authentication log review confirmed login geography inconsistencies |
| 5 | User confirmed concerns about possible broader compromise |
| 6 | Account scope review identified access to payroll/HR systems |
| 7 | Tier 1 containment executed: account disabled, sessions revoked |
| 8 | Warm handoff to security team with documented indicators and timeline |
| 9 | Security team led broader account-activity review and remediation |
| 10 | Account re-enabled after security verification; ticket closed with full disposition |

---

## Analyst Notes

A few things stood out during this investigation that informed how I prioritized response:

**The MFA profile review caught what the password reset would have missed.** A standard password reset would have changed the credential and ended the call. Reviewing MFA enrollment as part of the reset workflow is what surfaced the unauthorized device — and that's what flipped this from a routine ticket to an incident. That habit of "look at the surrounding identity context, not just the immediate ask" is what I rely on for early compromise detection.

**Geographic inconsistency by itself wasn't conclusive — combined with the new MFA device, it was.** Users travel, work from secondary locations, or use VPNs. A single login from an unexpected location is noise. A new MFA device enrolled from an unexpected location, on an account with access to payroll systems, is a pattern. Compromise detection at Tier 1 is about pattern recognition, not single-indicator alerts.

**The user's own concern accelerated the timeline.** When I asked clarifying questions about recent activity, the user mentioned they'd already had concerns about something feeling off. That shifted my mental model from "I'm investigating to confirm or rule out compromise" to "the user is reporting compromise; I'm investigating to scope it." Different starting assumption, faster containment.

---

## Findings

- The account showed indicators of compromise.
- An unauthorized MFA method had been added to the user's account.
- Authentication activity was inconsistent with the user's known location.
- The suspected compromise window was active for an extended period before detection.
- Sensitive payroll or financial-related systems may have been accessed during the compromise period.
- The incident required cross-team escalation due to the potential exposure of sensitive account information.

---

## Containment & Recovery Support

The following containment and recovery actions were supported or coordinated with the appropriate teams:

- Disabled the affected account during investigation.
- Removed the unauthorized MFA method.
- Reset the user's password.
- Revoked active sessions.
- Reviewed MFA devices and contact information with the user.
- Reviewed email settings for suspicious mailbox rules, auto-forwarding, signatures, auto-replies, or reply-to changes.
- Escalated potential payroll or financial exposure to the appropriate internal team.
- Re-enabled the account after verification and security clearance.
- Documented actions taken and final resolution in the ticketing system.

---

## MITRE ATT&CK Mapping

| Technique | Description |
|---|---|
| T1078 - Valid Accounts | Valid credentials appeared to be used for unauthorized account access. |
| T1098 - Account Manipulation | An unauthorized MFA method was added to the account. |
| T1556.006 - Multi-Factor Authentication | MFA configuration was manipulated or abused as part of the account compromise. |
| T1114 - Email Collection | Email account review was required due to possible unauthorized access and mailbox manipulation risk. |

---

## Outcome

The account was secured, unauthorized MFA access was removed, active sessions were revoked, password recovery was completed, and potential payroll or financial exposure was escalated for review.

---

## Skills Demonstrated

- Identity and Access Management
- MFA Review and Compromise Detection
- Account Compromise Investigation
- Suspicious Authentication Activity Review
- Identity Verification
- Security Escalation and Warm Handoff
- Incident Documentation
- User Impact Assessment
- MITRE ATT&CK Mapping

---

## Lessons Learned

- A routine password reset workflow that includes MFA profile review can surface account compromise that the user has not yet identified — making service desk identity workflows a meaningful early-detection control.
- Unauthorized MFA device enrollment is a high-confidence compromise indicator and should trigger immediate escalation, not gradual investigation.
- Geographic inconsistency on its own is noise; combined with other indicators (new MFA device, unusual access patterns, user-reported concerns) it becomes a high-confidence signal.
- Accounts with access to payroll, HR, or financial systems require expedited escalation timelines because the downstream impact of even a short compromise window is significant.
- Tier 1 service desk and identity support analysts can play an important role in early compromise detection if the workflow allows time for surrounding-context review, not just task completion.

---

## Improvement Recommendations

If I were contributing to a post-incident review for this organization, I would recommend:

- **Automated alerting on MFA device additions from new locations** — A rule that flags MFA device enrollment when the enrollment source location differs from the user's typical login geography would have surfaced this compromise via automated detection rather than relying on a coincidental password reset call.

- **Privileged-data-access tagging for risk-based authentication** — Accounts with access to payroll, HR, or financial systems should carry an attribute that triggers stricter conditional access policies (sign-in frequency, device compliance, location restrictions). This account's elevated data access made the compromise window more impactful than it would have been on a standard user.

- **Service desk playbook expansion for MFA review on resets** — Even where compromise isn't suspected, a brief MFA profile check during password resets is a low-cost detection control that demonstrably caught compromise in this case. Codifying it as a required step in the reset playbook would standardize the practice.

- **User-side compromise reporting clarity** — The user mentioned they'd had concerns "for a while" before calling. Clearer guidance on how and when to report suspected compromise (versus waiting until something forces a call) would shorten compromise windows generally.

---

## Sanitization Notice

This case study is based on real-world experience and has been fully sanitized. Names, dates, ticket numbers, internal identifiers, client-specific details, screenshots, and sensitive information have been removed or generalized. Containment and remediation actions described were executed in coordination with the client security team; investigation scope, decisions, and analyst reasoning reflect my Tier 1 contribution to the broader response.
