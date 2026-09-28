---
layout: Conceptual
title: Create an ISOC workspace in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/onboard-isoc-workspace
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to create an ISOC workspace in the Microsoft Defender portal for Integrated Security Operations Center (ISOC) capabilities that require a workspace.
author: mberdugo
ms.author: monaberdugo
ms.localizationpriority: high
ms.collection:
- m365-security
- m365solution-getstarted
- highpri
- tier1
- usx-security
- zerotrust-solution
- msftsolution-secops
ms.topic: how-to
ms.service: microsoft-sentinel
ai-usage: ai-assisted
ms.date: 2026-09-14T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: d4cd8f9f-a172-c40e-e447-98402fd7e6eb
document_version_independent_id: d4cd8f9f-a172-c40e-e447-98402fd7e6eb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/onboard-isoc-workspace.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: onboard-isoc-workspace
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/onboard-isoc-workspace.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 3c927217-7087-4c29-9f05-9e3aa5f2b7b7
---

# Create an ISOC workspace in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn

Use this procedure to create an Integrated Security Operations Center (ISOC) workspace in the Microsoft Defender portal for capabilities that require a workspace.

Before you begin, review the eligibility and workspace requirements in [ISOC in Microsoft Defender](isoc-overview).

## Prerequisites

Before you begin, make sure the following requirements are met:

- Your tenant is [eligible for ISOC](isoc-overview).
- You have an active Azure subscription.
- You have the **Security Administrator** role in Microsoft Entra ID.
- You have one of the following permission configurations on the Azure subscription:
    - Unconditional **Owner**.
    - **User Access Administrator** and **Microsoft Sentinel Contributor**.

## Create an ISOC workspace

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Go to **Setup & configuration** &gt; **Settings** &gt; **Microsoft Sentinel** &gt; **SIEM workspaces**.
3. Select **+ Create workspace**.
4. In **Subscription**, select the Azure subscription where you want to create the workspace.

    [![Screenshot of the Connect Microsoft Sentinel to Defender dialog in the Microsoft Defender portal, where you select an Azure subscription to create and connect an ISOC workspace.](media/onboard-isoc-workspace/connect-microsoft-sentinel-to-defender.png)](media/onboard-isoc-workspace/connect-microsoft-sentinel-to-defender.png#lightbox)

    The portal checks whether you have the required permissions on the selected subscription.
5. After the permissions check succeeds, review the workspace details.

    The setup provides values for the resource group, workspace, and region.
6. To change the workspace configuration, select the edit icon next to **Workspace details**.
7. Update the resource group, workspace name, region, or tags as needed.
8. Select **Connect**.

The Defender portal creates the required Azure resources and connects the new workspace to the Defender portal.

Provisioning can take several minutes. During provisioning, the setup shows the following states:

- **Creating resources** - The required Azure resources are being deployed.
- **Connecting the workspace** - The newly created workspace is being connected to the Defender portal.

When provisioning is complete, a confirmation dialog appears and the workspace is listed on the **SIEM workspaces** page.