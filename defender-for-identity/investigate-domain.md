---
layout: Conceptual
title: Investigate an Active Directory domain - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/investigate-domain
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
description: Learn how to investigate an Active Directory domain in Microsoft Defender. Review domain health scores, security policies, trust relationships, and recommendations.
ms.date: 2026-07-30T00:00:00.0000000Z
ms.topic: concept-article
ms.custom: msecd-doc-authoring-106
ai-usage: ai-assisted
locale: en-us
document_id: aea0d7dd-9615-ec1f-6e09-457e4850db3b
document_version_independent_id: aea0d7dd-9615-ec1f-6e09-457e4850db3b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/investigate-domain.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: investigate-domain
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/investigate-domain.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: ad25c832-db00-c58e-fb6d-b753bfbb86ee
---

# Investigate an Active Directory domain - Microsoft Defender for Identity | Microsoft Learn

Active Directory domains are frequently targeted in identity-based attacks. Configuration issues such as unhealthy sensors, weak security policies, or risky trust relationships can expose an environment, but the information needed to assess a domain's security is often distributed between different tools and views.

The Active Directory domain page in Microsoft Defender brings together domain health, sensor coverage, security policies, trust relationships, and recommendations for your on-premises Active Directory environment into a single view. Use it to determine whether a domain is healthy and fully monitored, identify configuration or policy issues that increase risk, review trust relationships, and act on prioritized recommendations.

## Prerequisites

