# Microsoft Entra PIM Lab

## Status

Completed

## Type

Identity and Access Management Lab / Privileged Access Management Case Study

## Objective

This lab demonstrates how Microsoft Entra Privileged Identity Management can reduce standing administrative access by requiring eligible users to activate privileged roles only when needed.

The goal was to simulate a realistic just-in-time privileged access workflow for IT support operations, including role eligibility, activation requirements, approval, justification, ticket information, and audit validation.

## Environment

- Platform: Microsoft Entra ID
- License: Microsoft Entra ID P2 Trial
- Organization: Harborview Health Partners
- Feature: Privileged Identity Management
- Test user: Mike Iverson
- Reviewer/Approver: Brian Johnson
- Roles tested:
  - Helpdesk Administrator
  - Authentication Administrator

## Lab Scenario

Harborview Health Partners wants to reduce standing privileged access for service desk and IAM support staff.

Instead of granting permanent administrative rights, selected IT support users are made eligible for privileged roles through Microsoft Entra Privileged Identity Management. When elevated access is needed, the user must activate the role, provide a business justification, include ticket information, satisfy MFA, and receive approval.

This lab simulates a service desk support scenario where an analyst requests temporary privileged access to perform an account recovery task after validating the user.

## Roles Onboarded to PIM

| Role | Purpose |
|---|---|
| Helpdesk Administrator | Supports service desk tasks such as password reset and user support workflows |
| Authentication Administrator | Supports authentication method and MFA-related account recovery workflows |

## Role Configuration

| Role | Assignment Type | Max Activation Duration | MFA Required | Justification Required | Ticket Required | Approval Required | Approver |
|---|---|---:|---|---|---|---|---|
| Helpdesk Administrator | Eligible | 8 hours | Yes | Yes | Yes | Yes | `GRP-PIM-Approvers` |
| Authentication Administrator | Eligible | 4 hours | Yes | Yes | Yes | Yes | `GRP-PIM-Approvers` |

## Eligible Assignments

| User | Role | Assignment State |
|---|---|---|
| Mike Iverson | Helpdesk Administrator | Eligible |
| Mike Iverson | Authentication Administrator | Eligible |

## Activation Workflow Demonstrated

Mike Iverson activated the eligible Helpdesk Administrator role through Microsoft Entra PIM.

The activation request required:

- Azure MFA
- Business justification
- Ticket information
- Approval before activation
- Time-bound access

Example ticket number used:

`HHP-INC-1007`

Example justification used:

`Temporary elevation requested to perform service desk account recovery task for a validated user support case.`

## Approval Workflow Demonstrated

The Helpdesk Administrator role was configured to require approval before activation.

The activation request was reviewed and approved by the configured approver group. After approval, PIM completed the role activation and Mike Iverson received temporary active access to the Helpdesk Administrator role.

Approval reason:

`Approved for time-bound service desk support task after user validation.`

## Audit Log Validation

PIM audit history was reviewed to validate the privileged access workflow.

The audit log showed successful events for:

- Updating PIM role settings
- Adding eligible role assignments
- Requesting role activation
- Approving the activation request
- Completing the role activation

This confirms that the privileged access workflow was auditable from assignment through activation.

## Integration with Access Reviews

This lab connects to the Access Review process by showing how eligible privileged access should be reviewed periodically.

Eligible assignments such as Helpdesk Administrator and Authentication Administrator should not be granted indefinitely without review. In production, privileged role eligibility should be reviewed on a recurring basis to confirm that users still require the ability to activate those roles.

This supports least privilege and helps prevent privilege creep.

## Security Takeaways

- Privileged roles should not be permanently active by default.
- PIM supports just-in-time privileged access.
- Eligible assignments reduce standing administrative privilege.
- MFA, justification, ticket information, and approval strengthen privileged access workflows.
- PIM audit logs provide evidence of privileged role assignment and activation activity.
- Help desk and IAM workflows should use task-specific roles instead of broad administrator roles whenever possible.
- Privileged access should be reviewed periodically through access reviews.

## What I'd Do Differently in Production

