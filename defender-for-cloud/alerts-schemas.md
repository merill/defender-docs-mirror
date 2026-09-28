---
layout: Conceptual
title: Alerts schema - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/alerts-schemas
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
description: This article describes the different schemas used by Microsoft Defender for Cloud for security alerts.
ms.topic: concept-article
ms.date: 2025-05-18T00:00:00.0000000Z
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: f61760da-cdff-499d-7539-181e0ca001e6
document_version_independent_id: 65ff17ce-73a7-696a-9924-10dc8695f9ec
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/alerts-schemas.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/alerts-schemas
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/alerts-schemas.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 59af38a2-34b8-8fc9-1f44-7b8b64655b00
---

# Alerts schema - Microsoft Defender for Cloud | Microsoft Learn

Defender for Cloud provides alerts that help you identify, understand, and respond to security threats. Alerts are generated when Defender for Cloud detects suspicious activity or a security-related issue in your environment. You can view these alerts in the Defender for Cloud portal, or you can export them to external tools for further analysis and response.

You can view these security alerts in Microsoft Defender for Cloud's pages - [overview dashboard](overview-page), [alerts](manage-respond-alerts), [resource health pages](investigate-resource-health), or [workload protections dashboard](workload-protections-dashboard) - and through external tools such as:

- [Microsoft Sentinel](/en-us/azure/sentinel/) - Microsoft's cloud-native SIEM. The Sentinel Connector gets alerts from Microsoft Defender for Cloud and sends them to the [Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace) for Microsoft Sentinel.
- Third-party SIEMs - Send data to [Azure Event Hubs](/en-us/azure/event-hubs/). Then integrate your Event Hubs data with a third-party SIEM. Learn more in [Stream alerts to a SIEM, SOAR, or IT Service Management solution](export-to-siem).
- [The REST API](/en-us/rest/api/defenderforcloud-composite/operation-groups?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true) - If you're using the REST API to access alerts, see the [online Alerts API documentation](/en-us/rest/api/defenderforcloud-composite/alerts?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true).

If you're using any programmatic methods to consume the alerts, you need the correct schema to find the fields that are relevant to you. Also, if you're exporting to an Event Hubs or trying to trigger Workflow Automation with generic HTTP connectors, schemas should be utilized to properly parse the JSON objects.

Important

Since the schema is different for each of these scenarios, ensure you select the relevant tab.

## The schemas

# [Microsoft Sentinel](#tab/schema-sentinel)
The Sentinel Connector gets alerts from Microsoft Defender for Cloud and sends them to the Log Analytics Workspace for Microsoft Sentinel.

To create a Microsoft Sentinel case or incident using Defender for Cloud alerts, you need the schema for those alerts shown.

Learn more in the [Microsoft Sentinel documentation](/en-us/azure/sentinel/).

### The data model of the schema

