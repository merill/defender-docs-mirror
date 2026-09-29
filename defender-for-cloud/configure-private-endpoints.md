---
layout: Conceptual
title: Configure Private Endpoints with Microsoft Security Private Link - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/configure-private-endpoints
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
description: Configure private endpoints with Microsoft Security Private Link to securely connect your virtual network to Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: f42cb630-4dea-7175-54d1-e6ea54371515
document_version_independent_id: 7d695517-bf96-e049-5a26-91a050981142
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/configure-private-endpoints.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/configure-private-endpoints
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/configure-private-endpoints.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/16cd61cd-9ecf-429b-b494-91576c41f8e4
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/c4bdb33a-5524-4b66-b162-03f5621d7902
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 391bf2a8-0f49-7272-ff00-5ecfccb01830
---

# Configure Private Endpoints with Microsoft Security Private Link - Microsoft Defender for Cloud | Microsoft Learn

Use a [private endpoint in Azure Private Link](/en-us/azure/private-link/private-endpoint-overview) with Microsoft Security Private Link. This private endpoint configuration connects workloads in your private network to Microsoft Defender for Cloud over [Azure Private Link](/en-us/azure/private-link/private-link-overview).

Note

Microsoft Security Private Link isn't supported in sovereign cloud regions, such as Azure Government and Azure operated by 21Vianet.

## Prerequisites

Before you begin, make sure that:

- An Azure subscription with Defender for Cloud enabled. If you don't have an Azure subscription, create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A virtual network and subnet where your workloads are deployed. If you need to create these networking resources first, see [Create a virtual network and subnet](/en-us/azure/virtual-network/quick-create-portal). You create the private endpoint in this subnet.
- You reviewed the required [Security Private Link roles and permissions](concept-private-links#roles-and-permissions).

## Create a private endpoint using a Security Private Link resource (Azure portal)

You can create a private endpoint while creating a Security Private Link resource in the Azure portal.

If you already have a Security Private Link resource, skip this procedure. Go to Create a private endpoint for an existing Security Private Link resource later in this article. That section shows you how to create a private endpoint separately and connect it to your existing resource.

To create a private endpoint while creating a Security Private Link resource:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Select **Create a resource**.
3. Search for **Security Private Link**.
4. Under **Security Private Link** select **Create**.

    [![Screenshot of the Azure Marketplace showing the Security Private Link tile with the Create button.](media/configure-private-endpoints/marketplace-create-security-private-link.png)](media/configure-private-endpoints/marketplace-create-security-private-link.png#lightbox)
5. Select a subscription and an existing resource group, or create a new one.
6. If needed, select a resource group location.
7. Enter a name.
8. Select **Next: Networking**.

    Note

    Microsoft Security Private Link currently supports the **containers** sub-resource, which the Microsoft Defender for Containers plan uses.
9. Select **Create a private endpoint**.
10. Enter a name and a location.

    [![Screenshot of the Create Security Private Link wizard on the Networking tab, showing the Create a private endpoint pane with sub-resource and Private DNS integration.](media/configure-private-endpoints/create-private-endpoint-blade-networking-tab.png)](media/configure-private-endpoints/create-private-endpoint-blade-networking-tab.png#lightbox)
11. Select **containers** as the target sub-resource.
12. Select the virtual network and subnet.
13. Enable **Private DNS integration** to create a private DNS zone automatically.
14. Select **Add**.
15. Select **Next: Tags** and add any required tags.
16. Select **Review + create**.
17. Select **Create**.

## Create a private endpoint for an existing Security Private Link resource (Azure portal)

If you already have a Security Private Link resource, you can create a private endpoint separately and connect it to that resource.

To create a private endpoint for an existing Security Private Link resource:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Network foundation** &gt; **Private Link** &gt; **Private endpoints**.
3. Select **Create**.

    [![Screenshot of the Network foundation Private endpoints page, showing the Create button.](media/configure-private-endpoints/network-foundation-create-private-endpoint.png)](media/configure-private-endpoints/network-foundation-create-private-endpoint.png#lightbox)
4. Select a subscription and an existing resource group, or create a new one.
5. Enter a name and network interface name.
6. Select a region.
7. Select **Next: Resource**.

    Note

    Microsoft Security Private Link currently supports the **containers** sub-resource, which the Microsoft Defender for Containers plan uses.
8. Select **Connect to an Azure resource in my directory**.
9. Select a subscription.
10. Select **Microsoft.Security/privateLinks** as the resource type.
11. Select the Security Private Link resource for Defender for Cloud.
12. Select **containers** as the target sub-resource.
13. Select **Next: Virtual Network**.
14. Select the virtual network and the subnet.
15. Leave the private IP address allocation set to **Dynamic**.
16. Select **Next: DNS**.
17. Enable **Integrate with private DNS zone** and verify that the private DNS zone is populated automatically.
18. Select **Next: Tags**.
19. Add any required tags.
20. Select **Review + create**.
21. Select **Create**.

## Approve the private endpoint connection

When you create the private endpoint, you send a connection request to the Security Private Link resource.

- If you're an **Owner**, the connection is approved automatically.
- Otherwise, an **Owner** must approve the request from **Private endpoint connections** in the Azure portal.

## Validate the private endpoint connection

To validate private endpoint DNS resolution:

From a workload connected to the virtual network, run the following command to verify that the Microsoft Defender for Cloud API hostname resolves to a private IP address through DNS:

```bash
nslookup api.cloud.defender.microsoft.com
```

The FQDN should resolve to a private IP address under `privatelink.cloud.defender.microsoft.com`.