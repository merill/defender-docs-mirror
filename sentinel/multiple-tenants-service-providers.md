---
layout: Conceptual
title: Manage multiple tenants in Microsoft Sentinel as a Managed Security Service Provider | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/multiple-tenants-service-providers
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
description: How to onboard and manage multiple tenants in Microsoft Sentinel as a Managed Security Service Provider (MSSP) using Azure Lighthouse.
ms.author: guywild
author: guywi-ms
ms.reviewer: yobasha
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: b18d7b05-515b-8b9a-f1e0-bf4e0a7dc6c1
document_version_independent_id: b5764fa3-a81c-2ccc-b564-183ce3a68354
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/multiple-tenants-service-providers.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/multiple-tenants-service-providers
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/multiple-tenants-service-providers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 1e02b584-ce71-dcb6-88c3-48cb3c36b1bd
---

# Manage multiple tenants in Microsoft Sentinel as a Managed Security Service Provider | Microsoft Learn

If you're a managed security service provider (MSSP) and you're using [Azure Lighthouse](/en-us/azure/lighthouse/overview) to offer security operations center (SOC) services to your customers, you can manage your customers' Microsoft Sentinel resources directly from your own Azure tenant, without having to connect to the customer's tenant.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your move to the Defender portal to ensure a smooth experience and to take full advantage of unified security operations and multitenant management capabilities offered by the Defender portal. For guidance and best practices, see the [Microsoft Defender portal implementation guide for MSSPs](/en-us/defender-xdr/playbook-managed-security).

## Prerequisites

Before you manage multiple tenants in Microsoft Sentinel, complete the following prerequisite:

- [Onboard Azure Lighthouse](/en-us/azure/lighthouse/how-to/onboard-customer)

## Verify registration of Microsoft Sentinel resource providers

Your MSSP tenant must have the Microsoft Sentinel resource providers registered on at least one subscription. Each of your customers' tenants must also have those resource providers registered.

If you already registered Microsoft Sentinel in your tenant, and your customers did the same in theirs, you can skip ahead to Access Microsoft Sentinel in managed tenants.

**To verify registration**:

1. Select **Subscriptions** from the Azure portal, and then select a relevant subscription from the menu.
2. From the navigation menu on the subscription screen, under **Settings**, select **Resource providers**.
3. From the ***subscription name* | Resource providers** screen, search for *Microsoft.OperationalInsights* and *Microsoft.SecurityInsights*. Select each one and check the **Status** column. If the status is *NotRegistered*, select **Register**.

    ![Screenshot of checking resource providers.](media/multiple-tenants-service-providers/check-resource-provider.png)

## Access Microsoft Sentinel in managed tenants

To access your customers' Microsoft Sentinel workspaces from your own tenant, perform the following steps:

1. Under **Directory + subscription**, select the delegated directories (each directory maps to a tenant). Also select the subscriptions that contain your customer's Microsoft Sentinel workspaces.

    ![Choose tenants and subscriptions](media/multiple-tenants-service-providers/directory-subscription.png)
2. Open Microsoft Sentinel, where you'll see all the workspaces in the selected subscriptions and can work with them seamlessly, just like any workspace in your own tenant.

Note

You can't deploy connectors in Microsoft Sentinel from a managed workspace that uses only Azure Lighthouse. You must also configure GDAP. For more details, see [Microsoft Defender portal implementation guide for MSSPs](/en-us/defender-xdr/playbook-managed-security).