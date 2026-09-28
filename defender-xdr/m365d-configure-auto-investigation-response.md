---
layout: Conceptual
title: Configure automated investigation and response capabilities in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/m365d-configure-auto-investigation-response
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Set up automated investigation and response in Microsoft Defender XDR by reviewing prerequisites, configuring automation levels for device groups, and checking security and alert policies to enable self-healing workflows.
ms.author: guywild
author: guywi-ms
ms.topic: how-to
ms.service: defender-xdr
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
ms.custom:
- msecd-doc-authoring-1014
- autoir
- admindeeplinkDEFENDER
ms.reviewer: evaldm, isco
ai-usage: ai-assisted
locale: en-us
document_id: 575ef4e4-8f41-0aa2-a9a1-50ee2cf82ced
document_version_independent_id: 575ef4e4-8f41-0aa2-a9a1-50ee2cf82ced
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/m365d-configure-auto-investigation-response.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: m365d-configure-auto-investigation-response
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/m365d-configure-auto-investigation-response.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: e584e340-a64d-499b-1a0f-dd90432ac52f
---

# Configure automated investigation and response capabilities in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Microsoft Defender XDR includes powerful [automated investigation and response capabilities](m365d-autoir) that can save your security operations team much time and effort. With [self-healing](m365d-autoir#how-automated-investigation-and-self-healing-works), these capabilities mimic the steps a security analyst would take to investigate and respond to threats, only faster, and with more ability to scale.

This article describes how to configure automated investigation and response in [Microsoft Defender XDR](https://go.microsoft.com/fwlink/p/?linkid=2077139) with these steps:

1. Review the prerequisites.
2. Review or change the automation level for device groups.
3. Review your security and alert policies in Office 365.

After configuring automated investigation and response, you can [view and manage remediation actions in the Action center](m365d-autoir-actions) and update automated investigation settings as needed.

## Prerequisites for automated investigation and response in Microsoft Defender XDR

The following table lists the requirements for automated investigation and response in Microsoft Defender XDR.

| Requirement | Details |
| --- | --- |
| Subscription requirements | One of these subscriptions: <br>- Microsoft 365 E5<br>- Microsoft 365 A5<br>- Microsoft 365 E3 with the Microsoft Defender Suite add-on<br>- Microsoft 365 A3 with the Microsoft 365 A5 Security add-on<br>- Office 365 E5 plus Enterprise Mobility + Security E5 plus Windows E5<br><br> See [Microsoft Defender XDR licensing requirements](prerequisites#licensing-requirements). |
| Network requirements | - [Microsoft Defender for Identity](/en-us/azure-advanced-threat-protection/what-is-atp) enabled<br>- [Microsoft Defender for Cloud Apps](/en-us/cloud-app-security/what-is-cloud-app-security) configured<br>- [Microsoft Defender for Identity integration](/en-us/cloud-app-security/mdi-integration) |
| Windows device requirements | - Windows 11<br>- Windows 10, version 1709 or later installed (See [Windows release information](/en-us/windows/release-information/))<br>- The following threat protection services are configured:<br>    - [Microsoft Defender for Endpoint](/en-us/defender-endpoint/onboard-windows-client)<br>    - [Microsoft Defender Antivirus](/en-us/windows/security/threat-protection/windows-defender-antivirus/configure-windows-defender-antivirus-features) |
| Protection for email content and Office files | - [Microsoft Defender for Office 365 is configured](/en-us/defender-office-365/mdo-deployment-guide#step-2-configure-protection-policies)<br>- [Automated investigation and remediation capabilities in Defender for Endpoint are configured](/en-us/defender-endpoint/configure-automated-investigations-remediation) (required for manual response actions, such as deleting email messages on devices) |
| Permissions | To configure automated investigation and response capabilities, you must have one of the following roles assigned in either Microsoft Entra ID (https://portal.azure.com) or in the Microsoft 365 admin center (https://admin.microsoft.com): <br>- Security Administrator or higher<br><br>To work with automated investigation and response capabilities, such as by reviewing, approving, or rejecting pending actions, see [Required permissions for Action center tasks](m365d-action-center#required-permissions-for-action-center-tasks). |

## Review or change the automation level for device groups

Whether automated investigations run, and whether remediation actions are taken automatically or only upon approval for your devices depend on certain settings, such as your organization's device group policies. Review the configured automation level for your device group policies. You must be at least a security administrator to perform the following procedure:

1. Go to the Microsoft Defender portal at https://security.microsoft.com and sign in.
2. Go to **System** &gt; **Settings** &gt; **Endpoints** &gt; **Device groups** under **Permissions**.
3. Review your device group policies. In particular, look at the **Remediation level** column. We recommend using **Full - remediate threats automatically**. You might need to create or edit your device groups to get the level of automation you want. To get help creating or editing device groups, see the following articles:

    - [How threats are remediated](/en-us/defender-endpoint/automated-investigations#how-threats-are-remediated)
    - [Create and manage device groups](/en-us/defender-endpoint/machine-groups)

## Review your security and alert policies in Office 365

Microsoft provides built-in [alert policies](alert-policies) that help identify certain risks. These risks include Exchange admin permissions abuse, malware activity, potential external and internal threats, and data lifecycle management risks. Some alerts can trigger [automated investigation and response in Office 365](/en-us/defender-office-365/air-about). Make sure your [Defender for Office 365](/en-us/defender-office-365/mdo-about) features are configured correctly.

Although certain alerts and security policies can trigger automated investigations, *no remediation actions are taken automatically for email and content*. Instead, all remediation actions for email and email content await approval by your security operations team in the [Action center](m365d-action-center).

[The built-in security features for all cloud mailboxes](/en-us/defender-office-365/eop-about) and Defender for Office 365 help protect email and content. We recommend using the Standard and Strict [preset security policies](/en-us/defender-office-365/preset-security-policies#preset-security-policies-in-eop-and-microsoft-defender-for-office-365) to assign protection to users.

If you're using custom policies, use the [Configuration analyzer](/en-us/defender-office-365/configuration-analyzer-for-security-policies) to compare your policy settings to the Standard and Strict preset security policy settings. For a detailed listing of all policy settings, see the tables in [Recommended email and collaboration threat policy settings for cloud organizations](/en-us/defender-office-365/recommended-settings-for-eop-and-office365).

You can review your [alert policies](/en-us/defender-office-365/alert-policies-defender-portal) in the Defender portal at https://security.microsoft.com &gt; **Policies & rules** &gt; **Alert policy** or directly at https://security.microsoft.com/alertpoliciesv2. Several default alert policies are in the **Threat management** category. Some of the alert policies in the **Threat management** category can trigger automated investigation and response. To learn more, see [Threat management alert policies](alert-policies#threat-management-alert-policies).

## Change automated investigation settings

You can choose from several options to change settings for your automated investigation and response capabilities. Some options are listed in the following table:

| To do this | Follow these steps |
| --- | --- |
| Specify automation levels for groups of devices | 1. Set up one or more device groups. See [Create and manage device groups](/en-us/defender-endpoint/machine-groups).<br>2. In the Microsoft Defender portal, go to **Permissions** &gt; **Endpoints roles & groups** &gt; **Device groups**.<br>3. Select a device group and review its **Automation level** setting. (We recommend using **Full - remediate threats automatically**). See [Automation levels in automated investigation and remediation capabilities](/en-us/defender-endpoint/automation-levels).<br>4. Repeat steps 2 and 3 as appropriate for all your device groups. |