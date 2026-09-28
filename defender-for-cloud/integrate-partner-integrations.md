---
layout: Conceptual
title: Connect Partner Integrations in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/integrate-partner-integrations
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
description: Connect third-party partner solutions to Microsoft Defender for Cloud to enhance detection, simplify deployment, and extend multicloud protection.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 2ba70ba4-d463-f7f2-a28e-9f560b366de2
document_version_independent_id: 9024474a-172b-fbc0-652a-e909cddf9b3e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/integrate-partner-integrations.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/integrate-partner-integrations
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/integrate-partner-integrations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 0e1e6056-0223-9eb6-f213-f7455aebedb3
---

# Connect Partner Integrations in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud works with Microsoft services and partner solutions. You can add partner solutions to improve your security posture. These solutions help protect your resources in multicloud setups.

Each integration offers different benefits. Some help simplify deployment. Others extend detection, monitoring, or management.

You can review the [available integrations](partner-integrations).

## Prerequisites

Before you begin, ensure you have the following:

- An Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Defender for Cloud enabled on your Azure subscription. [Enable Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.

## Create the partner application

Complete the following steps to create the app. Some partners might require extra setup on their side.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Microsoft Entra ID**.
3. Select **+ Add** &gt; **App registration** &gt; **New registration**.

    [![Screenshot that shows  how to navigate to the app registration button.](media/integrate-partner-integrations/app-registration.png)](media/integrate-partner-integrations/app-registration.png#lightbox)
4. Enter a name.
5. Select **Accounts in this organizational directory only (Microsoft only - Single tenant)**.
6. Select **Register**.

## Create a client secret

After you create the app, add a client secret.

1. Select the application you created.
2. Go to **Manage** &gt; **Certificates & secrets**.

    [![Screenshot that shows you where to navigate to get to the Certificates and Secrets screen.](media/integrate-partner-integrations/secrets.png)](media/integrate-partner-integrations/secrets.png#lightbox)
3. Select **Client secrets** &gt; **+ New client secret**.
4. Enter a name.
5. Select **Add**.

## Grant subscription permissions to the application

Next, give the app access to your subscription.

1. Search for and go to **Subscriptions**.
2. Select the relevant subscription.
3. Select **Access control (IAM)** &gt; **+ Add** &gt; **Add role assignment**.

    [![Screenshot that shows how to navigate to the add role assignment button.](media/integrate-partner-integrations/add-role-assignment.png)](media/integrate-partner-integrations/add-role-assignment.png#lightbox)
4. Select **Security Reader**.
5. Select **Next**.
6. Select **+ Select members**.
7. Search for and select the application you created.

    [![Screenshot that shows how to search for and select the demo application.](media/integrate-partner-integrations/demo-application.png)](media/integrate-partner-integrations/demo-application.png#lightbox)
8. Select **Select**.
9. Select **Review + assign**.
10. Follow the preceding steps again to add the **Reader** role.

Repeat the role-assignment steps to assign the **Security Reader** and **Reader** roles for any other relevant subscriptions.