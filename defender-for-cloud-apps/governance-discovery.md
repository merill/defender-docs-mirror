---
layout: Conceptual
title: Govern discovered apps - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/governance-discovery
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Govern discovered apps by sanctioning approved apps or unsanctioning and blocking unwanted apps in your organization.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 0af2ab7c-033d-5769-c3a2-a7060c0996e6
document_version_independent_id: 0af2ab7c-033d-5769-c3a2-a7060c0996e6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/governance-discovery.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: governance-discovery
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/governance-discovery.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 0af08e99-65b5-ae06-85c0-f6f7de4ca1b6
---

# Govern discovered apps - Microsoft Defender for Cloud Apps | Microsoft Learn

Microsoft Defender for Cloud Apps lets you govern discovered apps by approving safe apps (**Sanctioned**) or prohibiting unwanted apps (**Unsanctioned**). Sanctioned apps are marked as approved for use, while unsanctioned apps can be monitored or blocked. This article covers how to sanction or unsanction apps, block apps by using built-in streams or block scripts, and resolve governance conflicts.

## Prerequisites

Before you block discovered cloud apps, make sure you meet these requirements:

- [Configure **Cloud Protection** in Microsoft Defender for Endpoint](/en-us/defender-endpoint/cloud-protection-configure)
- [Turn on **Network Protection** in Microsoft Defender for Endpoint](/en-us/defender-endpoint/network-protection#required-browser-configuration)
- Install the **Microsoft Defender Browser Protection** add-on in all non-Microsoft browsers in your organization.

## Sanctioning/unsanctioning an app

You can mark a specific risky app as unsanctioned by clicking the three dots at the end of the row. Then select **Unsanctioned**. Unsanctioning an app doesn't block use, but enables you to more easily monitor its use with the cloud discovery filters. You can then notify users of the unsanctioned app and suggest an alternative safe app for their use, or [generate a block script using the Defender for Cloud Apps APIs](api-discovery-script) to block all unsanctioned apps.

[![Tag as unsanctioned.](media/tag-as-unsanctioned.png)](media/tag-as-unsanctioned.png#lightbox)

Note

An app that is onboarded to inline proxy or connected via app connector, all such applications would be auto sanctioned state in Cloud Discovery.

## Blocking apps with built-in streams

If your organization's Microsoft 365 tenant uses Microsoft Defender for Endpoint, apps you mark as unsanctioned are blocked automatically. You can also scope blocking to specific device groups, monitor apps, and use the [warn and educate users when accessing risky apps](mde-govern#educate-users-when-accessing-risky-apps) features. For more information, see [Govern discovered apps using Microsoft Defender for Endpoint](mde-govern).

If your tenant uses Zscaler NSS, iboss, Corrata, Menlo, or Open Systems, unsanctioned apps are also blocked. However, you can't scope blocking by device groups or use the [warn and educate users when accessing risky apps](mde-govern#educate-users-when-accessing-risky-apps) features. For more information, see [Integrate with Zscaler](zscaler-integration), [Integrate with iboss](iboss-integration), [Integrate with Corrata](corrata-integration), [Integrate with Menlo](menlo-integration), and [Integrate with Open Systems](open-systems-integration).

## Block apps by exporting a block script

Defender for Cloud Apps enables you to block access to unsanctioned apps by using your existing on-premises security appliances. You can generate a dedicated block script and import it to your appliance. Using a block script doesn't require redirection of all of the organization's web traffic to a proxy.

Before you begin, make sure you have a supported on-premises security appliance configured and available to import the block script.

1. In the cloud discovery dashboard, tag any apps you want to block as **Unsanctioned**.

    [![Tag as unsanctioned.](media/tag-as-unsanctioned.png)](media/tag-as-unsanctioned.png#lightbox)
2. In the title bar, select **Actions** and then select **Generate block script...**.

    ![Screenshot of the Generate block script option in the Actions menu of Microsoft Defender for Cloud Apps.](media/generate-block-script.png)
3. In **Generate block script**, select the appliance you want to generate the block script for.

    ![Screenshot of the Generate block script dialog showing the appliance selection option for generating a block script.](media/generate-block-script-pop-up.png)
4. Then select the **Generate script** button to create a block script for all your unsanctioned apps. By default, the file is named with the date on which it was exported and the appliance type you selected. *2017-02-19\_CAS\_Fortigate\_block\_script.txt* would be an example file name.

    ![Screenshot of the Generate script button used to create a block script for all unsanctioned apps.](media/generate-block-script-button.png)
5. Import the file created to your appliance.

## Blocking unsupported streams

If your tenant doesn't use Microsoft Defender for Endpoint, Zscaler NSS, iboss, Corrata, Menlo, or Open Systems, you can export all domains for unsanctioned apps. Then configure your third-party appliance to block those domains.

In the **Discovered apps** page, filter all *Unsanctioned* apps and then use the export capability to export all the domains.

## Nonblockable applications

Some services are critical to business operations. To prevent downtime, you can't block these services in Defender for Cloud Apps, whether through the UI or policies:

- Microsoft Defender for Cloud Apps
- Microsoft Defender Security Center
- Microsoft 365 Security Center
- Microsoft Defender for Identity
- Microsoft Purview
- Microsoft Entra Permissions Management
- Microsoft Conditional Access Application Control
- Microsoft Secure Score
- Microsoft Purview
- Microsoft Intune
- Microsoft Support
- Microsoft AD FS Help
- Microsoft Support
- Microsoft Online Services

## Resolve governance conflicts between manual actions and policies

If there's a conflict between a manual sanction or unsanction action and a [governance action set by a cloud discovery policy](cloud-discovery-policies), the last operation applied takes precedence.