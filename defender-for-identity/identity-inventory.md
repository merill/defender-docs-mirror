---
layout: Conceptual
title: View the Identity inventory - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/identity-inventory
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: View and manage all identities across your organization from the Identity inventory page in Microsoft Defender. Investigate identity types, domains, and attributes.
ms.topic: article
ms.custom:
- msecd-doc-authoring-106
- sfi-ga-nochange
- sfi-image-nochange
ms.date: 2026-06-22T00:00:00.0000000Z
ms.reviewer: maelgami
locale: en-us
document_id: b70d63e9-d4f9-ef18-98b7-276e39e78bc3
document_version_independent_id: b70d63e9-d4f9-ef18-98b7-276e39e78bc3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/identity-inventory.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-inventory
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/identity-inventory.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: f514b218-b4d7-7a81-523f-78fc7425be9d
---

# View the Identity inventory - Microsoft Defender for Identity | Microsoft Learn

The **Identity inventory** provides a centralized view of all identities in your organization, so you can investigate, monitor, and manage them efficiently. At a glance, see key details like the identity's type, domain, tags, and other attributes to quickly spot identities that require attention.

When you [enable the Identity inventory integration](/en-us/defender-cloud-apps/general-setup#enable-identity-inventory-integration) in Microsoft Defender for Cloud Apps, SaaS and cloud application accounts are ingested into the Identity inventory. This provides a centralized view of identities across on-premises, cloud, and SaaS environments. With the integration enabled, you get access to unified experiences including the identity timeline, identity-centric response, improved identity correlation, and identity-centric protection.

Important

As Microsoft Defender moves toward a fully unified identity platform, some Defender for Cloud Apps data pipelines remain separate from the Identity inventory. As a result, identity correlations defined in the Identity inventory, including manual and policy-based correlations, don't currently affect the following Defender for Cloud Apps capabilities:

- Built-in detections
- UEBA (User and Entity Behavior Analytics)
- Scoped deployment
- Governance actions
- Defender for Cloud Apps policies
- Activity log
- Cloud discovery user enrichment and anonymization
- RBAC scoping

These features continue to use the Cloud Application Accounts inventory. For more information, see the relevant Defender for Cloud Apps documentation.

The **Identity inventory** page includes tabs for:

- **Human identities**: Human identities discovered in your environment from Active Directory and Microsoft Entra ID. When the Identity inventory integration is enabled, this tab also includes SaaS and cloud application accounts from Defender for Cloud Apps.
- **Non-Human identities (Preview)**: Non-human identities discovered in your SaaS, Entra ID, and on-premises environments, including:
    - OAuth apps registered in:
        - Microsoft Entra ID
        - Google Workspace
        - Salesforce
    - On-premises service accounts from Active Directory

From the top navigation:

- Add or remove columns.
- Apply filters.
- Sort the list by column values.
- Search for a specific identity.
- Export the list to a CSV file.
- Copy a link to the current filtered view.

Note

When you export the identities list to a CSV file, only the first 5,000 identities are included in the export.

## Access the Identity inventory

In the [Microsoft Defender portal](https://security.microsoft.com), select **Assets** &gt; **Identities**.

![Screenshot of the identity inventory page in the Microsoft Defender portal.](media/identity-inventory/identity-inventory-page.png)

## Identity inventory insights

The top section of the Identity inventory page gives you quick insights into your identity landscape through the following cards:

- The **Classify critical assets** card lets you define identity groups as business critical. For more information, see [Microsoft Security Exposure Management](/en-us/security-exposure-management/microsoft-security-exposure-management).
- The **Highly privileged identities** card helps you investigate all sensitive accounts in your organization in Advanced hunting, including Microsoft Entra ID Security administrators and Global administrators.
- The **Critical Active Directory service accounts** card helps you quickly identify all Active Directory accounts designated as critical, making it easier to focus on identities most at risk.
- The **Cloud application accounts** card connects you to your [Cloud application accounts](/en-us/defender-cloud-apps/accounts) identified by the Defender for Cloud apps application connectors. When the Identity inventory integration is enabled, cloud application accounts also appear in the **Human identities** tab.

## The identity inventory lists

Select a tab to view details and available actions for each identity type.

# [Human identities](#tab/human-identities)
The **Human identities** tab consolidates all user identities from Active Directory and Microsoft Entra ID in one place, making it easier to view and manage user accounts. To investigate details about a specific user, see [Investigate users in Microsoft Defender XDR](/en-us/defender-xdr/investigate-users).

### Human identity statistics

These important statistics help you prioritize identities for security posture improvements:

| Name | Description |
| --- | --- |
| Total | The total number of identities. |
| Critical | The number of your critical assets. |
| Disabled | The number of all disabled identities in your organization. |

### Human identity details

The **Identities** list highlights key details for each human identity, including these columns by default:

| Column name | Description |
| --- | --- |
| Display name | The full name of the identity as shown in the directory. |
| Domain | The Active Directory domain to which the identity belongs. |
| Object ID | A unique identifier for the identity in Microsoft Entra ID. |
| UPN (User Principal Name) | The unique sign-in name of the identity in an email-like format. |
| Identity environment | Indicates whether the identity is on-premises (originates from Active Directory), Cloud only (Entra ID) or Hybrid (synced from Azure Active Directory to Microsoft Entra ID). |
| Identity provider | The name of the identity provider. |
| Risk score | A score from 0 to 100 that's dynamically calculated for the identity. The score reflects how likely the identity is to be compromised and how much damage a compromise could cause. For details, see [Risk score tab](/en-us/defender-xdr/investigate-users#risk-score-tab). |
| Criticality level | The criticality level assigned to the identity. |
| Tags | Custom labels that help categorize identities considered high-value assets. For example, **Sensitive**, **Honeytoken**, or **Privileged Accounts** managed by a [Privileged Identity Management](/en-us/entra/id-governance/privileged-identity-management/pim-configure) (PIM) service. |
| SID | The Security Identifier, a unique value used to identify the identity in Active Directory. |
| Account status | Shows whether the identity is enabled or disabled. |
| Type | Specifies if the identity is a user account or service account. |
| Created time | The timestamp of when the identity was first created. |
| Last updated | The timestamp of the most recent update to the identity's attributes in Active Directory. |

Nondefault columns: Email, Microsoft Entra ID risk level, and Cloud ID.

# [Non-Human identities (Preview)](#tab/non-human-identities)
The **Non-Human identities** tab consolidates all non-human identities in one place, making it easier to check ownership and assess risk. To investigate details about a specific non-human identity, see [View a non-human identity](/en-us/defender-xdr/investigate-non-human-identities).

![Screenshot of non-human identities tab in the Identity Inventory.](media/identity-inventory/non-human-identities.png)

### Non-human identity stats

These statistics highlight non-human identities that might need prioritization. Select a statistic to get a filtered list of identities to investigate.

| Name | Description |
| --- | --- |
| Risky | The number of non-human identities with a high risk score. Risk scores are based on factors described in the [Risk score tab of the identity](/en-us/defender-cloud-apps/app-governance-visibility-insights-view-apps#getting-detailed-information-on-an-app). |
| Highly privileged | The number of non-human identities that have at least one high-privilege API permission or high-privilege Microsoft Entra role. |
| Overprivileged | The number of non-human identities with more permissions than they use. |
| Unused | The number of non-human identities with no recent sign-in activity. |
| External unverified publishers | The number of non-human identities from unverified external publishers. |
| New | The number of recently discovered non-human identities. |
| Used by AI agents (Preview) | The number of Entra ID service principals used by AI agents. |

### Non-human identity details

The **Non-Human identities** tab contains these sections:

- **Entra ID**: All service principals registered in Microsoft Entra ID, excluding managed identities and Microsoft first-party applications.
- **Active Directory**: On-premises service accounts.
- **Salesforce**: OAuth apps registered in Salesforce.
- **Google Workspace**: OAuth apps registered in Google.

The **Identities** list highlights key details for each non-human identity, including these columns by default:

| Column name | Description |
| --- | --- |
| Display name | The full name of the identity as shown in the directory. |
| Status | Shows whether the identity is enabled or disabled, and if disabled, by whom. |
| Risk score | Shows the identity risk score, from 0 to 100. Higher values indicate greater risk. |
| Graph API access | Shows whether the identity has at least one Graph API permission. |
| Permission type | Shows the type of permissions assigned to the identity: <br>- **Delegated**: Delegated API permissions only, no roles.<br>- **Application**: Application API permissions only, no roles.<br>- **Microsoft Entra roles**: Microsoft Entra roles only, no API permissions.<br>- **Mixed**: A combination of any two or more of the above.<br>- **None**: No API permissions or Entra roles assigned. |
| Origin | Shows whether the identity originated in the tenant or is registered in an external tenant. |
| Consent type | Shows whether the identity has admin or user-only consent. For identities with only user consent, the total consented users are shown. Identities with admin consent have broad access to all data, unless access policies and other restrictions limit that access. |
| Publisher | Publisher of the identity and their verification status. |
| Last used | Last time the identity signed in. This data is tracked only back to June 1, 2022. |
| Used by AI agents (Preview) | Shows the name of the AI agent platform whose agents use the Entra ID service principal, such as Copilot Studio or Azure AI Foundry. To view the specific Copilot Studio agent connected to the service principal, expand the OAuth app node in the [Graph tab](/en-us/defender-cloud-apps/app-governance-visibility-insights-view-apps#graph-tab). |

### Respond to high-risk identities

For Microsoft Entra ID identities, select **Create new policy** to set up a governance policy that automatically responds when high-risk apps appear. Use the built-in **New high risk app** template for a quick setup, or create a custom policy with risk score as a policy condition.

---

### Related articles

- [Investigate users in Microsoft Defender](/en-us/defender-xdr/investigate-users)
- [Investigate non-human identities in Microsoft Defender](/en-us/defender-xdr/investigate-users)
- [Investigate cloud application accounts](/en-us/defender-cloud-apps/accounts)