# Credential Harvesting Campaign Investigation

## Status

Complete

## Type

Sanitized Real-World Case Study

---

## Overview

This case study documents a sanitized security investigation involving a credential harvesting campaign that used a compromised internal account to send suspicious emails to multiple users.

The campaign used a fraudulent account-renewal lure to direct recipients to a malicious form designed to collect login credentials and personal information. Multiple user reports across support channels helped identify the campaign, confirm suspicious activity, and support escalation to the security team for containment.

---

## My Role

As a Tier 1 service desk agent supporting this MSP client, I was one of multiple agents handling user reports during this campaign. My specific contributions were:

- Triaged user reports of suspicious emails received through phone and chat channels
- Verified that the suspicious emails originated from a trusted internal sender — the indicator that elevated this from routine phishing to potential compromise
- Reviewed the malicious URL and account-renewal form structure for credential harvesting indicators
- Recognized the cross-channel reporting pattern that suggested broader campaign rather than isolated phishing
- Documented user reports, observed indicators, and timeline details in the ticketing system
- Executed Tier 1 containment per playbook on the confirmed compromised internal account: account disable and session revocation
- Coordinated escalation to the client security team with full documentation of indicators, affected users I was aware of, and remediation actions taken

The client security team led broader campaign analysis, threat-hunting across the tenant for additional compromised accounts, mailbox-rule remediation across affected users, and any external coordination beyond Tier 1 scope.

---

## Objective

Determine whether reported suspicious emails were isolated phishing attempts or part of a broader credential harvesting campaign involving compromised accounts, malicious links, and unauthorized mailbox changes.

---

## Environment

- **Organization Type:** Higher Education
- **Source:** Service Desk / Security Support
- **Systems Involved:** Identity Management Platform, MFA Platform, Email Platform, Ticketing System
- **Data Reviewed:** User Reports, Email Indicators, Malicious URL, Account Status, MFA Activity, Mailbox Rules, Forwarding Settings

---

## Severity

High

---

## Detection

The investigation began after multiple users reported suspicious emails through phone and chat support channels.

### Indicators Observed

- Suspicious email sent from a trusted internal account
- Malicious URL leading to a fraudulent account-renewal form
- Form designed to collect credentials and personal information
- Altered mailbox forwarding settings in compromised accounts
- Multiple users reporting the same suspicious message across different support channels

---

## Investigation Steps

1. Reviewed user reports received through phone and chat support channels.
2. Confirmed the suspicious email originated from a trusted internal account.
3. Reviewed the malicious URL and account-renewal lure for credential harvesting indicators.
4. Verified the compromised account status in the identity management platform.
5. Reviewed MFA activity and account access indicators where available.
6. Identified suspicious mailbox forwarding behavior associated with compromised accounts.
7. Coordinated escalation to the security team for session revocation, account containment, and broader campaign review.
8. Documented user reports, observed indicators, escalation details, and remediation actions in the ticketing system.

---

## Investigation Sequence

| Step | Event |
|---|---|
| 1 | Initial user report received via chat channel — flagged suspicious email |
| 2 | Second report received via phone channel referencing similar message |
| 3 | Pattern recognized; began investigating sender account status |
| 4 | Additional reports received across channels; campaign hypothesis confirmed |
| 5 | Internal sender confirmed compromised via authentication and account review |
| 6 | URL and form structure reviewed and confirmed as credential harvesting |
| 7 | Mailbox forwarding behavior identified on compromised account |
| 8 | Tier 1 containment executed: account disabled, sessions revoked |
| 9 | Warm handoff to security team with documented campaign indicators |
| 10 | Security team led broader tenant review and downstream remediation |

---

## Analyst Notes

A few things stood out during this investigation that informed how I prioritized response:

**Cross-channel reporting was the key signal.** A single phishing report is routine. Two reports of similar content within a short window, arriving via different channels (chat and phone), is a different problem — it suggests the message is widespread enough that multiple users hit it independently. That pattern is what flipped my mental model from "isolated phishing" to "potential campaign with a compromised internal account."

**The internal sender changed the threat model.** Phishing from external spoofed addresses is common and gets filtered or flagged by email security. Phishing from a real internal account that passed authentication is a fundamentally different problem — it means at least one account is already compromised, the message will land in inboxes with full sender legitimacy, and other users are far more likely to click. That's why the escalation needed to be fast.

**Mailbox forwarding rules were the next thing I looked for.** Once I suspected a compromised internal account, mailbox rule review became priority. Adversaries commonly add forwarding rules during the post-compromise persistence phase to maintain visibility into responses or to exfiltrate sensitive replies. Finding one would confirm both compromise and adversary intent. This case had altered forwarding behavior, which validated the hypothesis.

**Some users reported the message before clicking it.** That's worth noting because user-reporting infrastructure (a "Report Phishing" button, awareness training, easy reporting paths) is itself a security control. In this case, the early reports from users who didn't click accelerated campaign recognition by an unknown but meaningful margin.

