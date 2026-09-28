---
layout: Conceptual
title: How to onboard to the Microsoft Sentinel data lake | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/isv/sentinel-data-lake-onboarding
breadcrumb_path: ../breadcrumb/toc.json
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
ms.subservice: sentinel-platform
search.appverid: met150
description: Onboard your tenant to the Microsoft Sentinel data lake from the Microsoft Defender portal so you can ingest and analyze security data.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: smarapareddy
ms.date: 2026-06-22T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1012
locale: en-us
document_id: ab60da92-af03-8978-a791-aefd130b03f7
document_version_independent_id: c521f07a-c79f-0e59-3ef8-9ca46136f320
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/isv/sentinel-data-lake-onboarding.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/isv/sentinel-data-lake-onboarding
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/isv/sentinel-data-lake-onboarding.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 26a90950-93db-9165-1236-b215a233308e
---

# How to onboard to the Microsoft Sentinel data lake | Microsoft Learn

Before developing platform solutions you need to onboard your tenant to the Microsoft Sentinel data lake. Onboard your tenant to the Microsoft Sentinel data lake from the Microsoft Defender portal. Onboarding is a one-time process that takes about 60 minutes and connects a Log Analytics workspace and sets up the data lake for your tenant. After you onboard, you can ingest security telemetry into the data lake and query it in later articles in this series.

## Prerequisites

- Access to the [Microsoft Defender portal](https://security.microsoft.com).
- Decide on data lake region. The data lake is onboarded in the same region as your primary Sentinel workspace. Check your workspace's region before you start and ensure that the region is suitable for the data lake. For more information, see [Supported regions](/en-us/azure/sentinel/geographical-availability-data-residency#supported-regions). 
    Note

    When you onboard to data lake, only Workspaces that are in the same region as your primary Sentinel workspace are attached to the data lake. Once you have onboarded, the region can’t be changed through the Defender portal.

| Operation | Required role |
| --- | --- |
| Onboarding to the Sentinel data lake | Microsoft Entra ID - Security Administrator or Global Administrator |
| Onboard Sentinel workspace to Defender portal | Subscription Owner, or User Access Administrator at subscription scope and Microsoft Sentinel Contributor at subscription or resource group scope |
| Onboard Sentinel workspace to Data Lake | Subscription Owner or Microsoft Sentinel Contributor at subscription or resource group scope |

Note

These elevated roles are needed only for the one-time onboarding. To follow least-privilege practices, elevate to them just in time with [Microsoft Entra Privileged Identity Management (PIM)](/en-us/entra/id-governance/privileged-identity-management/pim-configure), and use **Security Administrator** instead of **Global Administrator** where possible.

## Create a Log Analytics workspace

Before you onboard to the data lake, you need to create or identify a Log Analytics workspace to which Microsoft sentinel can be added. If you already have a workspace in a data lake supported region, you can skip workspace creation and move to the next step.

1. If you don’t have a workspace, follow the steps in [Create a Log Analytics workspace](/en-us/azure/sentinel/quickstart-onboard?tabs=defender-portal#create-a-log-analytics-workspace) to create a workspace. Select the region of your Log Analytics workspace from the [supported regions](/en-us/azure/sentinel/geographical-availability-data-residency#supported-regions) for the data lake, such as East US 2.
2. Add Sentinel to the Log Analytics Workspace by following the steps in [Add Microsoft Sentinel to your Log Analytics workspace](/en-us/azure/sentinel/quickstart-onboard?tabs=defender-portal#add-microsoft-sentinel-to-your-log-analytics-workspace).

## Connect the workspace to the Defender portal and set it as primary

To connect your Sentinel workspace and set it as primary, complete the following steps:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Under **System** &gt; **Settings** &gt; **Microsoft Sentinel** select **SIEM workspaces**
3. Select your Sentinel workspace and select **Connect workspace**.
4. Set the workspace as **Primary**.

Note

If your Sentinel workspace doesn't appear in the Defender portal, or the **Subscription** filter is blank or shows **Undefined**, you likely have a missing role. Recheck the prerequisites before retrying.

[![Screenshot of the SIEM workspaces page with a workspace selected and the Connect workspace button highlighted.](media/sentinel-data-lake-onboarding/connect-workspace.png)](media/sentinel-data-lake-onboarding/connect-workspace.png#lightbox)

## Start onboarding from the Defender portal

After your workspace is connected, start the onboarding process in the Defender portal.

1. In the [Microsoft Defender portal](https://security.microsoft.com), under **System** &gt; **Settings** select **Microsoft Sentinel** then select **Data lake**
2. Select **Start setup**. If a side panel indicates missing permissions, verify that you have the roles listed in Prerequisites.

    [![Screenshot of the Data lake page in the Defender portal with the Start setup button highlighted.](media/sentinel-data-lake-onboarding/start-setup.png)](media/sentinel-data-lake-onboarding/start-setup.png#lightbox)

## Select a subscription and resource group

Choose where to enable billing for the data lake.

1. In the setup side panel, select your target **Subscription**.
2. Select the target **Resource group** to enable billing for the Sentinel data lake.
3. Select **Set up data lake**.

    [![Screenshot of the Set up Sentinel data lake panel showing the Subscription and Resource group fields and the Setup data lake button.](media/sentinel-data-lake-onboarding/set-up-data-lake.png)](media/sentinel-data-lake-onboarding/set-up-data-lake.png#lightbox)

Caution

Don't delete the billing subscription or resource group selected during onboarding. Deleting either breaks the data lake setup, and the Defender portal shows **Something went wrong, please try again**.

If you delete the billing subscription or resource group after onboarding, you'll no longer have access to data lake functions or experiences. If you deleted the billing subscription or resource group, contact Microsoft support for assistance.

## Monitor onboarding progress

After you start the setup, a progress panel appears.

1. Wait for the onboarding process to finish. Onboarding might take up to 60 minutes to complete.
2. You can close the setup panel. The process continues in the background, and a **Setup in progress** banner appears on the Defender portal home page.

### Validate onboarding

After the setup completes, confirm the data lake is ready:

1. In the Defender portal &gt; **SIEM workspaces**, confirm your Sentinel workspace appears as **Connected** and **Primary**.
2. Confirm the **Data lake** settings page loads without errors and shows your configured subscription and resource group.
3. Under **Microsoft Sentinel** in the left navigation bar, confirm the **Data lake** exploration options are available.

For more information, see [Onboard to Microsoft Sentinel data lake from the Defender portal](../datalake/sentinel-lake-onboarding).

## Verify the onboarding

Confirm that your data lake is ready to use.

1. When onboarding finishes, a new banner appears with cards that describe how to use your data lake.
2. Confirm that **Data lake exploration** is available under **Microsoft Sentinel**.

    [![Screenshot of the Microsoft Sentinel menu with the Data lake exploration section highlighted in the Defender portal.](media/sentinel-data-lake-onboarding/data-lake-exploration.png)](media/sentinel-data-lake-onboarding/data-lake-exploration.png#lightbox)