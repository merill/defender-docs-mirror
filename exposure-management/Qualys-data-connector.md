---
layout: Conceptual
title: Qualys data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/qualys-data-connector
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to the Qualys data connector in Microsoft Security Exposure Management.
ms.topic: overview
ms.date: 2026-07-16T00:00:00.0000000Z
locale: en-us
document_id: b4e04133-3998-f06f-c706-5963f2438d0d
document_version_independent_id: b4e04133-3998-f06f-c706-5963f2438d0d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/Qualys-data-connector.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: qualys-data-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/Qualys-data-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 593c23a7-74f4-50de-3b04-adfdcd5af42f
---

# Qualys data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

To integrate with Qualys, you have to provide basic credentials for a Qualys user with **Manager** role or a **Reader** role with full scope.

## Qualys configuration

1. To set up the Qualys integration, you need the API\_URL of your Qualys instance, such as “qualysapi.qg1.apps.qualys.co.uk”. You can find it [here](https://www.qualys.com/platform-identification/).
    1. If you can't find it:
        1. Sign in to your Qualys account.
        2. Go to **Help** → **About**.
        3. You'll see the required information under **Security Operations Center** (SOC).
2. You'll need credentials of a user with at least **Read Asset**permissions to successfully retrieve data from the connector. To create a user with a Read Asset role:
    1. Sign in to Qualys.
    2. Go to **Administration** area.
    3. Go to the **Role Management** section.
    4. Select New Role.
    5. Provide a role name, for example, "Read Asset."
    6. For the Role permissions, check API Access.
    7. From the **Modules** drop down, choose Asset View.
    8. To limit the permissions, choose the **Change** option within the **Asset View** selected module.
    9. Make sure to enable, at least, **Read Asset** under **Asset Management Permissions**.
3. Add the newly created role to the user you intend to authenticate with in the Exposure Management Qualys Connector.
    1. Under **Administration** go to **User** **Management**.
    2. Select the user you onboarded with the Exposure Management Qualys Connector and choose **Edit**.
    3. Under **Roles and Scopes**, add the Read Asset role created in previous sections to the user assigned roles.
    4. Under **Edit** scope, select **Allow user view access to all objects** to allow this user full scope.
    5. Save the **Read Asset** role assignment to the user.

## Establish Qualys connection in Exposure Management

To establish a connection with Qualys in Exposure Management, follow these steps:

1. Open the [Data Connectors](https://security.microsoft.com/exposure-data-connectors) from the Exposure Management navigation and select **Connect** in the Qualys tile.
2. Enter your Qualys API URL and authentication credentials and select **Connect**.

## Retrieved data

Qualys connector retrieves data on compute devices, including machines and virtual machines, and vulnerability findings from Qualys on those assets. It also retrieves some networking data to identify those devices.

| Category | Properties |
| --- | --- |
| **Assets/devices** | - Gateway address- FQDN- IP address- MAC address- OS information- Qualys criticality data |
| **Vulnerability findings** | Qualys retrieves CVE findings on the assets that it ingests. |

## Troubleshooting the Qualys data connector

Here are some common issues that might arise when configuring the Qualys Connector, and suggestions for how to resolve them.

| Error Type | Troubleshooting Action |
| --- | --- |
| **Error code** 401: Authorization failure | An authorization failure indicates that credentials might not be correct, or there might not be sufficient permissions to access the Qualys data. Check your credentials and make sure they're correct and valid. Also check that your credentials have the required permissions. See the Qualys configuration section for details on how to assign the appropriate role and scope. You can validate your user credentials by running the following command:curl -u "user:password" -H "X-Requested-With: Curl" -X "POST"-d "action=list" "`https://qualysapi.qg1.apps.qualys.ca/qps/rest/2.0/search/am/hostasset`" &gt;output.txt |
| **Error code** 409: Possible insufficient permissions | Qualys connector utilizes the knowledge\_base API, which requires specific permissions. You can see more details in the KnowledgeBase section of [this Qualys API document](https://cdn2.qualys.com/docs/qualys-api-vmpc-user-guide.pdf). To validate the provided user has sufficient permissions, run the following command and verify it succeeds:curl -u "user:password" -H "X-Requested-With: Curl" -X "POST"-d "action=list""`https://qualysapi.qg1.apps.qualys.ca/api/2.0/fo/knowledge_base/vuln/`" &gt;output.txt In case it fails, refer to Qualys documentation to mitigate. |
| **Error code 403:** Access forbidden error | This error indicates that the provided credentials lack the necessary permissions to run the requested APIs. Update your credentials with the proper permissions as described in the configuration section, and make sure they have at minimum the Read Asset permissions. |
| **Error code 404:** Not found error | This error indicates that the requested endpoint wasn't found to be reachable. Verify that your Qualys API endpoint is correct, see the configuration section for details. |
| **Error code 429** 'Too many requests" | The system periodically pulls data from the configured external providers, which might have a limit on the number of concurrent requests. We recommend creating a dedicated user or account for the connector to avoid reaching this limit. |
| 'Temporary disconnected' or 'Temporary failure' error message | In the case where this error message appears without any additional information, verify the connector configuration (API endpoint and credentials). If they're valid and the issue doesn't resolve on its own, contact Support. |
| Not seeing my assets or the vulnerabilities reported by Qualys in the ingested data | See Retrieved data for a description of the data expected to be retrieved by the Qualys connector. If there's still missing data, contact Support. |
| Qualys allowed IPs need to be configured to enable Exposure Management connectors to access Qualys | Read how to add the set of IPs to add to your allowlist here: [Allowlist IP addresses](configure-data-connectors#allowlist-ip-addresses). |