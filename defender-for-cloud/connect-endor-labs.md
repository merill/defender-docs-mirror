---
layout: Conceptual
title: Connect Endor Labs to Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/connect-endor-labs
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
description: Learn how to connect Endor Labs with Microsoft Defender for Cloud to enhance vulnerability analysis and gain visibility of critical vulnerabilities.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
locale: en-us
document_id: fdf3833b-73c5-c2de-b6bc-c8bc9c7de193
document_version_independent_id: 536d7d35-7f1b-c44c-5d41-b20cb1eb828c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/connect-endor-labs.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/connect-endor-labs
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/connect-endor-labs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: aafac40b-6053-a5ac-b337-e7ab2643ec2e
---

# Connect Endor Labs to Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud integrates with Endor Labs to help identify and mitigate vulnerabilities in partner dependencies. This integration helps streamline discovery and remediation.

This article explains the benefits and steps to connect Endor Labs to Defender for Cloud. After setup, security teams get better visibility and control over threats from code to runtime.

## Prerequisites

- A Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for an Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Microsoft Defender for Cloud on your Azure subscription](get-started#enable-defender-for-cloud-on-your-azure-subscription) enabled.
- [Defender Cloud Security Posture Management (CSPM)](tutorial-enable-cspm-plan) enabled on your Azure subscription.
- Connect your DevOps environments to Defender for Cloud:

    - [Connect Azure DevOps organizations to Defender for Cloud](quickstart-onboard-devops)
    - [Connect GitHub organizations to Defender for Cloud](quickstart-onboard-github)
    - [Connect GitLab groups to Defender for Cloud](quickstart-onboard-devops)
- An Endor Labs account. For more information, see the [Endor Labs product site](https://www.endorlabs.com/).
- An Endor Labs Application Programming Interface (API) key with read-only permissions. For setup instructions, see [Creating API keys in Endor Labs](https://docs.endorlabs.com/administration/api-keys/). We recommend an expiration date of 180 days.
- The appropriate roles for the following tasks:

    - **Create DevOps connectors**: Security Admin or Contributor assigned at the **subscription level** through Azure role-based-access control (RBAC).
    - **Create the Endor Labs connector**: Security Administrator (or higher) assigned at the **tenant level** through Microsoft Entra. Permissions can be granted through Privileged Identity Management (PIM). For details, see [Configure PIM](/en-us/entra/id-governance/privileged-identity-management/pim-configure).
    - **View reachability analysis findings**: Security Admin or Security Reader assigned at the **subscription level** through Azure role-based-access control (RBAC) on the subscription that hosts the DevOps connector.
- You can only have one connector to Endor Labs per tenant.
- Findings from Endor Labs are only shown if the corresponding repository is also connected to Defender for Cloud.

## Connect Endor Labs to Defender for Cloud

To connect your Endor Labs account to Defender for Cloud:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Integrations**.

    [![Microsoft Defender for Cloud Environment settings page with Integrations selected.](media/connect-endor-labs/integrations.png)](media/connect-endor-labs/integrations.png#lightbox)
4. Select **Add integration** &gt; **Endor Labs**.

    [![Add integration menu showing Endor Labs as a selectable integration.](media/connect-endor-labs/add-endor-labs.png)](media/connect-endor-labs/add-endor-labs.png#lightbox)

    Note

    The option to add the Endor Labs integration isn't available if you don't have the appropriate permissions, or if you already have an existing connector to Endor Labs.
5. Enter the Endor Labs **Namespace**, **API key ID**, and **API secret**.

    ![Endor Labs integration form with Namespace, API key ID, and API secret fields.](media/connect-endor-labs/enter-information.png)
6. Select **Create**.

A notice appears after the integration is successfully created. Defender for Cloud scans repositories that are connected to Endor Labs and populates security findings with results after six hours.