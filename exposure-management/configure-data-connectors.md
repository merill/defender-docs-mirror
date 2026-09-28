---
layout: Conceptual
title: Configure your data connectors in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/configure-data-connectors
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn about Configure your data connectors in Microsoft Security Exposure Management.
ms.topic: overview
ms.date: 2026-06-30T00:00:00.0000000Z
ms.custom: sfi-ga-nochange
locale: en-us
document_id: feb57bcd-65a5-bbee-a402-ee0af2670a1c
document_version_independent_id: feb57bcd-65a5-bbee-a402-ee0af2670a1c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/configure-data-connectors.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-data-connectors
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/configure-data-connectors.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: cfa2942d-ff72-5056-db84-4f7d68b2598b
---

# Configure your data connectors in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

[Microsoft Security Exposure Management](microsoft-security-exposure-management) consolidates security posture data from all your digital assets, enabling you to map your attack surface and focus your security efforts on areas at greatest risk. Data from Microsoft Security products like Microsoft Defender for Endpoint, Microsoft Defender for Identity, Microsoft Defender for Cloud, Microsoft Entra ID, and others are automatically ingested and consolidated within Exposure Management. You can further enrich and extend this data by connecting to a range of external data sources.

## Prerequisites

The following prerequisites are required to integrate external data connecters to Microsoft Security Exposure Management.

### Roles & permissions

For full access to connect and disconnect the data connectors you need one of the following Microsoft Entra ID roles:

- Global Admin (read and write permissions)
- Security Admin (read and write permissions)
- Security Operator (read and limited write permissions)

To view the status of the connectors, you can use one of the following roles:

- Global Reader (read permissions)
- Security Reader (read permissions)

You can also use [Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac) with the following permissions: - **Exposure Management (read)** for read-only access to Exposure Management experiences - **Exposure Management (manage)** for full access to manage Exposure Management experiences - **Core security settings (manage)** for connecting or changing vendor configurations (located under Authorization and settings category)

You can find more details about the permission levels in [Prerequisites and support](prerequisites) and the full list of available permissions in [Permissions in Microsoft Defender unified RBAC](/en-us/defender-xdr/custom-permissions-details).

## Establish a connection

To establish a connection with any of the supported external products, follow these steps:

Note

**OT data connectors** use a different setup flow in the Microsoft Defender portal. To configure Armis, Dragos, or Forescout, see [OT data connectors](ot-data-connectors).

1. Complete the applicable prerequisite steps for your external data connectors. Each connector has the following explicit instructions for setting up valid credentials and creating the connection:

    - [ServiceNow CMDB](servicenow-data-connector)
    - [Qualys VM](qualys-data-connector)
    - [Rapid7 VM](rapid7-data-connector)
    - [Tenable](tenable-data-connector)
    - [Armis](armis-data-connector)
    - [Dragos](dragos-data-connector)
    - [Forescout](forescout-data-connector)
    - [Wiz](wiz-data-connector)
    - [Palo Alto Prisma](palo-alto-prisma-data-connector)
2. Go to **Data Connectors** in the Exposure Management navigation.
3. Select **Connect** on the selected data connector from the external connectors catalog.
4. A side pane opens with the relevant connectivity details. Fill in the required fields and select **Connect**.
5. The data connector is now connected and starts ingesting data from the external source.

Note

It might take several hours for the connectors data to propagate to all experiences after the data connector is configured.

## Allowlist IP addresses

To ensure successful connections between Exposure Management and external products, you might need to allowlist specific Microsoft IP addresses.

These allowlist steps apply to external data connectors, including OT data connectors, when the external product requires Microsoft IP addresses to be allowed.

Follow these steps to obtain the required IP addresses and configure it with the external products:

1. Identify the IP addresses:
    1. Obtain and copy the list of the IPs for your allowlist from the IP ranges under "Scuba" in the public IP ranges reference here: [Download Azure IP Ranges and Service Tags – Public Cloud from Official Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=56519)
2. Access the external product's configuration settings:
    1. Sign in to the external product's administration or configuration portal.
    2. Navigate to the section where you can manage network settings or security settings.
3. Add the IP addresses to the allowlist:
    1. Locate the allowlist.
    2. Enter the IP addresses that you obtained in step 1.
    3. Save the changes to update the allowlist.
4. Verify the connection:
    1. After updating the allowlist, verify that the connection between the external product and our system is successful.
    2. Check for any error messages or connection issues and ensure that the allowlisted IP addresses are correctly configured.
5. Troubleshooting:
    1. If you encounter any issues, double-check the IP addresses and ensure they're correctly entered.
    2. Refer to the external product's documentation for more troubleshooting steps or contact their support team for assistance.

For specific instructions on allowlisting IP addresses for each external product, refer to their respective documentation or support resources.