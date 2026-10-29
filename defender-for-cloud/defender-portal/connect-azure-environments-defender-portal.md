---
layout: Conceptual
title: Connect Azure environments in the Defender portal - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-portal/connect-azure-environments-defender-portal
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
description: Connect Azure subscriptions and management groups to Microsoft Defender for Cloud in the Microsoft Defender portal.
ms.topic: how-to
ms.date: 2026-07-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d4e5c7b8-90a1-0371-765c-7a6d54084dc2
document_version_independent_id: 7f064a24-1e44-bf83-f66e-f10ccd581415
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-portal/connect-azure-environments-defender-portal.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: ../toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-portal/connect-azure-environments-defender-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-portal/connect-azure-environments-defender-portal.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 85e9e219-7658-c2e7-6219-7f6e125faf85
---

# Connect Azure environments in the Defender portal - Microsoft Defender for Cloud | Microsoft Learn

Important

This feature is in preview. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Connect Azure subscriptions and management groups to manage cloud security plans in the Microsoft Defender portal. The connector establishes the cloud security access and permissions required for the selected Azure environment.

Connecting an environment doesn't change its existing plans or billing. If cloud security plans are already enabled, they appear in the Defender portal, and the connector permissions replace the environment's existing cloud security access model. If no plans are enabled, enable them separately after the connector is active.

## Prerequisites

Before you begin, make sure you have:

- An Azure commercial environment.

    Note

    Azure national or sovereign clouds aren't currently supported.
- The **Global Administrator** or **Security Administrator** role in Microsoft Entra ID. Alternatively, you need the **Core security settings (Manage)** permission in [Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/custom-permissions-details#authorization-and-settings).
- The **Owner** or **User Access Administrator** role on the Azure subscription or management group that you want to connect.

    Note

    You might need to [elevate access to manage Azure subscriptions and management groups](/en-us/azure/role-based-access-control/elevate-access-global-admin?tabs=azure-portal%2Centra-audit-logs).

## Prepare your tenant

The first time you access **Cloud security** in the Defender portal, Defender prepares your tenant by collecting information about your Azure subscriptions, including their current coverage and enabled plans.

Tenant preparation can take up to an hour. You can begin connecting environments while preparation continues.

## Connect an Azure environment

To connect an Azure environment:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to **Cloud security** &gt; **Overview**.
3. Under **Manage cloud security**, select **Connect environments**.
4. Select **Connector page**.
5. Under **Microsoft Azure**, select **Connect**.
6. Optionally, enter a display name for the connector.
7. Select whether you want to connect a **Management Group** or **Subscription**.
8. Enter the management group ID or subscription ID, depending on the environment type you selected.

    If you don't enter a display name, this ID is used instead.
9. Select **Next**.
10. Select the capabilities that you want to enable for the environment:

    - **Discovery** identifies resources and builds the cloud inventory.
    - **Agent deployment** deploys and manages agents in the environment.
    - **AI access** reads supported AI prompts and resources to provide AI security insights.
    - **Agentless scanners** scan supported resources without installing an agent.

    Tip

    Microsoft recommends enabling all available capabilities to maintain full security coverage and avoid protection gaps.
11. Select **Next**.
12. Select a deployment method: **Auto-deploy** or **Manual deployment**.
13. **Auto-deploy only:** Select **Run auto-deploy**. The deployment and validation run automatically.
14. **Manual deployment only:**

    1. Select **Copy script**.
    2. Open Azure Cloud Shell and select **Bash**.
    3. Paste and run the script in Cloud Shell.
    4. After the script finishes successfully, copy the **Security Operator ID** returned by the script.
    5. Paste the value into **Security Operator ID**.
    6. Select **Validate**.
15. Select **Next**.
16. Review the connector details, then select **Activate connector**.
17. After the connector is successfully activated, select **Done**.

After a successful connection, the Azure environment appears in the Microsoft Defender portal with any existing enabled plans. If no plans are enabled, [configure cloud security plans](manage-plans-defender-portal) separately.

## Edit an existing connector

You can update the capabilities and permissions assigned to an existing connector.

To edit an existing connector:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to **Cloud security** &gt; **Overview**.
3. Under **Manage cloud security**, select **Connect environments**.
4. Select **Connector page**.
5. Select **My connectors**.
6. Select the Azure connector you want to update.
7. Select **Edit connector**.
8. Update the connector settings.

    Note

    If you change the connector capabilities or permissions, redeploy and validate the connector before continuing.
9. Select **Next**.
10. Review the connector details, then select **Activate connector**.
11. After the connector is successfully activated, select **Done**.