- A Microsoft Defender for Identity license, or another license that includes Defender for Identity (such as E5).
- A user role with at least [Security Reader](/en-us/azure/active-directory/roles/permissions-reference#security-reader) permissions.

## Access the Domain page

You can reach the Active Directory domain page through multiple entry points in Microsoft Defender:

- On the **Identity dashboard**, select a domain from the **Active Directory protected domains** widget.
- Select a domain name from the **Domain** column in the identity inventory.
- Select a domain from a domain-related security alert or incident.
- Search for a domain by name using the global search bar.

To switch between domains when you're on the domain page, use the domain selector at the top right of the page.

[![Screenshot that shows the Identity dashboard with the Active Directory protected domains widget.](media/investigate-domain/domain-page-identity-dashboard.png)](media/investigate-domain/domain-page-identity-dashboard.png#lightbox)

## Overview tab

The **Overview** tab provides a domain summary.

[![Screenshot that shows the domain overview tab with domain details, deployment health, health score, and identity summary cards.](media/investigate-domain/domain-page-overview.png)](media/investigate-domain/domain-page-overview.png#lightbox)

| Section | Description |
| --- | --- |
| **Domain details** | Shows key domain attributes: <br>1. Provider<br>2. Domain name<br>3. Functional level<br>4. Creation date<br>5. Identities count<br>6. Service accounts count<br>7. Group accounts count<br>8. Computer accounts count<br><br> Select any count to view the filtered list. |
| **Properties** | Shows the domain's **Canonical Name**, **SID**, and **ID**. |
| **Deployment Health** | Shows sensor deployment coverage and health status. A 100% coverage score means all domain controllers have sensors deployed. Select a deployment issue to navigate to sensor deployment settings. |
| **Health Score** | Displays an overall health score (Low, Medium, or High) based on identity infrastructure coverage, sensor health, and active recommendations. Select **How to fix** to view recommended actions. |
| **All Domain Identities** | Shows the total number of identities, including how many are classified as **Critical** or **Sensitive**. Select **View domain identities** to open the identity inventory filtered to this domain. |
| **Service accounts** | Shows a donut chart of service accounts by type: sMSA (standalone Managed Service Account), gMSA (group Managed Service Account), and User. Select **View domain service accounts** to open the service accounts page. |
| **Sensitive Entities** | Shows the count of sensitive identities, groups, and computers. Select any count to view the details. |
| **Active Recommendations** | Lists security recommendations that affect the health score, with links to remediation guidance. For example, the **Unsecure Domain Configurations** recommendation links to the corresponding security posture assessment. |
| **Group Policies** | Lists Group Policy Objects (GPOs) applied in the domain. Use this section to verify active policies and identify domains with no GPOs configured. |

## Incidents and alerts tab

Shows all incidents and alerts connected to the domain. Data on this tab includes only incidents and alerts created on or after February 1, 2026.

The tab includes default filters for **Status** (New, In progress) and **Alert severity** (High, Medium, Low). You can export, copy the list link, refresh, and customize columns.

[![Screenshot that shows the Incidents and alerts tab of the domain page in Microsoft Defender.](media/investigate-domain/domain-page-incidents-alerts.png)](media/investigate-domain/domain-page-incidents-alerts.png#lightbox)

| Column | Description |
| --- | --- |
| **Incident name** | The name of the incident. |
| **Incident Id** | The unique identifier of the incident. |
| **Priority score** | The priority score assigned to the incident. |
| **Tags** | Tags associated with the incident. |
| **Severity** | The severity level of the incident (High, Medium, Low). |
| **Investigation state** | The current state of the investigation. |
| **Categories** | The threat categories associated with the incident. |
| **Impacted assets** | The assets affected by the incident. |
| **Active alerts** | The number of active alerts in the incident. |

## Security recommendations (Preview)

For scoped users, the domain page shows security recommendations for the domains included in their assigned scope. This view helps scoped users focus on the identity risks that are relevant to the domains they're responsible for. Customers can use this experience to provide domain-level recommendation context without granting broader access across the environment. Each recommendation includes relevant risk information, affected assets, and suggested remediation actions to help scoped users understand what needs attention.

[![Screenshot that shows the Security recommendations tab of the domain page in Microsoft Defender.](media/investigate-domain/domain-page-security-recommendations.png)](media/investigate-domain/domain-page-security-recommendations.png#lightbox)

| Column | Description |
| --- | --- |
| **Recommendation name** | The name of the security recommendation. Select a recommendation to view more details and remediation guidance. |
| **Status** | The current status of the recommendation. |
| **Last sync** | The date and time when the recommendation was last updated. |

## Security Policies tab

Provides human-readable summaries of key Active Directory security policies in four cards. Use this tab to review critical Active Directory configurations and check whether they meet current security standards.

[![Screenshot that shows the Security policies tab of the Investigate domains page in Microsoft Defender.](media/investigate-domain/domain-page-security-policies.png)](media/investigate-domain/domain-page-security-policies.png#lightbox)

| Card | Details |
| --- | --- |
| **Password Policy** | Password maximum age, minimum age, history, complexity, authenticated password change only, no clear-text password change, admin lockout after failed attempts, password store clear text, and password change is refused. |
| **Account Lockout Policy** | Lockout duration and lockout threshold. |
| **Kerberos Policy** | Maximum ticket age and maximum renewal age. |
| **LDAP & Machine Account** | LDAP signing policy and machine account quota. If the domain has active recommendations for insecure configurations, a warning banner appears with a link to view the recommendations. |

## Trusts tab

Shows trust relationships for the domain. You can export the list.

| Column | Description |
| --- | --- |
| **Display Name** | The name of the trusted domain. |
| **Direction** | The direction of the trust (for example, Inbound, Outbound, or Bidirectional). |
| **Attributes** | The attributes of the trust relationship. |

Use this tab to review which domains trust each other and in which direction.

## Groups tab

Lists the groups in the domain. You can filter by tags, type, and scope. You can mark groups as sensitive to support exposure analysis and detect potential attack paths.

[![Screenshot that shows the Group Accounts tab of the domain page in Microsoft Defender.](media/investigate-domain/domain-page-groups.png)](media/investigate-domain/domain-page-groups.png#lightbox)

| Column | Description |
| --- | --- |
| **Name** | The name of the group. Select to view group details. |
| **Tags** | Tags assigned to the group, such as Sensitive. |
| **Type** | The group type (for example, Security). |
| **Scope** | The group scope (Universal, Global, or DomainLocal). |
| **Direct Members** | The number of direct members in the group. |
| **Canonical Name** | The full canonical name path of the group in Active Directory. |
| **Description** | The description of the group. |

## Computers tab

Lists the computer accounts in the domain. You can filter by tags. You can mark computer accounts as sensitive to support exposure analysis and detect potential attack paths.

[![Screenshot that shows the Computer Accounts tab of the domain page in Microsoft Defender.](media/investigate-domain/domain-page-computers.png)](media/investigate-domain/domain-page-computers.png#lightbox)

| Column | Description |
| --- | --- |
| **Name** | The name of the computer account. Select to view computer details. |
| **Tags** | Tags assigned to the computer, such as Sensitive. |
| **Update Time** | The date and time the computer account was last updated. |
| **SID** | The Security Identifier of the computer account. |
| **Canonical Name** | The full canonical name path of the computer in Active Directory. |
| **Description** | The description of the computer account. |