- Use separate dedicated admin accounts instead of daily user accounts.
- Require approval from an IAM manager, security lead, or service owner for sensitive roles.
- Require ticket numbers for all privileged activations.
- Use shorter activation windows for higher-risk roles.
- Send PIM activation events to a SIEM for monitoring and alerting.
- Configure alerts for repeated activations, after-hours activations, and high-risk role activations.
- Review eligible assignments on a recurring schedule.
- Avoid broad roles when more specific roles can satisfy the task.
- Use Privileged Access Groups where appropriate to manage role eligibility at scale.
- Maintain at least one monitored break-glass account outside normal PIM workflows.
- Document standard operating procedures for privileged access requests and approvals.

## Screenshots

| Screenshot | Description |
|---|---|
| ![PIM groups created](./screenshots/01-pim-groups-created.PNG) | PIM-related groups created for eligible users and approvers |
| ![PIM Entra roles overview](./screenshots/02-pim-entra-roles-overview.PNG) | Microsoft Entra roles opened in Privileged Identity Management |
| ![Helpdesk role assignments overview](./screenshots/03-helpdesk-admin-role-assignments-overview.PNG) | Helpdesk Administrator role opened in PIM |
| ![Helpdesk role settings](./screenshots/04-helpdesk-admin-role-settings.PNG) | Helpdesk Administrator settings requiring MFA, justification, ticket information, and approval |
| ![Helpdesk assignment membership](./screenshots/05-helpdesk-admin-add-eligible-assignment-membership.PNG) | Mike Iverson selected for Helpdesk Administrator assignment |
| ![Helpdesk assignment settings](./screenshots/06-helpdesk-admin-eligible-assignment-settings.PNG) | Helpdesk Administrator assignment configured as eligible |
| ![Helpdesk eligible assignment created](./screenshots/07-helpdesk-admin-eligible-assignment-created.PNG) | Mike Iverson added as eligible for Helpdesk Administrator |
| ![Authentication Administrator overview](./screenshots/08-authentication-admin-role-overview.PNG) | Authentication Administrator role opened in PIM |
| ![Authentication Administrator activation settings](./screenshots/09-authentication-admin-activation-settings.PNG) | Authentication Administrator activation settings configured |
| ![Authentication Administrator membership](./screenshots/10-authentication-admin-add-eligible-assignment-membership.PNG) | Mike Iverson selected for Authentication Administrator assignment |
| ![Authentication Administrator assignment settings](./screenshots/11-authentication-admin-eligible-assignment-settings.PNG) | Authentication Administrator assignment configured as eligible |
| ![Authentication Administrator eligible assignment created](./screenshots/12-authentication-admin-eligible-assignment-created.PNG) | Mike Iverson added as eligible for Authentication Administrator |
| ![Mike eligible roles](./screenshots/13-mike-iverson-my-eligible-roles.PNG) | Mike Iverson viewing eligible PIM roles |
| ![Activation request](./screenshots/14-helpdesk-admin-activation-request.PNG) | Helpdesk Administrator activation request with justification and ticket information |
| ![Pending approval](./screenshots/15-helpdesk-admin-activation-pending-approval.PNG) | Activation request pending approval |
| ![Approval request pending](./screenshots/16-pim-approval-request-pending.PNG) | Approver view showing Mike Iverson's pending PIM activation request |
| ![Approval request approved](./screenshots/17-pim-approval-request-approved.PNG) | PIM approval request approved |
| ![Audit approval and activation](./screenshots/18-pim-audit-log-approval-and-activation-success.PNG) | PIM audit log showing approval and activation success |
| ![Active role confirmation](./screenshots/19-helpdesk-admin-active-role-confirmation.PNG) | Helpdesk Administrator role shown as activated for Mike Iverson |
| ![Final audit history](./screenshots/20-pim-final-audit-history.PNG) | Final PIM audit history showing assignment, approval, and activation events |

## Notes

This lab was completed in a Microsoft Entra ID P2 trial tenant using a simulated healthcare organization.

All screenshots were sanitized before publication. Sensitive identifiers such as tenant IDs, personal email addresses, full user principal names, and other unnecessary internal identifiers were redacted.

The lab was designed to demonstrate the security value of just-in-time privileged access, not to grant broad permanent administrative access.
