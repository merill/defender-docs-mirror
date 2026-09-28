---
layout: Conceptual
title: Transition Your Microsoft Sentinel Environment to the Defender Portal | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/move-to-defender
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Move Microsoft Sentinel operations from the Azure portal to the Microsoft Defender portal.
ms.author: guywild
author: guywi-ms
ms.reviewer: soulisabag
ms.topic: how-to
ms.date: 2026-09-10T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1028
locale: en-us
document_id: a6a0f54f-1bcd-f8f5-1010-3cf121ef687d
document_version_independent_id: d6fa3825-581d-d394-8e93-4ad7e2b9a124
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/move-to-defender.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/move-to-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/move-to-defender.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 556efc75-a41a-43a1-c8c3-78721b7d6ea0
---

# Transition Your Microsoft Sentinel Environment to the Defender Portal | Microsoft Learn

Microsoft Sentinel is available in the Microsoft Defender portal with [Microsoft Defender XDR](/en-us/microsoft-365/security/defender) or on its own. It delivers a unified experience across SIEM and XDR for faster, more accurate threat detection and response, simpler workflows, and better operational efficiency.

This article explains how to transition your Microsoft Sentinel experience from the Azure portal to the Defender portal. If you use Microsoft Sentinel in the Azure portal, transition to Microsoft Defender for unified security operations and the latest features. Before you begin, review the Prerequisites for transitioning to the Defender portal section for required access and preparatory steps. For more information, see [Microsoft Sentinel in the Microsoft Defender portal](microsoft-sentinel-defender-portal) or watch our [Microsoft Sentinel in the Defender portal video playlist](https://www.youtube.com/playlist?list=PL3ZTgFEc7Lyska6WLWBzc8sob-kYA2jPj).

Note

Transitioning to the Defender portal, even for non-E5 customers, has no extra cost. The customer continues to be billed as usual for their consumption on Sentinel only.

## Prerequisites

Before you start, note:

- This article is for customers with an existing workspace enabled for Microsoft Sentinel who want to transition their Microsoft Sentinel experience to the Defender portal. If you're a new customer who onboarded with the permissions of a subscription [Owner (Azure built-in role)](/en-us/azure/role-based-access-control/built-in-roles#owner) or a [User access administrator (Azure built-in role)](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator), your workspaces are automatically onboarded to the Defender portal. For more information, see [Quickstart: Onboard to the Defender portal](quickstart-onboard).
- Some Microsoft Sentinel features have new locations in the Defender portal. For more information, see [Quick reference for Microsoft Sentinel feature locations in the Defender portal](microsoft-sentinel-defender-portal#quick-reference).
- When relevant, detailed prerequisites are in the linked articles for each step.

## Plan and set up your transition environment

**Audience**: Security architects

**Videos**:

- [Onboarding a Microsoft Sentinel workspace in Microsoft Defender](https://youtu.be/Hgcz87XdJx0?si=n78kqKVoLvbwZp5k)
- [Managing unified RBAC in Microsoft Defender](https://youtu.be/0xvPy1zWIfg?si=sBuxxOVr1O_yuTyS)

### Review planning guidance, complete prerequisites, and onboard

Review all planning guidance and finish all prerequisites before you onboard your workspace to the Defender portal. For more information, see the following articles:

- [**Plan for unified security operations in the Defender portal**](/en-us/defender-xdr/isoc-overview). After onboarding to the Defender portal, the **[Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles/security#microsoft-sentinel-contributor)** role is assigned to the **Microsoft Threat Protection** and **WindowsDefenderATP** apps in your subscription.
- [**Manage Microsoft Sentinel and Defender XDR permissions in the Defender portal**](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/managing-microsoft-sentinel-and-microsoft-defender-xdr-permissions-in-microsoft-/4480583). The "Manage Microsoft Sentinel and Defender XDR permissions in the Defender portal" blog post explains how Microsoft Sentinel and Defender XDR permissions work in the unified Defender portal, what to expect as you transition, as well as an introduction to the new unified role-based access control (URBAC). To read more about URBAC, see [Map Microsoft Defender XDR unified RBAC permissions to existing RBAC permissions](/en-us/defender-xdr/compare-rbac-roles#map-microsoft-defender-xdr-unified-rbac-permissions-to-existing-rbac-permissions).
- [**Deploy for unified security operations in the Defender portal**](/en-us/defender-xdr/isoc-overview). While this article is for new customers who don't yet have a workspace for Microsoft Sentinel or other services onboarded to the Defender portal, use it as a reference if you're moving to the Defender portal.
- [**Connect Microsoft Sentinel to the Defender portal**](/en-us/azure/sentinel/microsoft-sentinel-onboard). The "Connect Microsoft Sentinel to the Defender portal" article lists the prerequisites for onboarding your workspace to the Defender portal. If you plan to use Microsoft Sentinel without Defender XDR, you need to take an extra step to trigger the connection between Microsoft Sentinel and the Defender portal.

### Review differences for data storage and privacy

When you use the Azure portal, the [Microsoft Sentinel policies](geographical-availability-data-residency) for data storage, process, retention, and sharing apply. When you use the Defender portal, the [Microsoft Defender XDR policies](/en-us/defender-xdr/data-privacy) apply instead, even when you work with Microsoft Sentinel data.

The following table provides additional details and links so that you can compare experiences across the Azure and Defender portals.

| Area of support | Azure portal | Defender portal |
| --- | --- | --- |
| **Business continuity and disaster recovery (BCDR)** | Customers are responsible for replicating their data | Microsoft Defender uses automation for BCDR on control planes. |
| **Data storage and processing** | - [Data storage location](geographical-availability-data-residency#data-storage-location)- [Supported regions](geographical-availability-data-residency#supported-regions) | [Data storage location](/en-us/defender-xdr/data-privacy#data-storage-location) |
| **Data retention** | [Data retention](geographical-availability-data-residency#data-retention) | [Data retention](/en-us/defender-xdr/data-privacy#data-retention) |
| **Data sharing** | [Data sharing](geographical-availability-data-residency#data-sharing-for-microsoft-sentinel) | [Data sharing](/en-us/defender-xdr/data-privacy#data-sharing) |

For more information about data storage and privacy policies, see [Geographical availability and data residency in Microsoft Sentinel](geographical-availability-data-residency) and [Data security and retention in Microsoft Defender XDR](/en-us/defender-xdr/data-privacy).

### Onboarding to the Defender portal with customer-managed keys (CMK)

Important

CMK encryption is not fully supported for data stored in the Microsoft Sentinel data lake. All data ingested into the data lake - such as custom tables or transformed data - is encrypted using Microsoft-managed keys.

If you enabled CMK before onboarding, when you onboard your Microsoft Sentinel-enabled workspace to the Defender portal, all log data in your workspace continues to be encrypted with CMK - including both previously and newly ingested data.

Analytic rules and other Sentinel content, such as automation rules, also continue to be CMK-encrypted. However, alerts and incidents will no longer be CMK-encrypted after onboarding.

For more information about CMK, see [Set up Microsoft Sentinel customer-managed key](customer-managed-keys).

### Configure multi-workspace and multitenant management

Defender supports one or more workspaces across multiple tenants through the [Microsoft Defender multitenant portal](https://mto.security.microsoft.com), which serves as a central place to manage incidents and alerts, hunt for threats across tenants, and lets Managed Security Service Partners (MSSPs) see across customers.

In multi-workspace scenarios, the multitenant portal lets you connect one primary workspace and multiple secondary workspaces per tenant. Onboard each workspace to the Defender portal separately for each tenant, just like onboarding for a single tenant.

For more information about multitenant and multi-workspace configuration, see:

- [**Set up Microsoft Defender multitenant management**](/en-us/defender-xdr/mto-requirements)
- [**Azure Lighthouse documentation**](/en-us/azure/lighthouse/how-to/manage-sentinel-workspaces). Azure Lighthouse lets you use Microsoft Sentinel data from other tenants across onboarded workspaces. For example, you can run cross-workspace queries with the `workspace()` operator in Advanced hunting and analytics rules.
- [**Microsoft Entra B2B**](/en-us/entra/identity/multi-tenant-organizations/overview#b2b-direct-connect). Microsoft Entra B2B lets you access data across tenants. Granular Delegated Admin Privileges (GDAP) for Microsoft Sentinel is in preview.

## Configure and review your settings and content

**Audience**: Security engineers

**Video**: [Managing connectors in Microsoft Defender](https://youtu.be/IW9WOhhLbmY?si=XX4IXe47o9bXnWlV)

### Confirm and configure data collection

When Microsoft Sentinel is integrated with Microsoft Defender, the fundamental architecture of data collection and telemetry flow remains intact. Existing non-Microsoft data connectors continue operating without interruption. However, alert ingestion for Microsoft security products changes after onboarding to the Defender portal with Microsoft Defender XDR. Alerts from Microsoft security products are routed through the Microsoft Defender XDR connector instead of standalone Microsoft security product alert connectors.

In multi-workspace environments, the Microsoft Defender XDR connector is connected to the primary workspace only. To prevent duplicate tenant-based alerts across workspaces, standalone data connectors for Microsoft Defender for Office 365, Microsoft Entra ID Protection, Microsoft Defender for Cloud Apps, Microsoft Defender for Endpoint, and Microsoft Defender for Identity are automatically disconnected in secondary workspaces during onboarding. As a result, tenant-based alerts from these Microsoft security products are available only in the primary workspace.

From a Log Analytics perspective, Microsoft Sentinel’s integration into Microsoft Defender doesn't change how Microsoft Sentinel stores log data in Log Analytics. Despite the front-end unification, the Microsoft Sentinel backend remains fully integrated with Log Analytics for data storage, search, and correlation.

Alerts related to Defender products are streamed directly from the [Microsoft Defender connector](/en-us/azure/sentinel/connect-microsoft-365-defender) to ensure consistency. Make sure that you have incidents and alerts from this connector turned on in your workspace. Once you have this data connector configured in your workspace, [offboarding the workspace from Microsoft Defender](/en-us/azure/sentinel/microsoft-sentinel-onboard#offboard-microsoft-sentinel) also disconnects the Microsoft Defender connector.

Note

This connector-routing change results in schema differences for some alerts. For a detailed comparison, see [Alert schema differences: Standalone vs. Microsoft Defender XDR connector](security-alert-schema-differences).

To migrate analytics rule incident creation and alert grouping settings, see [Migrate Microsoft Sentinel incident creation rules and alert grouping settings to Defender XDR](/en-us/azure/sentinel/migrate-sentinel-incident-creation-rules-alert-grouping).

For more information, see [Connect data from Microsoft Defender to Microsoft Sentinel](connect-microsoft-365-defender).

#### Integrate with Microsoft Defender for Cloud

Review the following connector-specific actions to avoid duplicate events when integrating Microsoft Defender for Cloud with the Defender portal:

- If you're using the tenant-based data connector for Defender for Cloud, make sure to take action to prevent duplicate events and alerts.
- If you're using the legacy, subscription-based connector instead, MDC alerts may still be forwarded to your primary Sentinel workspace using the data connector for Microsoft Defender XDR.

For more information, see [Alerts and incidents in Microsoft Defender](/en-us/azure/defender-for-cloud/concept-integration-365#microsoft-sentinel-customers).

#### Data connector visibility in the Defender portal

After onboarding your workspace to Defender, the following data connectors are used for unified security operations and aren't shown in the **Data connectors** page in the Defender portal:

- Microsoft Defender for Cloud Apps
- Microsoft Defender for Endpoint
- Microsoft Defender for Identity
- Microsoft Defender for Office 365 (Preview)
- Microsoft Defender XDR
- Subscription-based Microsoft Defender for Cloud (Legacy)
- Tenant-based Microsoft Defender for Cloud (Preview)

These data connectors continue to be listed in Microsoft Sentinel in the Azure portal.

### Configure your ecosystem

While Microsoft Sentinel's [Workspace Manager](workspace-manager) isn't available in the Defender portal, use one of the following alternative capabilities for distributing content as code across workspaces:

- [**Deploy content as code from your repository** (Public preview)](ci-cd). Use YAML or JSON files in GitHub or Azure DevOps to manage and deploy configurations across Microsoft Sentinel and Defender using unified CI/CD workflows.
- [**Multitenant portal**](/en-us/defender-xdr/mto-overview). The Microsoft Defender multitenant portal supports managing and distributing content across multiple tenants.

Otherwise, continue to deploy solution packages that include various types of security content from the Content hub in the Defender portal. For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](sentinel-solutions-deploy).

### Configure analytics rules

Microsoft Sentinel analytics rules are available in the Defender portal for detection, configuration, and management. For more information, see [Microsoft Sentinel configuration in the Defender portal](microsoft-sentinel-defender-portal#configuration). Analytics rule functionality remains the same, including creation, updating, and management through the wizard, repositories, and the Microsoft Sentinel API. Incident correlation and multistage attack detection also continue to work in the Defender portal. The alert correlation functionality managed by the Fusion analytics rule in the Azure portal is handled by the Defender XDR engine in the Defender portal, which consolidates all signals in one place.

When moving to the Defender portal, the following changes are important to note:

| Feature | Description |
| --- | --- |
| **Custom detection rules** | If you have detection use cases that involve both Defender XDR and Microsoft Sentinel data, where you don't need to retain Defender XDR data for more than 30 days, we recommend creating [custom detection rules](/en-us/defender-xdr/custom-detections-overview) that query data from both Microsoft Sentinel and Defender XDR tables. Creating custom detection rules that query both sources is supported without needing to ingest Defender XDR data into Microsoft Sentinel. For more information, see [Use Microsoft Sentinel custom functions in advanced hunting in Microsoft Defender](/en-us/defender-xdr/advanced-hunting-defender-use-custom-rules#custom-detection-rules). |
| **Alert promotion (preview)** | Supported third-party alerts are automatically promoted to Microsoft Defender XDR alerts. Review existing analytics rules for potential duplicates. For supported sources, requirements, and alert-tuning guidance, see [Alert promotion](/en-us/defender-xdr/investigate-alerts#alert-promotion-preview). |
| **Alert correlation** | In the Defender portal, correlations are automatically applied to alerts against both Microsoft Defender data and third-party data ingested from Microsoft Sentinel, regardless of alert scenarios. The criteria used to correlate alerts together in a single incident are part of the Defender portal's proprietary, internal correlation logic. For more information, see [Alert correlation and incident merging in the Defender portal](/en-us/defender-xdr/alerts-incidents-correlation). |
| **Alert grouping and incident merging** | While you will still see the alert grouping configuration in Analytics rules, the [Defender XDR correlation engine](/en-us/defender-xdr/alerts-incidents-correlation) fully controls alert grouping and incident merging when necessary in the Defender portal. This ensures a comprehensive view of the full attack story by stitching together relevant alerts for multistage attacks. For example, multiple individual analytics rules configured to generate an incident for each alert may result in merged incidents if they match Defender XDR correlation logic. |
| **Alert visibility** | If you have Microsoft Sentinel analytics rules configured to trigger alerts only (see [Configure incident creation settings](create-analytics-rules#configure-the-incident-creation-settings)), with incident creation turned off, these alerts aren't visible in the Defender portal. |
| **Alert tuning** | Once your Microsoft Sentinel workspace is onboarded to Defender, all incidents, including those from your Microsoft Sentinel analytics rules, are generated by the Defender XDR engine. As a result, the [alert tuning capabilities](/en-us/defender-xdr/investigate-alerts#tune-an-alert) in the Defender portal, previously available only for Defender XDR alerts, can now be applied to alerts from Microsoft Sentinel. Alert tuning allows you to streamline incident response by automating the resolution of common alerts, reducing false positives, and minimizing noise, so analysts can prioritize significant security incidents. |
| **Fusion: Advanced multistage attack detection** | In the Azure portal, the Fusion analytics rule creates incidents based on alert correlations made by the Fusion correlation engine. This rule is disabled when you onboard Microsoft Sentinel to the Defender portal. You don't lose alert correlation functionality because the Defender portal uses Microsoft Defender XDR's incident-creation and correlation functionalities to replace those of the Fusion engine. For more information, see [Advanced multistage attack detection in Microsoft Sentinel](fusion) |

### Configure automation rules and playbooks

In Microsoft Sentinel, playbooks are based on workflows built in [Azure Logic Apps](/en-us/azure/logic-apps/logic-apps-overview), a cloud service that helps you schedule, automate, and orchestrate tasks and workflows across systems throughout the enterprise.

The following limitations apply to Microsoft Sentinel automation rules and playbooks when working in the Defender portal. You might need to make some changes in your environment when making the transition.

| Functionality | Description |
| --- | --- |
| **Automation rules with alert triggers** | In the Defender portal, automation rules with alert triggers act only on Microsoft Sentinel alerts. To automate responses to Defender XDR alerts as well, use the **[Enhanced Alert Trigger](automation/generate-playbook#enhanced-alert-trigger)**. For more information, see [Alert create trigger](automate-incident-handling-with-automation-rules#alert-create-trigger). |
| **Automation rules with incident triggers** | In both the Azure portal and the Defender portal, the **Incident provider** condition property is removed, as all incidents have *Microsoft XDR* as the incident provider (the value in the *ProviderName* field). At that point, any existing automation rules run on both Microsoft Sentinel and Microsoft Defender XDR incidents, including those where the **Incident provider** condition is set to only *Microsoft Sentinel* or *Microsoft 365 Defender*. However, automation rules that specify a specific analytics rule name run only on incidents that contain alerts that were created by the specified analytics rule. This means that you can define the **Analytic rule name** condition property to an analytics rule that exists only in Microsoft Sentinel to limit your rule to run on incidents only in Microsoft Sentinel. Also, after onboarding to the Defender portal, the **SecurityIncident** table no longer includes a **Description** field. Therefore: - If you're using this **Description** field as a condition for an automation rule with an incident creation trigger, that automation rule won't work after onboarding to the Defender portal. In such cases, make sure to update the configuration appropriately. For more information, see [Incident trigger conditions](automate-incident-handling-with-automation-rules#conditions). - If you have an integration configured with an external ticketing system, like ServiceNow, the incident description will be missing. |
| **Latency in playbook triggers** | [It might take up to 5 minutes](move-to-defender#5min) for Microsoft Defender incidents to appear in Microsoft Sentinel. If this delay is present, playbook triggering is delayed too. |
| **Automation batching window** | If multiple changes are made to the same incident within 5-10 minutes, a single update is sent to Microsoft Sentinel, with only the most recent change. Intermediate updates are lost, which can impact workflows that depend on processing sequential incident state changes. For more information, see [Incident update trigger](automate-incident-handling-with-automation-rules#incident-update-trigger). |
| **Changes to existing incident names** | The Defender portal uses a unique engine to correlate incidents and alerts. When onboarding your workspace to the Defender portal, existing incident names might be changed if the correlation is applied. To ensure that your automation rules always run correctly, we therefore recommend that you avoid using incident titles as condition criteria in your automation rules, and suggest instead to use the name of any analytics rule that created alerts included in the incident, and tags if more specificity is required. |
| ***Updated by* field** | After onboarding your workspace, the **Updated by** field has a [new set of supported values](automate-incident-handling-with-automation-rules#incident-update-trigger), which no longer include *Microsoft 365 Defender*. In existing automation rules, *Microsoft 365 Defender* is replaced by a value of *Other* after onboarding your workspace. |
| **Creating automation rules directly from an incident** | [Creating automation rules directly from an incident](false-positives#add-exceptions-with-automation-rules-azure-portal-only) is supported only in the Azure portal. If you're working in the Defender portal, create your automation rules from scratch from the **Automation** page. |
| **Microsoft incident creation rules** | Microsoft incident creation rules aren't supported in the Defender portal. For more information, see [Microsoft Defender XDR incidents and Microsoft incident creation rules](microsoft-365-defender-sentinel-integration#microsoft-defender-xdr-incidents-and-microsoft-incident-creation-rules). |
| **Running automation rules from the Defender portal** | It might take up to 10 minutes from the time that an alert is triggered and an incident is created or updated in the Defender portal to when an automation rule is run. This time lag is because the incident is created in the Defender portal and then forwarded to Microsoft Sentinel for the automation rule. |
| **Active playbooks tab** | After onboarding to the Defender portal, by default the **Active playbooks** tab shows a predefined filter with onboarded workspace's subscription. In the Azure portal, add data for other subscriptions using the subscription filter. For more information, see [Create and customize Microsoft Sentinel playbooks from templates](automation/use-playbook-templates). |
| **Running playbooks manually on demand** | The following procedures aren't currently supported in the Defender portal: - [Run a playbook manually on an alert](automation/run-playbooks#run-a-playbook-manually-on-an-alert)- [Run a playbook manually on an entity](automation/run-playbooks#run-a-playbook-manually-on-an-entity) |
| **Running playbooks on incidents requires Microsoft Sentinel sync** | If you try to run a playbook on an incident from the Defender portal and see the message *"Can't access data related to this action. Refresh the screen in a few minutes."*, this means that the incident isn't yet synchronized to Microsoft Sentinel. Refresh the incident page after the incident is synchronized to run the playbook successfully. |
| **Incidents: Adding alerts to incidents / Removing alerts from incidents** | Since adding or removing alerts from incidents isn't supported after onboarding your workspace to the Defender portal, these actions are also not supported from within playbooks. For more information, see [Understand how alerts are correlated and incidents are merged in the Defender portal](move-to-defender#understand-how-alerts-are-correlated-and-incidents-are-merged-in-the-defender-portal). |
| **Microsoft Defender XDR integration in multiple workspaces** | If you've integrated XDR data with more than one workspace in a single tenant, the data will now only be ingested into the primary workspace in the Defender portal. Transfer automation rules to the relevant workspace to keep them running. |
| **Automation and the Correlation engine** | The correlation engine may combine alerts from multiple signals into a single incident, which could result in automation receiving data you didn’t anticipate. We recommend reviewing your automation rules to ensure you're seeing the expected results. |

### Configure APIs

The unified experience in the Defender portal introduces notable changes to incidents and alerts from APIs. It supports API calls based on the [Microsoft Graph REST API v1.0](/en-us/graph/api/resources/security-api-overview?view=graph-rest-1.0&amp;preserve-view=true), which can be used for automation related to alerts, incidents, advanced hunting, and more.

The [Microsoft Sentinel API](/en-us/rest/api/securityinsights/api-versions) continues to support actions against Microsoft Sentinel resources, like analytics rules, automation rules and more. For interacting with unified incidents and alerts, we recommend that you use the Microsoft Graph REST API. If you're using the Microsoft Sentinel `SecurityInsights` API to interact with Microsoft Sentinel incidents, you might need to update your automation conditions and trigger criteria due to changes in the response body.

The following table lists fields that are important in the response snippets, and compares them across the Azure and Defender portals:

| Functionality | Azure portal | Defender portal |
| --- | --- | --- |
| **Link to the incident** | `incidentUrl`: The direct URL to the incident in the Microsoft Sentinel portal | `providerIncidentUrl` : This additional field provides a direct link to the incident, which can be used to synchronize this information with a third-party ticketing system like ServiceNow. `incidentUrl` is still available, but it points to the Microsoft Sentinel portal. |
| **The sources that triggered the detection and published the alert** | `alertProductNames` | `alertProductNames`: Requires adding `?$expand=alerts` to the GET. For example, `https://graph.microsoft.com/v1.0/security/incidents/368?$expand=alerts` |
| **The name of the alert provider** | `providerName` = "Azure Sentinel" | `providerName` = "Microsoft XDR" |
| **The service or product that created the alert** | Doesn't exist in the Azure portal | `serviceSource`For example, "microsoftDefenderForCloudApps" |
| **The detection technology or sensor that identified the notable component or activity** | Doesn't exist in the Azure portal | `detectionSource`For example, "cloudAppSecurity" |
| **The name of the product which published this alert** | Doesn't exist in the Azure portal | `productName`For example, "Microsoft Defender for Cloud Apps" |

## Run operations in the Defender portal

**Audience**: Security analysts

**Videos**:

- [Discover and manage Microsoft Sentinel content and threat intelligence in Microsoft Defender](https://youtu.be/HQ4JxM8-v5g?si=tMdCCMYOkPv28m_w)
- [Create automation and workbooks in Microsoft Defender](https://youtu.be/Lc0T_hPTug4?si=TgEpXViwxet7M7t1)
- [Alert correlation in Microsoft Defender](https://youtu.be/GIIxN1dMJTc?si=7VEO6asJA6dBC-V0)
- [Incident investigation in Microsoft Defender](https://youtu.be/BnZBVm8ZGsY?si=I-uHGASquUrr4xN5)
- [Case management in Microsoft Defender](https://youtu.be/TxLz-NsxcrM?si=hgg3DujUICLozuYt)
- [Advanced hunting in Microsoft Defender](https://youtu.be/06ukKCHMkeY?si=520Gg8JNmRVYUXKD)
- [SOC optimizations in Microsoft Defender](https://youtu.be/-Cv5K8A4kfY?si=3o9xVB7WnfH0E3VR)

### Update incident triage processes for the Defender portal

If you've used Microsoft Sentinel in the Azure portal, you'll notice significant user experience enhancements in the Defender portal. While you might need to update SOC processes and retrain your analysts, the design consolidates all relevant information in a single place to provide more streamlined and efficient workflows.

The unified incident queue in the Defender portal consolidates all incidents across products into a single view, impacting how analysts triage incidents that now contain multiple, cross-security domain alerts. For example:

- Traditionally, analysts triage incidents based on specific security domains or expertise, often handling tickets per entity, such as a user or host. This approach can create blind spots, which the unified experience aims to address.
- When an attacker moves laterally, related alerts might end up in separate incidents due to different security domains. The unified experience eliminates this issue by providing a comprehensive view, ensuring all related alerts are correlated and managed cohesively.

Analysts can also view detection sources and product names in the Defender portal, and apply and share filters for more efficient incident and alert triage.

The unified triage process can help reduce analyst workloads and even potentially combine the roles of tier 1 and tier 2 analysts. However, the unified triage process can also require broader and deeper analyst knowledge. We recommend training on the new portal interface to ensure a smooth transition.

The Defender portal also provides investigation capabilities that aren't available in the Azure portal, including the [attack story and incident graph](/en-us/defender-xdr/investigate-incidents#attack-story) for visualizing the full scope of an attack, and [blast radius analysis](/en-us/defender-xdr/investigate-incidents#blast-radius-analysis) to help analysts visualize possible propagation paths, assess business impact, and prioritize containment actions.

For more information, see [Incidents and alerts in the Microsoft Defender portal](/en-us/defender-xdr/incidents-overview?toc=%2Fazure%2Fsentinel%2FTOC.json&amp;bc=%2Fazure%2Fsentinel%2Fbreadcrumb%2Ftoc.json).

### Understand how alerts are correlated and incidents are merged in the Defender portal

Defender’s correlation engine merges incidents when it recognizes common elements between alerts in separate incidents. When a new alert meets correlation criteria, Microsoft Defender aggregates and correlates it with other related alerts from all the detection sources into a new incident. After onboarding Microsoft Sentinel to the Defender portal, the unified incident queue reveals a more comprehensive attack, making analysts more efficient and providing a complete attack story.

In multi-workspace scenarios, only alerts from a primary workspace are correlated with Microsoft Defender XDR data. There are also specific scenarios in which incidents aren't merged.

After onboarding Microsoft Sentinel to the Defender portal, the following changes apply to incidents and alerts:

| Feature | Description |
| --- | --- |
| **Delay just after onboarding your workspace** | It may take up to 5 minutes for Microsoft Defender incidents to fully integrate with Microsoft Sentinel. This doesn't affect features provided directly by Microsoft Defender, such as automatic attack disruption. |
| **Security incident creation rules** | Any active [Microsoft security incident creation rules](create-incidents-from-alerts) are deactivated to avoid creating duplicate incidents. The incident creation settings in other types of analytics rules remain as they are, and are configurable in the Defender portal. |
| **Incident provider name** | In the Defender portal, the **Incident provider name** is always Microsoft XDR. |
| **Adding / removing alerts from incidents** | Adding or removing Microsoft Sentinel alerts to or from incidents is supported only in the Defender portal. To remove an alert from an incident in the Defender portal, you must [add the alert to another incident](/en-us/defender-xdr/move-alert-to-another-incident). |
| **Editing comments** | Add comments to incidents in either the Defender or Azure portal, but editing existing comments isn't supported in the Defender portal. Edits made to comments in the Azure portal aren't synchronized to the Defender portal. |
| **Programmatic and manual creation of incidents** | Incidents created in Microsoft Sentinel through the API, by a Logic App playbook, or manually from the Azure portal, aren't synchronized to the Defender portal. These incidents are still supported in the Azure portal and the API. See [Create your own incidents manually in Microsoft Sentinel](create-incident-manually). |
| **Reopening closed incidents** | In the Defender portal, you can't set alert grouping in Microsoft Sentinel analytics rules to reopen closed incidents if new alerts are added. Closed incidents aren't reopened in this case, and new alerts trigger new incidents. |

For more information, see [Incidents and alerts in the Microsoft Defender portal](/en-us/defender-xdr/incidents-overview) and [Alert correlation and incident merging in the Microsoft Defender portal](/en-us/defender-xdr/alerts-incidents-correlation).

### Note changes for investigations with Advanced hunting

After onboarding Microsoft Sentinel to the Defender portal, access and use all your existing log tables, Kusto Query Language (KQL) queries, and functions in the **Advanced hunting** page. All Microsoft Sentinel alerts that are tied to incidents are ingested into the `AlertInfo` table, accessible from the **Advanced hunting** page.

Bookmarks aren't available in Advanced hunting, which provides a unified query experience across Microsoft Defender and Microsoft Sentinel data. However, bookmarks are still available in **Microsoft Sentinel** &gt; **Threat management** &gt; **Hunting**, which provides the Microsoft Sentinel-specific hunting experience. You can also use alternatives such as incident tags, saved queries, or custom hunting tables to preserve and track investigation context.

For more information, see [Advanced hunting with Microsoft Sentinel data in Microsoft Defender](/en-us/defender-xdr/advanced-hunting-microsoft-defender), especially the list of [known issues for advanced hunting with Microsoft Sentinel data](/en-us/defender-xdr/advanced-hunting-microsoft-defender), and [Keep track of data during hunting with Microsoft Sentinel](/en-us/azure/sentinel/bookmarks).

### Investigate with entities in the Defender portal

In the Microsoft Defender portal, entities are generally either *assets*, such as accounts, hosts, or mailboxes, or *evidence*, such as IP addresses, files, or URLs.

After onboarding Microsoft Sentinel to the Defender portal, entity pages for [user entities](/en-us/defender-xdr/investigate-users), [device entities](/en-us/defender-xdr/entity-page-device), and IP addresses are consolidated into a single view with a comprehensive view of the entity's activity and context and data from both Microsoft Sentinel and Microsoft Defender XDR.

The Defender portal also provides a global search bar that centralizes results from all entities so that you can search across SIEM and XDR.

For more information, see [Entity pages in Microsoft Sentinel](/en-us/azure/sentinel/entity-pages?tabs=defender-portal).

### Investigate with UEBA in the Defender portal

Most functionalities of User and Entity Behavior Analytics (UEBA) remain the same in the Defender portal as they were in the Azure portal, with exceptions for adding entities to threat intelligence and for `IdentityInfo` table schema differences:

- Adding entities to threat intelligence from incidents is supported only in the Azure portal. For more information, see [Add entity to threat indicators](add-entity-to-threat-intelligence).
- After you onboard Microsoft Sentinel to the Microsoft Defender portal, the `IdentityInfo` table is available in both Microsoft Defender Advanced hunting and your Microsoft Sentinel Log Analytics workspace. The Advanced hunting version includes unified fields from Defender XDR and Microsoft Sentinel. Some fields available in the Microsoft Sentinel Log Analytics version are renamed or aren't supported in Advanced hunting.

    Be sure to review and update any queries that run in Microsoft Defender, such as Advanced hunting queries or custom detections. Microsoft Sentinel analytic rules, workbooks, and other Sentinel queries continue to use the `IdentityInfo` table in the Log Analytics workspace and aren’t affected.

    For more information and a comparison of the table schemas in Advanced hunting experience and Log Analytics, see [IdentityInfo table](ueba-reference?tabs=unified-table#identityinfo-table).

Important

When you transition to the Defender portal, the `IdentityInfo` table becomes a native Defender table that doesn't support table-level role-based access control (RBAC). If your organization uses table-level RBAC to restrict access to the `IdentityInfo` table in the Azure portal, this access control will no longer be available after you transition to the Defender portal.

### Update investigation processes to use Microsoft Defender threat intelligence

For Microsoft Sentinel customers moving from the Azure portal to the Defender portal, the familiar threat intelligence features are retained in the Defender portal under **Intel management**, and enhanced with other threat intelligence features available in the Defender portal. Supported features depend on the licenses you have, such as:

| Feature | Description |
| --- | --- |
| **Threat analytics** | Supported for [Microsoft Defender XDR](/en-us/defender-xdr/) customers. An in-product solution provided by Microsoft security researchers, designed to help security teams by offering insights on emerging threats, active threats, and their impacts. The data is presented in an intuitive dashboard with cards, rows of data, filters, and more. |
| **Intel Profiles** | Supported for [Microsoft Defender Threat Intelligence](/en-us/defender-xdr/defender-threat-intelligence) customers. Categorize threats and behaviors by a Threat Actor Profile, making it easier to track and correlate. These profiles include any Indicators of Compromise (IoC) related to tactics, techniques, and tools used in attacks. |
| **Intel Explorer** | Supported for [Microsoft Defender Threat Intelligence](/en-us/defender-xdr/defender-threat-intelligence) customers. Consolidates available IoCs and provides threat-related articles as they are posted, enabling security teams to stay updated on emerging threats. |
| **Intel projects** | Deprecated. To organize and investigate threat indicators, [link indicators to a case](/en-us/defender-xdr/manage-cases#link-indicators-preview). |

In the Defender portal, use the `ThreatIntelObjects` and `ThreatIntelIndicators` together with Indicators for Compromise for threat hunting, incident response, Copilot, reporting, and to create relational graphs showing connections between indicators and entities.

For customers using the Microsoft Defender Threat Intelligence (MDTI) feed, a free version is available via Microsoft Sentinel's data connector for MDTI. Users with MDTI licenses can also ingest MDTI data and use Security Copilot for threat analysis, active threat review, and threat actor research.

For more information about threat management, threat analytics, intelligence projects, and threat intelligence in Microsoft Sentinel, see:

- [Threat management](microsoft-sentinel-defender-portal#threat-management)
- [Threat analytics in Microsoft Defender XDR](/en-us/defender-xdr/threat-analytics)
- [Link indicators to a case](/en-us/defender-xdr/manage-cases#link-indicators-preview)
- [Threat intelligence in Microsoft Sentinel](/en-us/azure/sentinel/understand-threat-intelligence)

### Use workbooks to visualize and report on Microsoft Defender data

Azure workbooks continue to be the primary tool for data visualization and interaction in the Defender portal, functioning as they did in the Azure portal.

To use workbooks with data from Advanced hunting, make sure that you ingest logs into Microsoft Sentinel.

For more information, see [Visualize and monitor your data by using workbooks in Microsoft Sentinel](monitor-your-data).

### Similar incidents (Preview) aren't supported in the Defender portal

The Microsoft Sentinel [similar incidents in case investigations](investigate-cases#similar-incidents-preview) feature is in Preview and isn't supported in the Defender portal. Because this feature isn't supported in the Defender portal, the **Similar incidents** tab isn't available on an incident details page.