| Field | Description |
| --- | --- |
| **AlertName** | Alert display name |
| **AlertType** | unique alert identifier |
| **ConfidenceLevel** | (Optional) The confidence level of this alert (High/Low) |
| **ConfidenceScore** | (Optional) Numeric confidence indicator of the security alert |
| **Description** | Description text for the alert |
| **DisplayName** | The alert's display name |
| **EndTime** | The effect end time of the alert (the time of the last event contributing to the alert) |
| **Entities** | A list of entities related to the alert. This list can hold a mixture of entities of diverse types |
| **ExtendedLinks** | (Optional) A bag for all links related to the alert. This bag can hold a mixture of links for diverse types |
| **ExtendedProperties** | A bag of extra fields, which are relevant to the alert |
| **IsIncident** | Determines if the alert is an incident or a regular alert. An incident is a security alert that aggregates multiple alerts into one security incident |
| **ProcessingEndTime** | UTC timestamp in which the alert was created |
| **ProductComponentName** | (Optional) The name of a component inside the product, which generated the alert. |
| **ProductName** | constant ('Azure Security Center') |
| **ProviderName** | unused |
| **RemediationSteps** | Manual action items to take to remediate the security threat |
| **ResourceId** | Full identifier of the affected resource |
| **Severity** | The alert severity (High/Medium/Low/Informational) |
| **SourceComputerId** | a unique GUID for the affected server (if the alert is generated on the server) |
| **SourceSystem** | unused |
| **StartTime** | The effect start time of the alert (the time of the first event contributing to the alert) |
| **SystemAlertId** | Unique identifier of this security alert instance |
| **TenantId** | the identifier of the parent Microsoft Entra ID tenant of the subscription under which the scanned resource resides |
| **TimeGenerated** | UTC timestamp on which the assessment took place (Security Center's scan time) (identical to DiscoveredTimeUTC) |
| **Type** | constant ('SecurityAlert') |
| **VendorName** | The name of the vendor that provided the alert (for example, 'Microsoft') |
| **VendorOriginalId** | unused |
| **WorkspaceResourceGroup** | in case the alert is generated on a Virtual Machine (VM), Server, Virtual Machine Scale Set, or App Service instance that reports to a workspace, contains that workspace resource group name |
| **WorkspaceSubscriptionId** | in case the alert is generated on a VM, Server, Virtual Machine Scale Set, or App Service instance that reports to a workspace, contains that workspace subscriptionId |
|  |  |

# [Azure Activity Log](#tab/schema-activitylog)
Microsoft Defender for Cloud audits generated Security alerts as events in Azure Activity Log.

You can view the security alerts events in Activity Log by searching for the Activate Alert event as shown:

[![Searching the Activity log for the Activate Alert event.](media/alerts-schemas/sample-activity-log-alert.png)](media/alerts-schemas/sample-activity-log-alert.png#lightbox)

### Sample JSON for alerts sent to Azure Activity Log

```json
{
    "channels": "Operation",
    "correlationId": "2518250008431989649_e7313e05-edf4-466d-adfd-35974921aeff",
    "description": "PREVIEW - Role binding to the cluster-admin role detected. Kubernetes audit log analysis detected a new binding to the cluster-admin role which gives administrator privileges.\r\nUnnecessary administrator privileges might cause privilege escalation in the cluster.",
    "eventDataId": "2518250008431989649_e7313e05-edf4-466d-adfd-35974921aeff",
    "eventName": {
        "value": "PREVIEW - Role binding to the cluster-admin role detected",
        "localizedValue": "PREVIEW - Role binding to the cluster-admin role detected"
    },
    "category": {
        "value": "Security",
        "localizedValue": "Security"
    },
    "eventTimestamp": "2019-12-25T18:52:36.801035Z",
    "id": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RESOURCE_GROUP_NAME/providers/Microsoft.Security/locations/centralus/alerts/2518250008431989649_e7313e05-edf4-466d-adfd-35974921aeff/events/2518250008431989649_e7313e05-edf4-466d-adfd-35974921aeff/ticks/637128967568010350",
    "level": "Informational",
    "operationId": "2518250008431989649_e7313e05-edf4-466d-adfd-35974921aeff",
    "operationName": {
        "value": "Microsoft.Security/locations/alerts/activate/action",
        "localizedValue": "Activate Alert"
    },
    "resourceGroupName": "RESOURCE_GROUP_NAME",
    "resourceProviderName": {
        "value": "Microsoft.Security",
        "localizedValue": "Microsoft.Security"
    },
    "resourceType": {
        "value": "Microsoft.Security/locations/alerts",
        "localizedValue": "Microsoft.Security/locations/alerts"
    },
    "resourceId": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RESOURCE_GROUP_NAME/providers/Microsoft.Security/locations/centralus/alerts/2518250008431989649_e7313e05-edf4-466d-adfd-35974921aeff",
    "status": {
        "value": "Active",
        "localizedValue": "Active"
    },
    "subStatus": {
        "value": "",
        "localizedValue": ""
    },
    "submissionTimestamp": "2019-12-25T19:14:03.5507487Z",
    "subscriptionId": "SUBSCRIPTION_ID",
    "properties": {
        "clusterRoleBindingName": "cluster-admin-binding",
        "subjectName": "for-binding-test",
        "subjectKind": "ServiceAccount",
        "username": "masterclient",
        "actionTaken": "Detected",
        "resourceType": "Kubernetes Service",
        "severity": "Low",
        "intent": "[\"Persistence\"]",
        "compromisedEntity": "ASC-IGNITE-DEMO",
        "remediationSteps": "[\"Review the user in the alert details. If cluster-admin is unnecessary for this user, consider granting lower privileges to the user.\"]",
        "attackedResourceType": "Kubernetes Service"
    },
    "relatedEvents": []
}
```

### The data model of the schema

| Field | Description |
| --- | --- |
| **channels** | Constant, "Operation" |
| **correlationId** | The Microsoft Defender for Cloud alert ID |
| **description** | Description of the alert |
| **eventDataId** | See correlationId |
| **eventName** | The value and localizedValue subfields contain the alert display name |
| **category** | The value and localizedValue subfields are constant - "Security" |
| **eventTimestamp** | UTC timestamp for when the alert was generated |
| **id** | The fully qualified alert ID |
| **level** | Constant, "Informational" |
| **operationId** | See correlationId |
| **operationName** | The value field is constant - `Microsoft.Security/locations/alerts/activate/action`, and the localized value is `Activate Alert` (can potentially be localized par the user locale) |
| **resourceGroupName** | Includes the resource group name |
| **resourceProviderName** | The value and localizedValue subfields are constant - "Microsoft.Security" |
| **resourceType** | The value and localizedValue subfields are constant - "Microsoft.Security/locations/alerts" |
| **resourceId** | The fully qualified Azure resource ID |
| **status** | The value and localizedValue subfields are constant - "Active" |
| **subStatus** | The value and localizedValue subfields are empty |
| **submissionTimestamp** | The UTC timestamp of event submission to Activity Log |
| **subscriptionId** | The subscription ID of the compromised resource |
| **properties** | A JSON bag of other properties pertaining to the alert. Properties can change from one alert to the other, however, the following fields appear in all alerts:- severity: The severity of the attack- compromisedEntity: The name of the compromised resource- remediationSteps: Array of remediation steps to be taken- intent: The kill-chain intent of the alert. Possible intents are documented in the [Intentions table](alerts-reference#mitre-attck-tactics) |
| **relatedEvents** | Constant - empty array |

# [Workflow automation](#tab/schema-workflow-automation)
For the alerts schema when using workflow automation, see the [connectors documentation](/en-us/connectors/ascalert/).

# [Continuous export](#tab/schema-continuousexport)
Defender for Cloud's continuous export feature passes alert data to:

- Azure Event Hubs using the same schema as [the alerts API](/en-us/rest/api/defenderforcloud-composite/alerts?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true).
- Log Analytics workspaces according to the [SecurityAlert schema](/en-us/azure/azure-monitor/reference/tables/SecurityAlert) in the Azure Monitor data documentation.

# [MS Graph API](#tab/schema-graphapi)
Microsoft Graph is the gateway to data and intelligence in Microsoft 365. It provides a unified programmability model that you can use to access the tremendous amount of data in Microsoft 365, Windows 10, and Enterprise Mobility + Security. Use the wealth of data in Microsoft Graph to build apps for organizations and consumers that interact with millions of users.

The schema and a JSON representation for security alerts sent to MS Graph, are available in [the Microsoft Graph documentation](/en-us/graph/api/resources/alert).

---