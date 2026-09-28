---
layout: Conceptual
title: Update SAP connector and DCR settings - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/update-sap-connector-data-collection-rule
breadcrumb_path: ../breadcrumb/toc.json
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
ms.reviewer: mapankra
description: Update Microsoft Sentinel SAP connector polling settings and data collection rules without disconnecting the connector.
ms.author: mapankra
author: MartinPankraz
ms.topic: how-to
ms.date: 2026-08-10T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
locale: en-us
document_id: daaad522-c371-0c00-14f7-db35cca81fb0
document_version_independent_id: 1b14647c-36a7-43e0-1ca9-47e9f449b94c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/update-sap-connector-data-collection-rule.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/update-sap-connector-data-collection-rule
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/update-sap-connector-data-collection-rule.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 0de85be5-ef93-7428-255c-48bfde10c70d
---

# Update SAP connector and DCR settings - Microsoft Sentinel | Microsoft Learn

Update the SAP data connector or its data collection rule (DCR) independently to tune collection settings without disconnecting SAP systems. You don't need to update both resources. This article shows one option for each resource: Azure API Playground for the connector and the Azure portal template experience for the DCR.

Important

Update the active `dataConnectors` resource, not the connector-definition resource. The DCR might be shared by multiple connectors, so review its impact before you deploy DCR changes.

Important

Changing polling frequency or other defaults can affect SAP and SAP Integration Suite performance, ingestion latency, and Microsoft Sentinel costs. A shorter interval might increase source-system load, while a longer interval might delay detections or create a backlog. Test changes on one connector first, monitor connector health and ingestion volume, and then roll out the change to other systems. For more guidance, see [Run the agentless SAP connector cost-efficiently](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/run-agentless-sap-connector-cost-efficiently/4464781).

## Update a data connector with API Playground

