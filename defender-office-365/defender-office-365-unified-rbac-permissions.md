---
layout: Conceptual
title: Unified RBAC permissions for Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/defender-office-365-unified-rbac-permissions
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Quick reference for Microsoft Defender unified RBAC permissions mapped to Defender for Office 365 features, including threat policies, investigation, quarantine, and reporting.
ms.service: defender-office-365
author: chrisda
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: reference
ms.date: 2026-07-10T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 0d29a5d7-8ee5-6d49-5db0-8f4862ac00a6
document_version_independent_id: 0d29a5d7-8ee5-6d49-5db0-8f4862ac00a6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/defender-office-365-unified-rbac-permissions.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-office-365-unified-rbac-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/defender-office-365-unified-rbac-permissions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: a9a5c0fd-67b8-070e-f55c-1b57278a80ca
---

# Unified RBAC permissions for Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Use this quick reference to find the Microsoft Defender unified role-based access control (RBAC) permissions that are required for Microsoft Defender for Office 365 features in the Microsoft Defender portal:

- Find the exact permission that's required for a feature.
- Build custom roles based on specific Defender for Office 365 tasks.
- Understand what's in scope and out of scope for Unified RBAC.

For step-by-step configuration guidance, see [How to configure Unified RBAC for Microsoft Defender for Office 365](step-by-step-guides/configure-unified-rbac-defender-office-365). For all Unified RBAC permissions, see [Permissions in Microsoft Defender unified RBAC](/en-us/defender-xdr/custom-permissions-details).

Important

Starting July 2026, Unified RBAC is the default permission model for new Microsoft Defender for Office 365 Plan 2 organizations. The legacy Email & collaboration roles page isn't available for those organizations. Existing organizations can manually activate Unified RBAC at any time. For more information, see [MC1246006](https://admin.microsoft.com/Adminportal/Home#/MessageCenter/:/messages/MC1246006).

## Scope and constraints

Unified RBAC applies only to the Defender portal at https://security.microsoft.com. Unified RBAC doesn't apply to:

- The Exchange admin center.
- The Microsoft Purview portal.
- PowerShell (uses [Exchange Online RBAC](/en-us/exchange/permissions-exo/permissions-exo)).

Microsoft Entra roles (for example, Security Administrator) always grant access regardless of Unified RBAC activation.

## Quick lookup

The following table maps common tasks to the required Unified RBAC permission:

| Task | Required permission |
| --- | --- |
| View threat policies | Core security settings (read) |
| Edit threat policies | Core security settings (manage) |
| View email in Threat Explorer | Email & collaboration metadata (read) |
| Preview email content | Email & collaboration content (read) |
| Remediate emails | Email & collaboration advanced actions (manage) |
| Manage quarantine | Email & collaboration quarantine (manage) |
| Submit messages to Microsoft | Response (manage) |
| View incidents and alerts | Security data basics (read) |
| Manage incidents | Alerts (manage) |
| Approve automated investigation actions | Response (manage) |
| Manage Tenant Allow/Block List entries | Detection tuning (manage) |
| Manage user tags | System settings (manage) |
| Run advanced hunting queries | Security data basics (read) |
| Take actions from advanced hunting | Response (manage) and Email & collaboration advanced actions (manage) |

## Defender for Office 365 permissions

The following tables list the Unified RBAC permissions that apply to Defender for Office 365 features, grouped by permission category.

### Security operations – Security data

