---
layout: Conceptual
title: Connect a Partner Integration to Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/connect-an-integration
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
description: Learn how to connect partner integrations into Microsoft Defender for Cloud to enhance security and gain insights for your multicloud environment.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 4ac1bcd7-9439-f0d0-0348-4f6ac0b7f64a
document_version_independent_id: c2498525-34d8-7d6b-d80b-86b044882a06
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/connect-an-integration.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/connect-an-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/connect-an-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 13dac874-d775-c548-05eb-876d71ba6cb5
---

# Connect a Partner Integration to Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud connects with partner integrations. Your selected integration lets Defender for Cloud receive or share information that helps secure your multicloud environment.

For the full list of available integrations, see [Overview of partner integrations](partner-integrations).

## Prerequisites

Before you connect a partner integration, make sure you meet the following prerequisites:

- An Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Defender for Cloud enabled on your Azure subscription. [Enable Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.
- Connect your [non-Azure machines](quickstart-onboard-machines), [Amazon Web Service accounts](quickstart-onboard-aws), or [Google Cloud Platform](quickstart-onboard-gcp).
- Have a subscription or an account with your partner integration.

## Connect a partner integration in Defender for Cloud

To connect a partner integration:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Integrations**.

    [![Microsoft Defender for Cloud Environment settings page with the Integrations tab selected.](media/connect-an-integration/integrations.png)](media/connect-an-integration/integrations.png#lightbox)
4. Select **+ Add integration**.

    [![Integrations page showing the + Add integration button above the connector list.](media/connect-an-integration/add-integration.png)](media/connect-an-integration/add-integration.png#lightbox)
5. Select the partner integration that you want to connect.
6. Enter the required information for the integration.
7. Select **Save**.

The integration now appears in the list of connected integrations.