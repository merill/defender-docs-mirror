---
layout: Conceptual
title: Alerts and incidents in Microsoft Defender XDR for Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-integration-365
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
description: Learn about the benefits of receiving Microsoft Defender for Cloud's alerts in Microsoft Defender XDR
ms.topic: concept-article
ms.date: 2026-01-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: e39e6737-13ae-7cc3-34c8-5e988619ffe4
document_version_independent_id: 409443a1-3abd-a65c-7565-ae6a95e2c0d6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/concept-integration-365.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/concept-integration-365
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/concept-integration-365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: ef16404a-c43c-fecc-40d0-48a46f8cddae
---

# Alerts and incidents in Microsoft Defender XDR for Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

**Applies to:**

- [Microsoft Defender XDR](/en-us/defender-xdr/microsoft-365-defender)
- [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud)

Microsoft Defender for Cloud is integrated with Microsoft Defender Extended Detection and Response (XDR). This integration allows security teams to access Defender for Cloud alerts and incidents within the Microsoft Defender portal. This integration provides richer context to investigations that span cloud resources, devices, and identities.

The partnership with Microsoft Defender XDR allows security teams to get the complete picture of an attack, including suspicious and malicious events that happen in their cloud environment. Security teams can accomplish this goal through immediate correlations of alerts and incidents.

Microsoft Defender XDR offers a comprehensive solution that combines protection, detection, investigation, and response capabilities. The solution protects against attacks on devices, email, collaboration, identity, and cloud apps. Our detection and investigation capabilities are now extended to cloud entities, offering security operations teams a single pane of glass to significantly improve their operational efficiency.