Several options are available for updating a data connector, including REST API clients and scripts. The following procedure shows one option using [Azure API Playground](https://portal.azure.com/?feature.customportal=false#view/Microsoft_Azure_Resources/ArmPlayground.ReactView).

### SAP BTP connector

1. Use the [Data Connectors - List](/en-us/rest/api/securityinsights/data-connectors/list) operation. Select the latest preview API version in the reference. For example:

    ```http
    GET /subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.OperationalInsights/workspaces/<workspace-name>/providers/Microsoft.SecurityInsights/dataConnectors?api-version=<api-version>-preview
    ```
2. In the response, locate the target connector in the `value` array. Copy its `id`.
3. Use the copied `id` as the URL for a `PUT` request. Use the existing connector properties as the starting point, and change only the settings you need.

    The following SAP BTP example changes the polling frequency. `queryWindowInMin` is the polling-frequency field.

    ```json
    {
      "id": "<connector-resource-id>",
      "name": "<connector-id>",
      "type": "Microsoft.SecurityInsights/dataConnectors",
      "kind": "RestApiPoller",
      "properties": {
        "dataType": "SAPBTPAuditLog_CL",
        "connectorDefinitionName": "SAPBTPAuditEvents",
        "addOnAttributes": {
          "SubaccountName": "<subaccount-name>"
        },
        "auth": {
          "ClientSecret": "<client-secret>",
          "ClientId": "<client-id>",
          "grantType": "client_credentials",
          "tokenEndpoint": "<token-endpoint>",
          "type": "OAuth2"
        },
        "request": {
          "apiEndpoint": "<api-endpoint>/auditlog/v2/auditlogrecords",
          "queryWindowInMin": 1
        }
      }
    }
    ```

    Retrieve `<client-id>`, `<client-secret>`, `<token-endpoint>`, and `<api-endpoint>` from the SAP BTP auditlog-management service key: `uaa.clientid`, `uaa.clientsecret`, `uaa.url`, and `url`. For details, see [Set up the BTP subaccount and solution](deploy-sap-btp-solution#set-up-the-btp-subaccount-and-solution). The list API response omits the client ID and client secret, so read them from your secure store and don't submit blank credential values.
4. Select **Send**. The update might take several minutes to become active.

### SAP applications agentless connector

The SAP BTP and SAP applications agentless connectors use different request properties. For the SAP applications agentless connector, use the existing connector `id` and include the SAPCC definition. If the RFC destination changes, update the `rfcDestinationName` header. For example:

```json
{
  "id": "<connector-resource-id>",
  "name": "<connector-id>",
  "type": "Microsoft.SecurityInsights/dataConnectors",
  "kind": "RestApiPoller",
  "properties": {
    "dataType": "SentinelHealth",
    "connectorDefinitionName": "SAPCC",
    "auth": {
      "GrantType": "client_credentials",
      "ClientSecret": "<client-secret>",
      "ClientId": "<client-id>",
      "tokenEndpoint": "<token-endpoint>?grant_type=client_credentials",
      "type": "OAuth2"
    },
    "request": {
      "apiEndpoint": "<integration-suite-endpoint>/http/microsoft/sentinel/sap-log-trigger",
      "rateLimitQPS": 2,
      "queryWindowInMin": 1,
      "queryTimeFormat": "yyyy-MM-ddTHH:mm:ss.000000+00:00",
      "retryCount": 1,
      "timeoutInSeconds": 180,
      "headers": {
        "rfcDestinationName": "<rfc-destination-name>"
      },
      "startTimeAttributeName": "startTimeUTC",
      "endTimeAttributeName": "endTimeUTC"
    }
  }
}
```

Keep the existing SAPCC properties unless you intend to change them. Use the full resource returned by the list operation as your starting point, and preserve any properties not shown in this minimal example.

Retrieve `<client-id>`, `<client-secret>`, `<token-endpoint>`, and `<integration-suite-endpoint>` from the SAP BTP Process Integration Runtime service key: `clientid`, `clientsecret`, `tokenurl`, and `url`. For details, see [Connect your agentless data connector](deploy-data-connector-agentless#connect-your-agentless-data-connector). The list API response omits the client ID and client secret, so read them from your secure store and don't submit blank credential values.

Keep `queryTimeFormat`, `startTimeAttributeName`, and `endTimeAttributeName` together. They define how the poller supplies the time window to the SAP Data Collector endpoint.

For the full SAP BTP field mapping, see the [SAP BTP polling configuration](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/SAP%20BTP/Data%20Connectors/SAPBTPPollerConnector/SAPBTP_PollingConfig.json). For the SAP applications agentless field mapping, see the [SAP Integration Suite tools](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/SAP/Tools/IntegrationSuite).

## Update the DCR with an exported template

Several options are available for updating a DCR, including REST API clients, scripts, and ARM templates. The following procedure shows one portal-based option using an exported template.

1. In the Azure portal, open the DCR and select **Automation** &gt; **Export template**.
2. Select **Copy**, to store the well-formatted template JSON.
3. Select **Deploy**, then on the next screen select **Edit template** and paste the copied JSON into the editor.
4. Change only the required DCR properties (**streamDeclarations** and **dataFlows**) and keep the resource name unchanged.
5. Select **Review + create**, then select **Create**.

Wait for the deployment to complete and for the DCR change to take effect. Verify connector health and new data in the relevant SAP tables before relying on the update.

For more detail about selectively updating SAP-related DCR data flows, see the SAP community blog [Activating Advanced Security Information Model (ASIM) LogServ with Sentinel for SAP RISE](https://community.sap.com/t5/enterprise-resource-planning-blog-posts-by-members/activating-advanced-security-information-model-logserv-with-sentinel-for/ba-p/14454303).

## Automate updates at scale

For mass onboarding and updates, use the API and CLI-based approaches in [Deploy the Microsoft Sentinel solution for SAP BTP](deploy-sap-btp-solution#mass-onboard-sap-btp-subaccounts-at-scale) and [Connect your SAP system to Microsoft Sentinel](deploy-data-connector-agentless#mass-onboard-sap-systems-at-scale).