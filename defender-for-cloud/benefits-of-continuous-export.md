---
layout: Conceptual
title: Export alerts and recommendations with continuous export - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/benefits-of-continuous-export
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn about the benefits of continuous export in Microsoft Defender for Cloud. Stream security data to Azure Monitor workspace for analysis and visualization.
ms.date: 2025-07-15T00:00:00.0000000Z
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: 06eb5fb7-5517-3b87-03e7-522b0a4c54cc
document_version_independent_id: eb703b15-31c0-8afa-ab24-da6cbc701112
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/benefits-of-continuous-export.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/benefits-of-continuous-export
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/benefits-of-continuous-export.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/f0234678-3067-4edc-abf7-8142d54bb7d2
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/b0f4f6b9-28ed-4892-be4e-517310289c68
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: f5747870-ba3d-0bbe-d8d9-f0aa09829472
---

# Export alerts and recommendations with continuous export - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud provides continuous export of security data. This feature allows you to stream security data to Log Analytics in Azure Monitor, to Azure Event Hubs, or to another Security Information and Event Management (SIEM), Security Orchestration Automated Response (SOAR), or IT classic [deployment model solution](export-to-siem). You can analyze and visualize the data using Azure Monitor logs and other Azure Monitor features.

When you set up continuous export, you can fully customize what information to export and where the information goes. For example, you can configure it so that:

- All high-severity alerts are sent to an Azure event hub.
- All medium or higher-severity findings from vulnerability assessment scans of your computers running SQL Server are sent to a specific Log Analytics workspace.
- Specific recommendations are delivered to an event hub or Log Analytics workspace whenever they're generated.
- The secure score for a subscription is sent to a Log Analytics workspace whenever the score for a control changes by 0.01 or more.

## What data types can be exported?

You can use continuous export to export the following data types whenever they change:

- Security recommendations.
    - Recommendation severity.
    - Security findings.
- Secure score.
    - Controls.
- Security alerts.
- Regulatory compliance.
- Attack paths

Recommendation severity, security findings, and controls are *sub* categories that belong to a *parent* category. For example:

- The recommendations [System updates should be installed on your machines (powered by Update Center)](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/e1145ab1-eb4f-43d8-911b-36ddf771d13f) and [System updates should be installed on your machines](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/4ab6e3c5-74dd-8b35-9ab9-f61b30875b27) each has one sub recommendation per outstanding system update.
- The recommendation [Machines should have vulnerability findings resolved](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/1195afff-c881-495e-9bc5-1486211ae03f) has a sub recommendation for every vulnerability that the vulnerability scanner identifies.

Note

If you’re configuring [continuous export by using the REST API](continuous-export-rest-api), always include the parent with the findings.

## Export data to an event hub or Log Analytics workspace in another tenant

You *can't* configure data to be exported to a Log Analytics workspace in another tenant if you use Azure Policy to assign the configuration. This process works only when you use the REST API to assign the configuration, and the configuration is unsupported in the Azure portal (because it requires a multitenant context). Azure Lighthouse *doesn't* resolve this issue with Azure Policy, although you can use Azure Lighthouse as the authentication method.

When you collect data in a tenant, you can analyze the data from one, central location.

To export data to an event hub or Log Analytics workspace in a different tenant:

- In the tenant that has the event hub or Log Analytics workspace, [invite a user](/en-us/azure/active-directory/external-identities/what-is-b2b#easily-invite-guest-users-from-the-azure-portal) from the tenant that hosts the continuous export configuration, or you can configure Azure Lighthouse for the source and destination tenant.
- If you use business-to-business (B2B) guest user access in Microsoft Entra ID, ensure that the user accepts the invitation to access the tenant as a guest.
- If you use a Log Analytics workspace, assign the user in the workspace tenant one of these roles: Owner, Contributor, Log Analytics Contributor, Microsoft Sentinel Contributor, or Monitoring Contributor.
- Create and submit the request to the Azure REST API to configure the required resources. You must manage the bearer tokens in both the context of the local (workspace) tenant and the remote (continuous export) tenant.

## Export to a Log Analytics workspace

If you want to analyze Microsoft Defender for Cloud data inside a Log Analytics workspace or use Azure alerts together with Defender for Cloud alerts, set up continuous export to your Log Analytics workspace.

### Log Analytics tables and schemas

Security alerts and recommendations are stored in the **SecurityAlert** and **SecurityRecommendation** tables respectively.

The name of the Log Analytics solution that contains these tables depends on whether you enabled the enhanced security features: Security (the Security and Audit solution) or SecurityCenterFree.

Tip

To see the data on the destination workspace, you must enable one of these solutions: Security and Audit or SecurityCenterFree.

![Screenshot that shows the SecurityAlert table in Log Analytics.](media/benefits-of-continuous-export/log-analytics-securityalert-solution.png)

To view the event schemas of the exported data types, see [Log Analytics table schemas](https://aka.ms/ASCAutomationSchemas).