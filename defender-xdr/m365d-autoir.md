---
layout: Conceptual
title: Automated investigation and response in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/m365d-autoir
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Get an overview of automated investigation and response capabilities, also called self-healing, in Microsoft Defender XDR
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.date: 2025-04-28T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
ms.topic: overview
ms.custom: autoir
ms.reviewer: evaldm, isco
locale: en-us
document_id: c8f56099-1b2a-824a-b259-a75abbf79ff8
document_version_independent_id: c8f56099-1b2a-824a-b259-a75abbf79ff8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/m365d-autoir.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: m365d-autoir
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/m365d-autoir.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 90d2be49-1e16-d187-d125-4e9f5e912878
---

# Automated investigation and response in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

If your organization is using [Microsoft Defender XDR](microsoft-365-defender), your security operations team receives an alert within the Microsoft Defender portal whenever a malicious or suspicious activity or artifact is detected. Given the seemingly never-ending flow of threats that can come in, security teams often face the challenge of addressing the high volume of alerts. Fortunately, Microsoft Defender XDR includes automated investigation and response (AIR) capabilities that can help your security operations team address threats more efficiently and effectively.

This article provides an overview of AIR and includes links to next steps and additional resources.

## How automated investigation and self-healing works

As security alerts are triggered, it's up to your security operations team to look into those alerts and take steps to protect your organization. Prioritizing and investigating alerts can be very time consuming, especially when new alerts keep coming in while an investigation is going on. Security operations teams can feel overwhelmed by the sheer volume of threats they must monitor and protect against. Automated investigation and response capabilities, with self-healing, in Microsoft Defender XDR can help.

Watch the following video to see how self-healing works: 

In Microsoft Defender XDR, automated investigation and response with self-healing capabilities works across your devices, email & content, and identities.

Tip

This article describes how automated investigation and response works. To configure these capabilities, see [Configure automated investigation and response capabilities in Microsoft Defender XDR](m365d-configure-auto-investigation-response).

## Your own virtual analyst

Imagine having a virtual analyst in your Tier 1 or Tier 2 security operations team. The virtual analyst mimics the ideal steps that security operations would take to investigate and remediate threats. The virtual analyst could work 24x7, with unlimited capacity, and take on a significant load of investigations and threat remediation. Such a virtual analyst could significantly reduce the time to respond, freeing up your security operations team for other important threats or strategic projects. If this scenario sounds like science fiction, it's not! Such a virtual analyst is part of your Microsoft Defender XDR suite, and its name is *automated investigation and response*.

Automated investigation and response capabilities enable your security operations team to dramatically increase your organization's capacity to deal with security alerts and incidents. With automated investigation and response, you can reduce the cost of dealing with investigation and response activities and get the most out of your threat protection suite. Automated investigation and response capabilities help your security operations team by:

1. Determining whether a threat requires action.
2. Taking (or recommending) any necessary remediation actions.
3. Determining whether and what other investigations should occur.
4. Repeating the process as necessary for other alerts.

## The automated investigation process

An alert creates an incident, which can start an automated investigation. The automated investigation results in a verdict for each piece of evidence. Verdicts can be:

- *Malicious*
- *Suspicious*
- *No threats found*

Remediation actions for malicious or suspicious entities are identified. Examples of remediation actions include:

- Sending a file to quarantine
- Stopping a process
- Isolating a device
- Blocking a URL
- Other actions

For more information, see [Remediation actions in Microsoft Defender XDR](m365d-remediation-actions).

Depending on [how automated investigation and response capabilities are configured](m365d-configure-auto-investigation-response) for your organization, remediation actions are taken automatically or only upon approval by your security operations team. All actions, whether pending or completed, are listed in the [Action center](m365d-action-center).

While an investigation is running, any other related alerts that arise are added to the investigation until it completes. If an affected entity is seen elsewhere, the automated investigation expands its scope to include that entity, and the investigation process repeats.

In Microsoft Defender XDR, each automated investigation correlates signals across Microsoft Defender for Identity, Microsoft Defender for Endpoint, and Microsoft Defender for Office 365, as summarized in the following table:

| Entities | Threat protection services |
| --- | --- |
| Devices (also referred to as endpoints or machines) | [Defender for Endpoint](/en-us/defender-endpoint/automated-investigations) |
| On-premises Active Directory users, entity behavior, and activities | [Defender for Identity](/en-us/azure-advanced-threat-protection/what-is-atp) |
| Email content (email messages that can contain files and URLs) | [Defender for Office 365](/en-us/defender-office-365/mdo-about) |

Note

Not every alert triggers an automated investigation, and not every investigation results in automated remediation actions. It depends on how automated investigation and response is configured for your organization. See [Configure automated investigation and response capabilities](m365d-configure-auto-investigation-response).

## Viewing a list of investigations

To view investigations, go to the **Incidents** page. Select an incident, and then select the **Investigations** tab. To learn more, see [Details and results of an automated investigation](m365d-autoir-results).

## Automated investigation & response card

The Automated investigation & response card is available in the Microsoft Defender portal (https://security.microsoft.com) homepage. This card provides visibility to the total number of available remediation actions. The card also gives an overview of all the alerts and required approval time for each alert.

![Screenshot that shows the automated investigation &amp; response card.](media/m365d-autoir/automated-investigation-response-card.png)

Using the Automated investigation & response card, your security operations team can quickly navigate to the Action center by selecting the **View pending actions** link, and then taking appropriate actions. The card enables your security operations team to more effectively manage actions that are pending approval.