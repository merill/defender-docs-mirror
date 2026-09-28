---
layout: Conceptual
title: Edit DevOps Connectors - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/edit-devops-connector
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
description: Update authorization, organization scope, and connector settings for Azure DevOps, GitHub, and GitLab environments onboarded to Defender for Cloud.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: ignite-2023, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 4ab01613-8a9f-ac52-0515-fdc0ba50afc8
document_version_independent_id: c688b13d-c638-76a9-6f04-69d819e2747c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/edit-devops-connector.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/edit-devops-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/edit-devops-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://authoring-docs-microsoft.poolparty.biz/devrel/5bd2b3fa-c186-4b92-a3c8-09f22a249d37
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/7eba7926-b7b2-4a7a-bf89-e6ac53b3e7f6
platformId: fe9f2551-cefe-fc03-c043-fe2d1dea0940
---

# Edit DevOps Connectors - Microsoft Defender for Cloud | Microsoft Learn

After onboarding your Azure DevOps, GitHub, or GitLab environments to Microsoft Defender for Cloud, you might need to change the authorization token for a connector. You might also need to add or remove onboarded organizations or groups, or install the GitHub application to another scope. This article shows how to update those connector settings.

## Prerequisites

Before you edit a DevOps connector, make sure you have the following:

- An Azure account with Defender for Cloud onboarded. If you don't already have an Azure account, [create an Azure account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An onboarded DevOps environment. For onboarding guidance, see [Onboard Azure DevOps](quickstart-onboard-devops), [Onboard GitHub](quickstart-onboard-github), or [Onboard GitLab](quickstart-onboard-gitlab).

## Make edits to your DevOps connector

To edit a DevOps connector in Defender for Cloud:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Find the connector you want to change.
4. Select **Edit settings** for the connector.

    [![Screenshot of the connector page that shows where to select Edit settings.](media/edit-devops-connector/edit-connector-1.png)](media/edit-devops-connector/edit-connector-1.png#lightbox)
5. Go to **Configure access**. Here you can exchange tokens, change onboarded organizations or groups, or toggle autodiscovery.

    Note

    If you're the owner of the connector, reauthorizing your environment to make changes is **optional**. If you're trying to take ownership of the connector, you must reauthorize by using your access token. This change is irreversible as soon as you select **Reauthorize**.
6. Use **Edit connector account** to update onboarded inventory. If an organization or group is grayed out, verify that you have permissions to that environment and that the scope isn't onboarded elsewhere in the tenant.

    [![Screenshot of the Edit connector account page that shows account selection options.](media/edit-devops-connector/edit-connector-2.png)](media/edit-devops-connector/edit-connector-2.png#lightbox)
7. To save inventory changes, select **Next: Review and generate &gt;** and then select **Update**. If you skip **Update**, Defender for Cloud doesn't save your inventory changes.