Incidents and alerts are now part of [Microsoft Defender XDR's public API](/en-us/microsoft-365/security/defender/api-overview). This integration allows exporting of security alerts data to any system using a single API. As Microsoft Defender for Cloud, we're committed to providing our users with the best possible security solutions, and this integration is a significant step towards achieving that goal.

## Prerequisites

- [Enable Defender for Cloud on your Azure subscription](connect-azure-subscription).
- Access to Defender for Cloud alerts in the Microsoft Defender portal depends on which Defender for Cloud plans are enabled. Learn more about the different [Defender for Cloud plan protections](defender-for-cloud-introduction#cloud-workload-protection-platform-cwpp).

Note

Permissions to view Defender for Cloud alerts and correlations are automatic for the entire tenant. Viewing specific subscriptions isn't supported. Use the **alert subscription ID** filter to view Defender for Cloud alerts associated with a specific Defender for Cloud subscription in the alert and incident queues. Learn more about [filters](/en-us/defender-xdr/incident-queue#filters).

The integration is available only by applying the appropriate [Microsoft Defender XDR Unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac) role for Defender for Cloud. To view Defender for Cloud alerts and correlations without Defender XDR Unified RBAC, you must be a Global Administrator or Security Administrator in Microsoft Entra ID.

## Investigation experience in Microsoft Defender XDR

The following table describes the detection and investigation experience in Microsoft Defender XDR with Defender for Cloud alerts.

| Area | Description |
| --- | --- |
| Incidents | All Defender for Cloud incidents are integrated to Microsoft Defender XDR.  - Searching for cloud resource assets in the [incident queue](/en-us/microsoft-365/security/defender/incident-queue) is supported.  - The [attack story](/en-us/microsoft-365/security/defender/investigate-incidents#attack-story) graph shows cloud resource.  - The [assets tab](/en-us/microsoft-365/security/defender/investigate-incidents#assets) in an incident page shows the cloud resource.  - Each virtual machine has its own entity page containing all related alerts and activity.  There are no duplications of incidents from other Defender workloads. |
| Alerts | All Defender for Cloud alerts, including multicloud, internal and external providers' alerts, are integrated to Microsoft Defender XDR. Defender for Cloud alerts show on the Microsoft Defender XDR [alert queue](/en-us/microsoft-365/security/defender-endpoint/alerts-queue-endpoint-detection-response). Microsoft Defender XDR The `cloud resource` asset shows up in the Asset tab of an alert. Resources are clearly identified as an Azure, Amazon, or a Google Cloud resource.  Defender for Cloud alerts are automatically associated with a tenant.  There are no duplications of alerts from other Defender workloads. |
| Alert and incident correlation | Alerts and incidents are automatically correlated, providing robust context to security operations teams to understand the complete attack story in their cloud environment. |
| Threat detection | Accurate matching of virtual entities to device entities to ensure precision and effective threat detection. |
| Unified API | Defender for Cloud alerts and incidents are now included in [Microsoft Defender XDR's public API](/en-us/microsoft-365/security/defender/api-overview), allowing customers to export their security alerts data into other systems using one API. |

Note

Informational alerts from Defender for Cloud aren't integrated to the Microsoft Defender portal to allow focus on the relevant and high severity alerts. This strategy streamlines management of incidents and reduces alert fatigue.

### Alert status synchronization

When the integration between Defender for Cloud and Microsoft Defender XDR is enabled, alert status changes are synchronized between the two services with the following behaviors:

| Scenario | Status synchronization |
| --- | --- |
| Defender for Cloud alert status changed in Defender for Cloud | Status reflected in Microsoft Defender XDR: **Yes** |
| Defender for Cloud alert status changed in Microsoft Defender XDR | Status reflected in Defender for Cloud: **Yes** |
| Microsoft Defender for Endpoint alert on cloud resource - status changed in Defender for Cloud | Status reflected in Defender for Cloud: **Yes**Status reflected in Microsoft Defender XDR: **No** |
| Microsoft Defender for Endpoint alert on cloud resource - status changed in Microsoft Defender XDR | Status reflected in Microsoft Defender XDR: **Yes**Status reflected in Defender for Cloud: **No** |

Important

- In Defender for Cloud, only Defender for Cloud alerts are valid entities. References to Microsoft Defender XDR alerts within Defender for Cloud apply only to Microsoft Defender for Endpoint alerts on cloud resources.
- Microsoft Defender for Endpoint alerts on cloud resources appear in both Defender for Cloud and Microsoft Defender XDR, but their statuses aren't synchronized between the two services.

## Advanced hunting in XDR

Microsoft Defender XDR's advanced hunting capabilities are extended to include Defender for Cloud alerts and incidents. This integration allows security teams to hunt across all their cloud resources, devices, and identities in a single query.

The advanced hunting experience in Microsoft Defender XDR is designed to provide security teams with the flexibility to create custom queries to hunt for threats across their environment. The integration with Defender for Cloud alerts and incidents allows security teams to hunt for threats across their cloud resources, devices, and identities.

The [CloudAuditEvents table](/en-us/defender-xdr/advanced-hunting-cloudauditevents-table) in advanced hunting allows you to investigate and hunt through control plane events and to create custom detections to surface suspicious Azure Resource Manager and Kubernetes (KubeAudit) control plane activities.

The [CloudProcessEvents table](/en-us/defender-xdr/advanced-hunting-cloudauditevents-table) in advanced hunting allows you to triage, investigate and create custom detections for suspicious activities that are invoked in your cloud infrastructure with information that includes details on the process details.

The [CloudStorageAggregatedEvents table](/en-us/defender-xdr/advanced-hunting-cloudstorageaggregatedevents-table)in advanced hunting allows you to investigate and hunt through cloud storage activities and to create custom detections that help surface suspicious file operations, access patterns and data interactions occurring across your cloud storage resources.

## Microsoft Sentinel customers

Microsoft Sentinel customers who are [integrating Microsoft Defender XDR incidents](/en-us/azure/sentinel/microsoft-365-defender-sentinel-integration)*and* are ingesting Defender for Cloud alerts must take the following steps to prevent duplicate alerts and incidents.

1. In Microsoft Sentinel, configure the **Tenant-based Microsoft Defender for Cloud (Preview)** data connector. This data connector is included in the **Microsoft Defender for Cloud** solution, available from the Microsoft Sentinel **Content hub**.

    The **Tenant-based Microsoft Defender for Cloud (Preview)** data connector synchronizes alert collection from all your subscriptions with the tenant-based Defender for Cloud incidents that are streaming through the Microsoft Defender XDR incidents connector. Defender for Cloud incidents are correlated across all subscriptions of the tenant.

    If you're working with multiple Microsoft Sentinel workspaces in the Defender portal, the correlated Defender for Cloud incidents are streamed to the primary workspace. For more information, see [Multiple Microsoft Sentinel workspaces in the Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2310579).
2. Disconnect the **Subscription-based Microsoft Defender for Cloud (Legacy)** data connector to prevent duplicate alerts.
3. Turn off any analytics rules used to create incidents from Defender for Cloud alerts, either *[Scheduled](/en-us/azure/sentinel/detect-threats-built-in)*[(regular query-type) or](/en-us/azure/sentinel/detect-threats-built-in)*[Microsoft security](/en-us/azure/sentinel/detect-threats-built-in)*[(incident creation)](/en-us/azure/sentinel/detect-threats-built-in) rules.

    If necessary, [use automation rules](/en-us/azure/sentinel/create-manage-use-automation-rules) to close noisy incidents, or use the [built-in tuning capabilities in the Defender portal](/en-us/defender-xdr/investigate-alerts#tune-an-alert) to suppress certain alerts.

For more information, see:

- [Ingest Microsoft Defender for Cloud incidents with Microsoft Defender XDR integration](/en-us/azure/sentinel/ingest-defender-for-cloud-incidents)
- [Discover and manage Microsoft Sentinel out-of-the-box content](/en-us/azure/sentinel/sentinel-solutions-deploy)