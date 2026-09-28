---
layout: Conceptual
title: GCP data connector reference for the Codeless Connector Framework - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/data-connection-rules-reference-gcp
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
description: This article provides reference JSON fields and properties for creating the GCP data connector type and its data connection rules as part of the Codeless Connector Framework.
services: sentinel
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: krishsa
ms.topic: reference
ms.date: 2024-09-30T00:00:00.0000000Z
locale: en-us
document_id: 34ee5f4a-897a-9b33-de5f-b56dce3b7a88
document_version_independent_id: ff31394e-3b3c-ed64-136e-2d938f0c51b7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/data-connection-rules-reference-gcp.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/data-connection-rules-reference-gcp
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/data-connection-rules-reference-gcp.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3439c05e-99ce-45d1-b266-9322ea647316
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/23472108-2f8d-47d2-b07a-c0b1e9d492b6
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 31c04151-6320-e3e7-3cc0-12925801433a
---

# GCP data connector reference for the Codeless Connector Framework - Microsoft Sentinel | Microsoft Learn

To create a Google Cloud Platform (GCP) data connector with the Codeless Connector Framework (CCF), use this reference as a supplement to the [Microsoft Sentinel REST API for Data Connectors](/en-us/rest/api/securityinsights/data-connectors/create-or-update?view=rest-securityinsights-2024-01-01-preview&amp;tabs=HTTP#gcpdataconnector&amp;preserve-view=true) docs.

Each `dataConnector` represents a specific *connection* of a Microsoft Sentinel data connector. One data connector might have multiple connections, which fetch data from different endpoints. The JSON configuration built using this reference document is used to complete the deployment template for the CCF data connector.

For more information, see [Create a codeless connector for Microsoft Sentinel](isv/create-codeless-connector#create-the-deployment-template).

## Build the GCP CCF data connector

Simplify the development of connecting your GCP data source with a sample GCP CCF data connector deployment template.

[**GCP CCF example template**](https://github.com/Azure/Azure-Sentinel/blob/master/DataConnectors/Templates/Connector_GCP_CCP_template.json)

With most of the deployment template sections filled out, you only need to build the first two components, the output table and the DCR. For more information, see the [Output table definition](isv/create-codeless-connector#output-table-definition) and [Data Collection Rule (DCR)](isv/create-codeless-connector#data-collection-rule) sections.

## Data Connectors - Create or update

Reference the [Create or Update](/en-us/rest/api/securityinsights/data-connectors/create-or-update) operation in the REST API docs to find the latest stable or preview API version. The difference between the *create* and the *update* operation is the update requires the **etag** value.

**PUT** method

```http
https://management.azure.com/subscriptions/{{subscriptionId}}/resourceGroups/{{resourceGroupName}}/providers/Microsoft.OperationalInsights/workspaces/{{workspaceName}}/providers/Microsoft.SecurityInsights/dataConnectors/{{dataConnectorId}}?api-version={{apiVersion}}
```

## URI parameters

For more information about the latest API version, see [Data Connectors - Create or Update URI Parameters](/en-us/rest/api/securityinsights/data-connectors/create-or-update#uri-parameters).

| Name | Description |
| --- | --- |
| **dataConnectorId** | The data connector ID must be a unique name and is the same as the `name` parameter in the request body. |
| **resourceGroupName** | The name of the resource group, not case sensitive. |
| **subscriptionId** | The ID of the target subscription. |
| **workspaceName** | The *name* of the workspace, not the ID.Regex pattern: `^[A-Za-z0-9][A-Za-z0-9-]+[A-Za-z0-9]$` |
| **api-version** | The API version to use for this operation. |

## Request body

The request body for a `GCP` CCF data connector has the following structure:

```json
{
   "name": "{{dataConnectorId}}",
   "kind": "GCP",
   "etag": "",
   "properties": {
        "connectorDefinitionName": "",
        "auth": {},
        "request": {},
        "dcrConfig": ""
   }
}

```

### GCP

**GCP** represents a CCF data connector where the paging and expected response payloads for your Google Cloud Platform (GCP) data source has already been configured. Configuring your GCP service to send data to a GCP Pub/Sub must be done separately. For more information, see [Publish message in Pub/Sub overview](https://cloud.google.com/pubsub/docs/publish-message-overview).

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| **name** | True | string | The unique name of the connection matching the URI parameter |
| **kind** | True | string | Must be `GCP` |
| **etag** |  | GUID | Leave empty for creation of new connectors. For update operations, the etag must match the existing connector's etag (GUID). |
| properties.connectorDefinitionName |  | string | The name of the DataConnectorDefinition resource that defines the UI configuration of the data connector. For more information, see [Data Connector Definition](isv/create-codeless-connector#data-connector-user-interface). |
| properties.**auth** | True | Nested JSON | Describes the credentials for polling the GCP data. For more information, see authentication configuration. |
| properties.**request** | True | Nested JSON | Describes the GCP project Id and GCP subscription for polling the data. For more information, see request configuration. |
| properties.**dcrConfig** |  | Nested JSON | Required parameters when the data is sent to a Data Collection Rule (DCR). For more information, see DCR configuration. |

## Authentication configuration

Authentication to GCP from Microsoft Sentinel uses a GCP Pub/Sub. You must configure the authentication separately. Use the Terraform scripts [here](https://github.com/Azure/Azure-Sentinel/blob/master/DataConnectors/GCP/Terraform/sentinel_resources_creation/GCPInitialAuthenticationSetup/GCPInitialAuthenticationSetup.tf). For more information, see [GCP Pub/Sub authentication from another cloud provider](https://cloud.google.com/docs/authentication/provide-credentials-adc#wlif).

As a best practice, use parameters in the auth section instead of hard-coding credentials. For more information, see [Secure confidential input](isv/create-codeless-connector#secure-confidential-input).

In order to create the deployment template which also uses parameters, you need to escape the parameters in this section with an extra starting `[`. This allows the parameters to assign a value based on the user interaction with the connector. For more information, see [Template expressions escape characters](/en-us/azure/azure-resource-manager/templates/template-expressions#escape-characters).

To enable the credentials to be entered from the UI, the `connectorUIConfig` section requires `instructions` with the desired parameters. For more information, see [Data connector definitions reference for the Codeless Connector Framework](data-connector-ui-definitions-reference#instructions).

GCP auth example:

```json
"auth": {
    "serviceAccountEmail": "[[parameters('GCPServiceAccountEmail')]",
    "projectNumber": "[[parameters('GCPProjectNumber')]",
    "workloadIdentityProviderId": "[[parameters('GCPWorkloadIdentityProviderId')]"
}
```

## Request configuration

The request section requires the `projectId` and `subscriptionNames` from the GCP Pub/Sub.

GCP request example:

```json
"request": {
    "projectId": "[[parameters('GCPProjectId')]",
    "subscriptionNames": [
        "[[parameters('GCPSubscriptionName')]"
    ]
}
```

## DCR configuration

| Field | Required | Type | Description |
| --- | --- | --- | --- |
| **DataCollectionEndpoint** | True | String | DCE (Data Collection Endpoint) for example: `https://example.ingest.monitor.azure.com`. |
| **DataCollectionRuleImmutableId** | True | String | The DCR immutable ID. Find it by viewing the DCR creation response or using the [DCR API](/en-us/rest/api/monitor/data-collection-rules/get) |
| **StreamName** | True | string | This value is the `streamDeclaration` defined in the DCR (prefix must begin with *Custom-*) |

## Example CCF data connector

Here's an example of all the components of the `GCP` CCF data connector JSON together.

```json
{
    "kind": "GCP",
    "properties": {
        "connectorDefinitionName": "[[parameters('connectorDefinitionName')]",
        "dcrConfig": {
            "streamName": "[variables('streamName')]",
            "dataCollectionEndpoint": "[[parameters('dcrConfig').dataCollectionEndpoint]",
            "dataCollectionRuleImmutableId": "[[parameters('dcrConfig').dataCollectionRuleImmutableId]"
        },
    "dataType": "[variables('dataType')]",
    "auth": {
        "serviceAccountEmail": "[[parameters('GCPServiceAccountEmail')]",
        "projectNumber": "[[parameters('GCPProjectNumber')]",
        "workloadIdentityProviderId": "[[parameters('GCPWorkloadIdentityProviderId')]"
    },
    "request": {
        "projectId": "[[parameters('GCPProjectId')]",
        "subscriptionNames": [
            "[[parameters('GCPSubscriptionName')]"
            ]
        }
    }
}
```

For more information, see [Create GCP data connector REST API example](/en-us/rest/api/securityinsights/data-connectors/create-or-update?view=rest-securityinsights-2024-01-01-preview&amp;tabs=HTTP#creates-or-updates-a-gcp-data-connector&amp;preserve-view=true).