For detailed permission descriptions, see [Security operations – Security data](/en-us/defender-xdr/custom-permissions-details#security-operations--security-data).

| Permission | Level | What it enables |
| --- | --- | --- |
| Security data basics | Read | View incidents, alerts, investigations, advanced hunting data, submissions, and reports |
| Alerts | Manage | Manage alerts, start automated investigations, classify and assign incidents |
| Response | Manage | Approve or dismiss remediation actions, submit messages to Microsoft, manage automation lists |
| Email & collaboration quarantine | Manage | View and release quarantined email and Teams messages |
| Email & collaboration advanced actions | Manage | Move or delete email (soft delete and hard delete), remediate from Threat Explorer |

### Security operations – Raw data (Email & collaboration)

For detailed permission descriptions, see [Security operations – Raw data (Email & collaboration)](/en-us/defender-xdr/custom-permissions-details#security-operations--raw-data-email--collaboration).

| Permission | Level | What it enables |
| --- | --- | --- |
| Email & collaboration metadata | Read | View email and collaboration data in Threat Explorer, email entity page, campaigns, threat trackers, and advanced hunting |
| Email & collaboration content | Read | View and download email content and attachments |
| Email & collaboration content: Emails associated with alerts | Read | View and download email content associated with the security alerts **Email reported by user as malware or phish** and **Email reported by user as junk** |
| Email & collaboration content: Quarantine Emails | Read | View and download quarantined messages for all users |

### Authorization and settings

For detailed permission descriptions, see [Authorization and settings](/en-us/defender-xdr/custom-permissions-details#authorization-and-settings).

| Permission | Level | What it enables |
| --- | --- | --- |
| Core security settings | Read | View threat policies, quarantine policies, preset security policies, DKIM/DMARC/SPF settings, Configuration Analyzer, and user-reported settings |
| Core security settings | Manage | Configure threat policies, quarantine policies, preset security policies, DKIM/DMARC/SPF settings, and user-reported settings |
| Detection tuning | Manage | Manage alert policies, custom detections, Tenant Allow/Block List entries |
| System settings | Read | View user tags and priority account tags |
| System settings | Manage | Manage user tags and priority account tags |

## Feature-to-permission mapping

The following tables show the required permission for each Defender for Office 365 experience in the Defender portal.

### Threat policies and protection

All threat policy features use **Core security settings** (read to view, manage to configure):

- [Anti-phishing policies](anti-phishing-policies-mdo-configure)
- [Anti-spam policies](anti-spam-policies-configure)
- [Anti-malware policies](anti-malware-policies-configure)
- [Safe Links policies](safe-links-policies-configure)
- [Safe Attachments policies](safe-attachments-policies-configure)
- [Outbound spam policies](outbound-spam-policies-configure)
- [Connection filter policies](connection-filter-policies-configure)
- [Preset security policies](preset-security-policies)
- [Configuration Analyzer](configuration-analyzer-for-security-policies)
- Email authentication settings ([SPF](email-authentication-spf-configure), [DKIM](email-authentication-dkim-configure), and [DMARC](email-authentication-dmarc-configure)).
- [Safe Attachments for SharePoint, OneDrive, and Microsoft Teams](safe-attachments-for-spo-odfb-teams-configure)
- [Quarantine policies](quarantine-policies)

Note

Mail flow connectors are outside Unified RBAC scope and are controlled by Exchange Online roles.

### Threat investigation and hunting

For more information about these experiences, see [Advanced hunting](/en-us/defender-xdr/advanced-hunting-overview).

| Experience | Task | Permission required |
| --- | --- | --- |
| [Threat Explorer](threat-explorer-real-time-detections-about) | View email metadata | Email & collaboration metadata (read) |
|  | View email content | Email & collaboration content (read) |
|  | Remediate emails | Email & collaboration advanced actions (manage) |
| [Email entity page](mdo-email-entity-page) | View metadata | Email & collaboration metadata (read) |
|  | View content | Email & collaboration content (read) |
|  | View content for emails associated with alerts | Email & collaboration content: Emails associated with alerts (read) |
|  | View quarantined messages | Email & collaboration content: Quarantine Emails (read) |
| [Campaigns](campaigns) | View campaign data | Email & collaboration metadata (read) |
| [Threat trackers](threat-trackers) | View tracker data | Email & collaboration metadata (read) |
| [Advanced hunting](/en-us/defender-xdr/advanced-hunting-overview) | Read data | Security data basics (read) |
|  | Take actions | Response (manage) and Email & collaboration advanced actions (manage) |

### Incidents, alerts, and response

For more information about these experiences, see [Manage incidents and alerts](mdo-sec-ops-manage-incidents-and-alerts).

| Experience | Task | Permission required |
| --- | --- | --- |
| [Incidents and alerts](mdo-sec-ops-manage-incidents-and-alerts) | View | Security data basics (read) |
|  | Classify, assign, and comment | Alerts (manage) |
| [Alert policies](alert-policies-defender-portal) | Manage | Detection tuning (manage) |
| [Action center](/en-us/defender-xdr/m365d-action-center) | View | Security data basics (read) |
|  | Approve or dismiss actions | Response (manage) |
| [Automated investigation and response](air-about) | View | Security data basics (read) |
|  | Approve | Response (manage) |

### Quarantine and submissions

For more information about these experiences, see [Manage quarantined messages](quarantine-admin-manage-messages-files) and [Admin submissions](submissions-admin).

| Experience | Task | Permission required |
| --- | --- | --- |
| [Quarantine](quarantine-admin-manage-messages-files) | View | Security data basics (read) |
|  | Release or delete messages | Email & collaboration quarantine (manage) |
|  | Submit from quarantine | Response (manage) |
| [Submissions](submissions-admin) | View | Security data basics (read) |
|  | Submit messages to Microsoft | Response (manage) |
| [User-reported settings](submissions-user-reported-messages-custom-mailbox) | View | Core security settings (read) |
|  | Configure | Core security settings (manage) |

### Tenant Allow/Block List

For more information, see [Tenant Allow/Block List](tenant-allow-block-list-about).

| Experience | Permission required |
| --- | --- |
| View entries | Core security settings (read) |
| Add, modify, or delete entries | Detection tuning (manage) |

### Reports and monitoring

For more information, see [Email security reports](reports-email-security).

| Experience | Permission required |
| --- | --- |
| Defender for Office 365 reports | Security data basics (read) |
| Email security reports | Security data basics (read) |
| Threat analytics | Security data basics (read) |

Note

[Mail flow reports](/en-us/exchange/monitoring/mail-flow-reports/mail-flow-reports) and [message trace](message-trace-defender-portal) are Exchange Online experiences outside the security portal. They're outside Unified RBAC permission scope and are controlled by [Exchange Online roles](/en-us/exchange/permissions-exo/permissions-exo).

### User tags

For more information, see [User tags](user-tags-about).

| Experience | Permission required |
| --- | --- |
| View user tags | System settings (read) |
| Manage user tags | System settings (manage) |
| Manage priority account tags | System settings (manage) |

### Microsoft Teams protection

For more information, see [Microsoft Teams protection](mdo-support-teams-about). Microsoft Teams protection uses the same permissions as email features:

| Experience | Permission required |
| --- | --- |
| View Teams message data | Email & collaboration metadata (read) |
| Quarantine Teams messages | Email & collaboration quarantine (manage) |
| Submit Teams messages | Response (manage) |

## Experiences outside Unified RBAC scope

The following features aren't controlled by Unified RBAC. Use the specified alternative permission model:

| Feature | Permission model |
| --- | --- |
| Attack Simulation Training | Microsoft Entra roles |
| Remove users from Teams chats | Microsoft Entra roles |
| Message trace | Exchange Online roles |
| Mail flow reports | Exchange Online roles |
| Mail flow connectors | Exchange Online roles |
| PowerShell cmdlets | Exchange Online roles |

## Inverse permission matrix

Use this section to understand what experiences each permission enables.

### Security data basics (read)

- Incidents and alerts (view)
- Action center (view)
- Automated investigation and response (view)
- Quarantine (view)
- Submissions (view)
- Reports and threat analytics
- Advanced hunting (read data)
- Teams data access

### Alerts (manage)

- Incident classification, assignment, and commenting

### Response (manage)

- Approve or dismiss remediation actions (automated investigation and response, Action center)
- Submit messages to Microsoft
- Advanced hunting actions

### Email & collaboration quarantine (manage)

- Release or delete quarantined email and Teams messages

### Email & collaboration advanced actions (manage)

- Remediate emails (Threat Explorer, email entity page)
- Advanced hunting actions (with Response (manage))

### Email & collaboration metadata (read)

- Threat Explorer (email metadata)
- Email entity page
- Campaigns
- Threat trackers
- Teams entity panel

### Email & collaboration content (read)

- Email preview
- Attachment access

### Core security settings (read/manage)

- All threat policy and configuration experiences (read to view, manage to configure)

### Detection tuning (manage)

- Alert policies
- Tenant Allow/Block List modifications

### System settings (read/manage)

- User tags
- Priority account tags

## Frequently asked questions

Common questions about Unified RBAC for Defender for Office 365:

- **Q: Who can activate Unified RBAC?**

    A: Global Administrator or Security Administrator in Microsoft Entra ID.
- **Q: Does Unified RBAC affect the Exchange admin center?**

    A: No. The Exchange admin center uses its own role-based access control.
- **Q: Does PowerShell use Unified RBAC?**

    A: No. PowerShell cmdlets continue to use [Exchange Online RBAC](/en-us/exchange/permissions-exo/permissions-exo).
- **Q: Can I import legacy Email & collaboration roles?**

    A: Yes. Use the import feature in the Defender portal. For more information, see [Import existing roles](/en-us/defender-xdr/import-rbac-roles).
- **Q: Can I scope roles to Defender for Office 365 only?**

    A: Yes. When you create or edit a role, select **Defender for Office 365** as the data source.
- **Q: What do I need before I activate Unified RBAC?**

    A: Review the activation prerequisites before you turn on Unified RBAC. For more information, see [Prerequisites to activate Microsoft Defender unified RBAC](/en-us/defender-xdr/activate-defender-rbac#prerequisites).
- **Q: Does Unified RBAC support Privileged Identity Management (PIM)?**

    A: Yes. Assign Unified RBAC roles to PIM-managed groups.