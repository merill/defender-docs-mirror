---
layout: Conceptual
title: Connect your GitLab groups - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/quickstart-onboard-gitlab
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
description: Learn how to connect your GitLab Environment to Defender for Cloud.
ms.date: 2025-05-13T00:00:00.0000000Z
ms.topic: quickstart
ms.custom: ignite-2023
ai-usage: ai-assisted
locale: en-us
document_id: acbeb7ae-036e-8fb2-49f6-9534837dbf2b
document_version_independent_id: 8c754cd4-3b87-794f-ec61-92e6e1d0a2cd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/quickstart-onboard-gitlab.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/quickstart-onboard-gitlab
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/quickstart-onboard-gitlab.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 8e8cb38d-bbd0-d864-188f-4545ef570442
---

# Connect your GitLab groups - Microsoft Defender for Cloud | Microsoft Learn

In this quickstart, you connect your GitLab groups on the **Environment settings** page in Microsoft Defender for Cloud. This page provides a simple onboarding experience to automatically discover your GitLab resources.

By connecting your GitLab groups to Defender for Cloud, you extend the security capabilities of Defender for Cloud to your GitLab resources. These features include:

- **Foundational Cloud Security Posture Management (CSPM) features**: You can assess your GitLab security posture through GitLab-specific security recommendations. You can also learn about all the [recommendations for DevOps](recommendations-reference) resources.
- **Defender CSPM features**: Defender CSPM customers receive code to cloud contextualized attack paths, risk assessments, and insights to identify the most critical weaknesses that attackers can use to breach their environment. Connecting your GitLab projects allows you to contextualize DevOps security findings with your cloud workloads and identify the origin and developer for timely remediation. For more information, learn how to [identify and analyze risks across your environment](concept-attack-path).

## Prerequisites

To complete this quickstart, you need:

- An Azure account with Defender for Cloud onboarded. If you don't already have an Azure account, [create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- GitLab Ultimate license for your GitLab Group.

## Availability

| Aspect | Details |
| --- | --- |
| Release state: | General availability. |
| Pricing: | For pricing, see the Defender for Cloud [pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/?v=17.23h#pricing). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator). |
| Required permissions: | **Account Administrator** with permissions to sign in to the Azure portal. **Contributor** to create a connector on the Azure subscription. **Group Owner** on the GitLab Group. |
| Regions and availability: | Refer to the [support and prerequisites](devops-support) section for region support and feature availability. |
| Clouds: | ![](media/quickstart-onboard-github/check-yes.png) Commercial ![](media/quickstart-onboard-github/x-no.png) National (Azure Government, Microsoft Azure operated by 21Vianet) |

Note

**Security Reader** role can be applied on the Resource Group/GitLab connector scope to avoid setting highly privileged permissions on a Subscription level for read access of DevOps security posture assessments.

## Connect your GitLab Group

To connect your GitLab Group to Defender for Cloud by using a native connector:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Add environment**.
4. Select **GitLab**.

    [![Screenshot that shows selections for adding GitLab as a connector.](media/quickstart-onboard-gitlab/gitlab-connector.png)](media/quickstart-onboard-gitlab/gitlab-connector.png#lightbox)
5. Enter a name, subscription, resource group, and region.

    The subscription is the location where Microsoft Defender for Cloud creates and stores the GitLab connection.
6. Select **Next: Configure access**.
7. Select **Authorize**.
8. In the popup dialog, read the list of permission requests, and then select **Accept**.
9. For Groups, select one of the following:

    - Select **all existing groups** to autodiscover all subgroups and projects in groups you're currently an Owner in.
    - Select **all existing and future groups** to autodiscover all subgroups and projects in all current and future groups you're an Owner in.

Since GitLab projects are onboarded at no additional cost, autodiscovery is applied across the group to ensure Defender for Cloud can comprehensively assess the security posture and respond to security threats across your entire DevOps ecosystem. Groups can later be manually added and removed through **Microsoft Defender for Cloud** &gt; **Environment settings**.

1. Select **Next: Review and generate**.
2. Review the information, and then select **Create**.

Note

To ensure proper functionality of advanced DevOps posture capabilities in Defender for Cloud, only one instance of a GitLab group can be onboarded to the Azure Tenant you are creating a connector in.

The **DevOps security** pane shows your onboarded repositories by GitLab group. The **Recommendations** pane shows all security assessments related to GitLab projects.