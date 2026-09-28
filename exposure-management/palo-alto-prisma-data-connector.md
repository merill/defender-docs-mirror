---
layout: Conceptual
title: Palo Alto Prisma data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/palo-alto-prisma-data-connector
author: dlanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to integrate the Palo Alto Prisma data connector in Microsoft Security Exposure Management.
ms.topic: overview
ms.date: 2025-09-09T00:00:00.0000000Z
locale: en-us
document_id: 4b5a13ad-6d96-8a61-7dc2-22db779620cb
document_version_independent_id: 4b5a13ad-6d96-8a61-7dc2-22db779620cb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/palo-alto-prisma-data-connector.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: palo-alto-prisma-data-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/palo-alto-prisma-data-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2624a017-7337-44fa-9494-a407bb0e59fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
- https://authoring-docs-microsoft.poolparty.biz/devrel/a438284e-c3c3-4c36-ab0b-aa7c244b912c
platformId: 689e77d0-24ab-4e4c-dbae-882aae0fca8d
---

# Palo Alto Prisma data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

To integrate with Palo Alto Prisma, you need to provide an authentication endpoint API URL, and a valid Access Key and Secret Key generated using a Palo Alto service account.

Note

We recommend creating a dedicated service account for use with data connectors in Exposure Management.

## Palo Alto Prisma configuration

First, you need to create a service account with the required permissions to get the Access Key and Secret Key.

Note

To create a Palo Alto API Client, you must be logged in as a user with the System Admin role.

### Add an API Client

1. Log in to your Palo Alto Prisma account with the required permissions.
2. Go to **Settings** &gt; **Access Control** &gt; **Access keys**.
3. Click **Add**, then **Access key**.
4. Enter a meaningful **Access Key Name**, then click **Save**.
5. Copy and save the **Access Key ID** and **Secret Access Key** that appears.
6. Close the credential window.

## Establish Palo Alto Prisma connection in Exposure Management

To establish a connection with Palo Alto Prisma in Exposure Management, follow these steps:

1. Open the [Exposure Management Connectors](https://security.microsoft.com/exposure-data-connectors) page and click **Connect** in the Palo Alto tile.
2. Enter your Palo Alto **Endpoint** and authentication credentials, then click **Connect**.

## Retrieved data

The Palo Alto Prisma connector retrieves data on compute devices. This data includes virtual machines and cloud resources, along with vulnerability findings and configuration data from Palo Alto Prisma on those assets. It also retrieves network and configuration information to identify those devices.

| **Category** | **Properties** |
| --- | --- |
| **Assets/devices** | - Cloud provider information- Resource type- Network interfaces- IP address- Public DNS name- Operating system details- Internet facing- Palo Alto criticality data |
| **Vulnerability findings** | Palo Alto Prisma retrieves CVE findings on the assets that it ingests. |

## Troubleshooting the Palo Alto Prisma data connector

Here are some common issues that might arise when configuring the Palo Alto Prisma Connector, and suggestions for how to resolve them.

| **Error Type** | **Troubleshooting Action** |
| --- | --- |
| **Authorization failure** | Check your credentials and make sure they're correct and valid. Also check that your credentials have the required permissions. See the Palo Alto configuration section for details on how to assign the appropriate roles. |
| **Access forbidden error** | This error indicates that the provided credentials lack the necessary permissions to run the requested APIs. Update your credentials with the proper permissions as described in the configuration section. |
| **Not found error** | This error indicates that the requested endpoint wasn't found to be reachable. Verify that your Palo Alto authentication endpoint URL is correct, see the configuration section for details. |
| **Too many requests** | The system periodically pulls data from the configured external providers, which might have a limit on the number of concurrent requests. We recommend creating a dedicated service account for the connector to avoid reaching this limit. |
| 'Temporary disconnected' or 'Temporary failure' error message | Verify the connector configuration (authentication endpoint URL and credentials). If the configuration is valid and the issue doesn't resolve on its own, contact Support. |
| Not seeing my assets or the vulnerabilities reported by Palo Alto Prisma in the ingested data | See Retrieved data for a description of the expected retrieved data by the Palo Alto Prisma connector. If there's still missing data, contact Support. |