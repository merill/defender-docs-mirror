---
layout: Conceptual
title: Connect your GitHub organizations - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/quickstart-onboard-github
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
description: Learn how to connect your GitHub Environment to Defender for Cloud and enhance the security of your GitHub resources.
ms.date: 2025-05-13T00:00:00.0000000Z
ms.topic: quickstart
ms.custom: ignite-2023
ai-usage: ai-assisted
locale: en-us
document_id: 0ca5abf1-c15e-1f2c-6307-69b4e49b1811
document_version_independent_id: 4e5464a4-72db-1a1a-499c-230081c1e4f2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/quickstart-onboard-github.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/quickstart-onboard-github
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/quickstart-onboard-github.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 6a4a3951-cad3-3a21-bd03-ccac9b407163
---

# Connect your GitHub organizations - Microsoft Defender for Cloud | Microsoft Learn

In this quick start, you connect your GitHub organizations on the **Environment settings** page in Microsoft Defender for Cloud. This page provides a simple onboarding experience to autodiscover your GitHub repositories.

By connecting your GitHub environments to Defender for Cloud, you extend the security capabilities of Defender for Cloud to your GitHub resources and improve security posture. [Learn more](defender-for-devops-introduction).

## Prerequisites

To complete this quick start, you need:

- An Azure account with Defender for Cloud onboarded. If you don't already have an Azure account, [create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Availability

| Aspect | Details |
| --- | --- |
| Release state: | General Availability. |
| Pricing: | For pricing, see the Defender for Cloud [pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/?v=17.23h#pricing) You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator). |
| Required permissions: | **Account Administrator** with permissions to sign in to the Azure portal. **Contributor** to create the connector on the Azure subscription. **Organization Owner** in GitHub. |
| GitHub supported plans and user models | GitHub Free, Pro, Team, and Enterprise Cloud (with personal accounts and Enterprise Managed Users) |
| Regions and availability: | Refer to the [support and prerequisites](devops-support) section for region support and feature availability. |
| Clouds: | ![](media/quickstart-onboard-github/check-yes.png) Commercial ![](media/quickstart-onboard-github/x-no.png) National (Azure Government, Microsoft Azure operated by 21Vianet) |

Note

**Security Reader** role can be applied on the Resource Group/GitHub connector scope to avoid setting highly privileged permissions on a Subscription level for read access of DevOps security posture assessments.

## Connect your GitHub environment

To connect your GitHub environment to Microsoft Defender for Cloud:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Add environment**.
4. Select **GitHub**.

    [![Screenshot that shows selections for adding GitHub as a connector.](media/quickstart-onboard-github/select-github.png)](media/quickstart-onboard-github/select-github.png#lightbox)
5. Enter a name (limit of 20 characters), and then select your subscription, resource group, and region.

    The subscription is the location where Defender for Cloud creates and stores the GitHub connection.
6. Select **Next: Configure access**.
7. Select **Authorize** to grant your Azure subscription access to your GitHub repositories. Sign in, if necessary, with an account that has permissions to the repositories that you want to protect.

    After authorization, if you wait too long to install the DevOps security GitHub application, the session will time out and you'll get an error message.
8. Select **Install**.
9. Select the organizations to install the Defender for Cloud GitHub application. It's recommended to grant access to **all repositories** to ensure Defender for Cloud can secure your entire GitHub environment.

    This step grants Defender for Cloud access to organizations that you wish to onboard.
10. All organizations with the Defender for Cloud GitHub application installed will be onboarded to Defender for Cloud. To change the behavior going forward, select one of the following:

    - Select **all existing organizations** to automatically discover all repositories in GitHub organizations where the DevOps security GitHub application is installed.
    - Select **all existing and future organizations** to automatically discover all repositories in GitHub organizations where the DevOps security GitHub application is installed and future organizations where the DevOps security GitHub application is installed.

        Note

        Organizations can be removed from your connector after the connector creation is complete. See the [editing your DevOps connector](edit-devops-connector) page for more information.
11. Select **Next: Review and generate**.
12. Select **Create**.

When the process finishes, the GitHub connector appears on your **Environment settings** page.

[![Screenshot that shows the environment settings page with the GitHub connector now connected.](media/quickstart-onboard-github/github-connector.png)](media/quickstart-onboard-github/github-connector.png#lightbox)

The Defender for Cloud service automatically discovers the organizations where you installed the DevOps security GitHub application.

Note

To ensure proper functionality of advanced DevOps posture capabilities in Defender for Cloud, only one instance of a GitHub organization can be onboarded to the Azure Tenant you are creating a connector in.

Upon successful onboarding, DevOps resources (e.g., repositories, builds) will be present within the Inventory and DevOps security pages. It might take up to 8 hours for resources to appear. Security scanning recommendations might require [an additional step to configure your workflows](github-action). Refresh intervals for security findings vary by recommendation and details can be found on the Recommendations page.