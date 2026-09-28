---
layout: Conceptual
title: Wiz data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/wiz-data-connector
author: dlanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to set up the Wiz data connector in Microsoft Security Exposure Management.
ms.topic: overview
ms.date: 2025-08-27T00:00:00.0000000Z
locale: en-us
document_id: eac54f9b-e502-66ba-d531-362f4a67984f
document_version_independent_id: eac54f9b-e502-66ba-d531-362f4a67984f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/wiz-data-connector.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: wiz-data-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/wiz-data-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/97159432-14a9-4307-a469-d2f2c75f0e33
- https://authoring-docs-microsoft.poolparty.biz/devrel/2624a017-7337-44fa-9494-a407bb0e59fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
- https://authoring-docs-microsoft.poolparty.biz/devrel/50565c62-5f6b-4687-be38-323113c72c2e
- https://authoring-docs-microsoft.poolparty.biz/devrel/a438284e-c3c3-4c36-ab0b-aa7c244b912c
platformId: 66d3e876-3c94-6644-17db-a42df03c995d
---

# Wiz data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

To integrate with Wiz, you need to provide an authentication endpoint URL, and a valid Client ID and Client Secret generated using a Wiz service account.

Note

We recommend creating a dedicated user for use with data connectors in Exposure Management.

## Wiz configuration

First, you need to create a service account with the required permissions to get the authentication endpoint URL, Client ID, and Client Secret.

Note

To create a service account, you must be logged in as a Wiz user with Write (W) permission on service accounts. Project-scoped roles can create service accounts only on their own projects.

### Add a service account

1. Go to the **Settings** &gt; **Access Management** &gt; **Service Accounts** page, then select **Add Service Account**.
2. Enter a meaningful **Name** for the account.
3. Choose the **Type** of service account to add. It should be **Custom Integration (GraphQL API)**
4. You can select to limit access to specific projects only by choosing up to 50 projects from the drop-down list. If you aren't sure which project to choose, it's better to leave it empty.
5. You can set an **Expiration date** for the service account, though we recommend leaving it empty.
6. Set the **API Scopes** to **Read graph resource** and **Read vulnerabilities**

    Note

    At minimum, the service account should have permissions of Read graph resources and Read vulnerabilities. We recommend Read:all permissions because more data might be retrieved as the connector is further developed.
7. Select **Add Service Account**. The secret credentials dialog shows the newly created Client ID and Client Secret for the service account.
8. Copy the Client ID and Client Secret to a secure place, such as a password management tool.
9. Select **Finish**.

### Get the authentication endpoint URL

1. At the top right of the Wiz portal, select **Profile** &gt; **Tenant Info**[Direct link](https://app.wiz.io/tenant-info/general)
2. `API Endpoint URL` - Copy the endpoint in the following form: `https://api.<TENANT_DATA_CENTER>.app.wiz.io/`

## Establish Wiz connection in Exposure Management

To establish a connection with Wiz in Exposure Management, follow these steps:

1. Open the [Data Connectors](https://security.microsoft.com/exposure-data-connectors) from the Exposure Management navigation and select **Connect** in the Wiz tile.
2. Enter your Wiz authentication data and select **Connect**.

## Retrieved data

Wiz connector retrieves data on compute devices. This data includes virtual machines and cloud resources, along with vulnerability findings and configuration data from Wiz on those assets. It also retrieves network and configuration information to identify those devices.

| **Category** | **Properties** |
| --- | --- |
| **Assets/devices** | - Cloud provider information- Network Interfaces- IP addresses- Virtual Machine Properties (Device name, Cloud provider ID)- Operating system details- Has high or Admin Privileges- Open to Internet or Internet facing- Contains sensitive data- Instance type- Is Container Host- Is Ephemeral- isManaged- Tags- Wiz projects- First seen- Last seen- Wiz Criticality |
| **Vulnerability findings** | Wiz retrieves common vulnerabilities and exposures (CVE) findings on the assets that it ingests. |

## Troubleshooting the Wiz data connector

Here are some common issues that might arise when configuring the Wiz Connector, and suggestions for how to resolve them.

| **Error Type** | **Troubleshooting Action** |
| --- | --- |
| **Error code 401**: Authorization failure | An authorization failure indicates that credentials might not be correct, or there might not be sufficient permissions to access the Wiz data. Check your credentials and make sure they're correct and valid. Also check that your credentials have the required permissions. See the Wiz configuration section for details on how to assign the appropriate scopes. You can validate your credentials by testing the authentication endpoint with your Client ID and Client Secret. |
| **Error code 403:** Access forbidden error | This error indicates that the provided credentials lack the necessary permissions to run the requested APIs. Update your credentials with the proper permissions as described in the configuration section. Make sure they have at minimum the "Read graph resources" and "Read vulnerabilities" permissions. |
| **Error code 404:** Not found error | This error indicates that the requested endpoint wasn't found to be reachable. Verify that your Wiz authentication endpoint URL is correct, see the configuration section for details. |
| **Error code 429** 'Too many requests' | The system periodically pulls data from the configured external providers, which might have a limit on the number of concurrent requests. Creating a dedicated service account for the connector helps avoid reaching this limit. |
| 'Temporary disconnected' or 'Temporary failure' error message | If this error message appears without any additional information, verify the connector configuration (authentication endpoint URL and credentials). If the configuration is valid and the issue doesn't resolve on its own, contact support. |
| Not seeing my assets or the vulnerabilities reported by Wiz in the ingested data | See Retrieved data for a description of the expected retrieved data by the Wiz connector. If there's still missing data, contact Support. |
| Wiz allowed IPs need to be configured to enable Exposure Management connectors to access Wiz | Read how to add the set of IPs to add to your allow list here: [Allow list IP addresses](configure-data-connectors#allowlist-ip-addresses). |