---

## Findings

- The suspicious emails were part of a broader credential harvesting campaign.
- A trusted internal account was used to increase legitimacy and improve the likelihood of user interaction.
- The phishing form attempted to collect login credentials and personal information.
- Multiple users received the same or similar phishing email.
- Some users reported the message before interacting with the malicious link, helping accelerate campaign validation.
- Compromised accounts showed signs of unauthorized mailbox forwarding behavior.
- Additional account review was required to identify and secure affected users.

---

## Containment & Recovery Support

The following containment and recovery actions were supported or coordinated with the appropriate teams:

- Disabled confirmed compromised accounts.
- Revoked active sessions.
- Removed malicious mailbox forwarding rules.
- Reset affected user passwords.
- Cleared or reset compromised account recovery/security data where applicable.
- Reviewed mailbox rules, signatures, auto-replies, and reply-to settings for unauthorized changes.
- Escalated affected accounts and campaign indicators to the security team.
- Advised affected users to review sensitive account settings where financial or payroll-related access may have been exposed.
- Documented campaign details, user reports, affected accounts, and resolution steps in the ticketing system.

---

## MITRE ATT&CK Mapping

| Technique | Description |
|---|---|
| T1566.002 - Spearphishing Link | Users received phishing emails containing a malicious link. |
| T1056.003 - Input Capture: Web Portal Capture | The phishing form attempted to collect credentials and personal information. |
| T1078 - Valid Accounts | Compromised accounts were used to send messages and increase trust. |
| T1114 - Email Collection | Mailbox review was required due to possible unauthorized access and forwarding rule abuse. |
| T1098 - Account Manipulation | Unauthorized forwarding rules or account setting changes were identified. |

---

## Outcome

The campaign was contained after compromised accounts were identified, affected sessions were revoked, malicious forwarding rules were removed, passwords were reset, and the security team was notified for broader review and follow-up.

---

## Skills Demonstrated

- Security Operations
- Phishing Investigation
- Credential Harvesting Analysis
- Account Compromise Review
- User Report Validation and Pattern Recognition
- Email Indicator Review
- Mailbox Rule Review
- Identity and Access Support
- Security Escalation and Warm Handoff
- Incident Documentation
- MITRE ATT&CK Mapping

---

## Lessons Learned

- In this incident, automated email security let the message through because it came from an authenticated internal sender. User reporting was the only detection mechanism that worked — which reinforces that user-reporting infrastructure (in-client report button, awareness training, easy reporting paths) is itself a security control, not just a nice-to-have.
- Phishing originating from authenticated internal accounts is meaningfully more dangerous than externally spoofed phishing because it bypasses sender-reputation controls and arrives with full organizational legitimacy.
- Cross-channel correlation of reports (chat, phone, ticketing) accelerated campaign recognition. A SOAR or ticketing-system rule that auto-correlates similar reports across channels would compress this further.
- Mailbox forwarding rule review should be standard during account compromise investigations, as forwarding rules are a common adversary persistence and exfiltration mechanism.
- Reports from users who did not click the link were disproportionately valuable for campaign containment, because they arrived earlier than reports from users who did click and then realized.

---

## Improvement Recommendations

If I were contributing to a post-incident review for this organization, I would recommend:

- **Internal-sender-with-external-link detection rules** — Email security tooling can be configured to flag emails from authenticated internal senders that contain external links to credential-collection forms or unfamiliar domains. This would have provided automated detection independent of user reports.

- **SOAR-based phishing report correlation** — Manual correlation of similar reports across chat, phone, and ticketing channels takes time and depends on individual analyst pattern recognition. A SOAR playbook that auto-correlates user phishing reports by indicator (sender, subject, URL hash) would compress the campaign-recognition window from manual analyst recognition to near-real-time.

- **Continuous mailbox rule auditing** — Instead of reviewing mailbox rules only during incidents, periodic auditing of newly-created forwarding rules across the tenant would surface compromise indicators earlier in the persistence phase, before the adversary uses the foothold to launch campaigns.

- **Phishing-report response acknowledgment** — Users who reported the suspicious email before clicking it provided the most valuable early-warning signal. A lightweight automated acknowledgment thanking those users (and confirming the report is being investigated) reinforces the reporting behavior and improves the user-detection control over time.

- **Risk-based conditional access on internal senders** — Standard internal accounts compromised in campaigns like this could trigger anomaly-based conditional access controls (unusual send volume, unusual recipient patterns) that limit campaign scale even if the compromise itself isn't immediately detected.

---

## Sanitization Notice

This case study is based on real-world experience and has been fully sanitized. Names, dates, ticket numbers, internal identifiers, screenshots, client-specific details, and sensitive information have been removed or generalized. Containment and remediation actions described were executed in coordination with the client security team; investigation scope, decisions, and analyst reasoning reflect my Tier 1 contribution to the broader response.
