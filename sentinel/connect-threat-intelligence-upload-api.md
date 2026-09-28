---
layout: Conceptual
title: Connect your TIP with the upload API (Preview) - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-threat-intelligence-upload-api
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
description: Connect a threat intelligence platform or custom feed to Microsoft Sentinel by using the preview upload API. Learn the prerequisites and how STIX-supported uploads ingest indicators without a data connector.
ms.author: pauloliveria
author: poliveria
ms.reviewer: yoninave
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 27ce0d6d-e80e-0611-3acf-e57e009f4d66
document_version_independent_id: fa7542e5-fe5b-59a5-a711-226fb1652cbe
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-threat-intelligence-upload-api.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-threat-intelligence-upload-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-threat-intelligence-upload-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 84e55a89-b0bf-acb7-e6ec-c2b7a99f5a3d
---

# Connect your TIP with the upload API (Preview) - Microsoft Sentinel | Microsoft Learn

Many organizations use threat intelligence platform (TIP) solutions to aggregate threat intelligence feeds from various sources. From the aggregated feed, the data is curated to apply to security solutions such as network devices, EDR/XDR solutions, or security information and event management (SIEM) solutions such as Microsoft Sentinel. The industry standard for describing cyberthreat information is called, "Structured Threat Information Expression" or STIX. By using the upload API which supports STIX objects, you use a more expressive way to import threat intelligence into Microsoft Sentinel.

The upload API ingests threat intelligence into Microsoft Sentinel without the need for a data connector. This article describes what you need to connect a TIP or custom solution to Microsoft Sentinel. For more information on the API details, see the reference document [Microsoft Sentinel upload API](stix-objects-api).

![Screenshot that shows the threat intelligence import path.](media/connect-threat-intelligence-upload-api/threat-intel-upload-api.png)

For more information about threat intelligence, see [Threat intelligence](understand-threat-intelligence).

Important

The Microsoft Sentinel threat intelligence upload API is in preview. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for more legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](overview#changes-for-new-customers-starting-july-2025).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).

Note

For information about feature availability in US Government clouds, see the Microsoft Sentinel tables in [Cloud feature availability for US Government customers](/en-us/azure/security/fundamentals/feature-availability).

## Prerequisites

- You must have read and write permissions to the Microsoft Sentinel workspace to store your threat intelligence STIX objects.
- You must be able to register a Microsoft Entra application.
- Your Microsoft Entra application must be granted the Microsoft Sentinel Contributor role at the workspace level.

## Steps to configure the upload API connection

Follow these steps to import STIX objects from your TIP or custom solution into Microsoft Sentinel:

1. Register a Microsoft Entra application, and then record its application ID.
2. Generate and record a client secret for your Microsoft Entra application.
3. Assign your Microsoft Entra application the Microsoft Sentinel Contributor role or the equivalent.
4. Configure your TIP solution or custom application.

## Register a Microsoft Entra application

The [default user role permissions](/en-us/azure/active-directory/fundamentals/users-default-permissions#restrict-member-users-default-permissions) allow users to create application registrations. If the application registration permission was switched to **No**, you need permission to manage applications in Microsoft Entra. Any of the following Microsoft Entra roles include the required permissions:

- Application administrator
- Application developer
- Cloud application administrator

For more information on registering your Microsoft Entra application, see [Register an application](/en-us/azure/active-directory/develop/quickstart-register-app#register-an-application).

After you register your application, record its application (client) ID from the application's **Overview** tab.

## Assign a role to the application

The upload API ingests threat intelligence objects at the workspace level and requires the role of Microsoft Sentinel Contributor.

1. From the Azure portal, go to **Log Analytics workspaces**.
2. Select **Access control (IAM)**.
3. Select **Add** &gt; **Add role assignment**.
4. On the **Role** tab, select the **Microsoft Sentinel Contributor** role, and then select **Next**.
5. On the **Members** tab, select **Assign access to** &gt; **User, group, or service principal**.
6. Select members. By default, Microsoft Entra applications aren't displayed in the available options. To find your application, search for it by name.

    ![Screenshot that shows the Microsoft Sentinel Contributor role assigned to the application at the workspace level.](media/connect-threat-intelligence-upload-api/assign-role.png)
7. Select **Review + assign**.

For more information on assigning roles to applications, see [Assign a role to the application](/en-us/azure/active-directory/develop/howto-create-service-principal-portal#assign-a-role-to-the-application).

## Configure your threat intelligence platform solution or custom application

The following configuration information is required by the upload API:

- Application (client) ID
- Microsoft Entra access token with [OAuth 2.0 authentication](/en-us/azure/active-directory/fundamentals/auth-oauth2)
- Microsoft Sentinel workspace ID

Enter these values in the configuration of your integrated TIP or custom solution where required.

1. Submit the threat intelligence to the upload API. For more information, see [Microsoft Sentinel upload API](stix-objects-api).
2. Within a few minutes, threat intelligence objects should begin flowing into your Microsoft Sentinel workspace. Find the new STIX objects on the **Threat intelligence** page, which is accessible from the Microsoft Sentinel menu.