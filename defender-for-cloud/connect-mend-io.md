---
layout: Conceptual
title: Connect Mend.io to Defender for Cloud (Preview) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/connect-mend-io
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
description: Learn how to connect Mend.io with Microsoft Defender for Cloud to enhance vulnerability analysis and gain visibility of critical vulnerabilities.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 989b79b8-00a7-22d0-053f-dc85df416b98
document_version_independent_id: e86e8351-73e1-1de8-f1e2-4b6e9c171adf
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/connect-mend-io.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/connect-mend-io
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/connect-mend-io.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: fddd228b-235d-6e81-20d9-c39f7ce93998
---

# Connect Mend.io to Defender for Cloud (Preview) - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud integrates with Mend.io to help identify and mitigate vulnerabilities in partner dependencies. The integration streamlines discovery and remediation.

This article explains the benefits and steps to connect Mend.io to Defender for Cloud. After setup, security teams get improved visibility and control over threats from code development to runtime.

## Prerequisites

- You need a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- You must [enable Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.
- You must [enable Defender Cloud Security Posture Management (CSPM)](tutorial-enable-cspm-plan) on your Azure subscription.
- Connect your DevOps environments to Defender for Cloud:

    - [Azure DevOps organizations](quickstart-onboard-devops)
    - [GitHub organizations](quickstart-onboard-github)
    - [GitLab groups](quickstart-onboard-devops)
- Have an account with the [Mend.io website](https://www.mend.io/).
- Obtain an activation key from Mend.io. For instructions, see [Mend.io integration activation token Application Programming Interface (API)](https://api-docs.mend.io/1.4/issue-tracker-api#getintegrationactivationtoken).
- You must have the appropriate role to:

    | Task | Role |
    | --- | --- |
    | Create DevOps connectors | Security Admin or Contributor assigned at the subscription level through Azure role-based-access control. |
    | Create the Mend.io connector | Security Administrator or Global Administrator assigned at the tenant level through Microsoft Entra. Permissions can be granted through [Privileged Identity Management](/en-us/entra/id-governance/privileged-identity-management/pim-configure). |
    | View reachability analysis findings | Security Admin or Security Reader assigned at the subscription level through Azure role-based-access control on the subscription that hosts the DevOps connector. |
- Connect only one Mend.io connector per tenant.
- Ensure repositories monitored by Mend.io are also connected to Defender for Cloud. Findings won't appear if those repositories aren't connected.

## Connect Mend.io to Defender for Cloud

To connect your Mend.io account to Defender for Cloud:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Integrations**.

    ![Microsoft Defender for Cloud Environment settings page with Integrations selected.](media/connect-mend-io/integrations.png)
4. Select **Add integration** &gt; **Mend.io**.

    [![Add integration menu showing Mend.io as a selectable integration.](media/connect-mend-io/add-mend-io.png)](media/connect-mend-io/add-mend-io.png#lightbox)

    Note

    The option to add the Mend.io integration isn't available if you don't have the appropriate permissions, or if you already have an existing connector to Mend.io.
5. Enter a Mend.io activation key.

    [![Mend.io integration form with the activation key field highlighted.](media/connect-mend-io/activation-key.png)](media/connect-mend-io/activation-key.png#lightbox)
6. Select **Create**.

After the integration is successfully created, a notice appears. Defender for Cloud scans repositories connected to Mend.io and populates results after six hours.