---
layout: Conceptual
title: Test your ASR rules deployment - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/attack-surface-reduction-rules-deployment-test
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to test attack surface reduction (ASR) rules in Audit mode, review triggered events, and configure exclusions before enabling rules in Block mode.
ms.service: defender-endpoint
ms.subservice: asr
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.reviewer: sugamar
ms.custom: msecd-doc-authoring-1016 - asr - sfi-image-nochange
ms.topic: how-to
ms.collection:
- m365-security
- m365solution-asr-rules
- highpri
- tier1
- mde-asr
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 21ddde49-4d45-088d-453f-10e37a1a3981
document_version_independent_id: 21ddde49-4d45-088d-453f-10e37a1a3981
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/attack-surface-reduction-rules-deployment-test.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: attack-surface-reduction-rules-deployment-test
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/attack-surface-reduction-rules-deployment-test.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bba62c59-6b53-4be4-8b9d-6624f9184c22
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f3a81ffb-ee36-4ec7-b54a-01b6681aff65
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 90e32960-d36c-85b1-5f26-458a3dabe6dc
---

# Test your ASR rules deployment - Microsoft Defender for Endpoint | Microsoft Learn

This article is part of the [Attack surface reduction rules deployment guide](attack-surface-reduction-rules-deployment).

Testing attack surface reduction (ASR) rules is a critical step in your deployment. You need to determine if any ASR rules will block your line-of-business apps. By starting with a small, controlled group, you can limit potential work disruptions as you expand the deployment across your organization.

Note

Before you begin the testing phase of your ASR rules deployment, disable any related ASR rules that are currently enabled in **Block** or **Warn** mode (if applicable). For information about using the report to find enabled ASR rules, see [Attack surface reduction rules reports](attack-surface-reduction-rules-report).

As illustrated in the following diagram, begin your ASR rules deployment with ring 1 (the initial small pilot group of devices used for testing).

> 
> [![Diagram of the ASR rules testing steps: audit rules, review data, and configure exclusions.](media/asr-rules-testing-steps.png)](media/asr-rules-testing-steps.png#lightbox)

## Assess and evaluate rules before deployment

If you have Defender for Endpoint Plan 2 (which includes advanced vulnerability management and hunting capabilities), [Microsoft Defender Vulnerability Management](/en-us/defender-vulnerability-management/defender-vulnerability-management) surfaces ASR rule–related security recommendations that can provide high-level impact indicators (for example, whether audit activity was observed across devices).

In the Microsoft Defender portal at https://security.microsoft.com, go to **Exposure management** &gt; **Recommendations** (or directly to the **Security recommendations** page at https://security.microsoft.com/exposure-recommendations). On the **Security recommendations** page, select an ASR rule to open the details flyout, and then select the **Devices** tab. The **User impact** value shows the percentage of devices that can accept a new policy enabling the rule in block mode without adversely affecting productivity.

[![Screenshot of the Devices tab of an ASR rule security recommendation showing user impact.](media/asrrecommendation.png)](media/asrrecommendation.png#lightbox)

Note

To accurately assess the potential effect of an ASR rule before enabling it in **Block** or **Warn** mode, you must review **Audit** mode data and detailed reporting, such as the [Attack surface reduction rule report](attack-surface-reduction-rules-report) or [Advanced hunting data](attack-surface-reduction-rules-monitor#asr-rule-events-in-advanced-hunting).

## Step 1: Test all ASR rules in Audit mode

Note

As described in [ASR rules](attack-surface-reduction-rules-overview#asr-rules), you can typically enable the standard protection rules in **Block** or **Warn** mode without testing.

Typically, enable all ASR rules in **Audit** mode at the same time so you can determine which rules are triggered by everyday business activities. Start with your ASR rule champions or devices in ring 1.

ASR rules in **Audit** mode don't affect users. But the rules generate logged events that you can evaluate.

If your organization has Microsoft Intune (included in subscriptions like Microsoft 365 E5 or available as an add-on), use the **Attack surface reduction** endpoint security policy in Intune to configure and distribute ASR rules in **Audit** mode. For instructions, see [Configure ASR rules and exclusions in Intune using endpoint security policies](attack-surface-reduction-rules-configure#configure-asr-rules-and-exclusions-in-intune-using-endpoint-security-policies).

If you don't have Intune, other ASR rule deployment methods are available:

- [Microsoft Configuration Manager](attack-surface-reduction-rules-configure#configure-asr-rules-and-global-asr-rule-exclusions-in-microsoft-configuration-manager)
- [Any MDM solution using the Policy CSP](attack-surface-reduction-rules-configure#configure-asr-rules-in-any-mdm-solution-using-the-policy-csp)
- [Group Policy](attack-surface-reduction-rules-configure#configure-asr-rules-in-group-policy)
- [PowerShell](attack-surface-reduction-rules-configure#configure-asr-rules-in-powershell)

Tip

The deployment method you use for ASR rules doesn't affect reporting data, as long as the devices are enrolled in Defender for Endpoint.

## Step 2: Review ASR rule data and assess impact

After ASR rules are deployed in **Audit** mode, review the triggered events to assess their effects and identify potential exclusions. The reporting methods available to you depend on your product and plan: the ASR rules report and device timeline require Defender for Endpoint Plan 2 or Microsoft Defender for Business, Advanced hunting requires Defender for Endpoint Plan 2, and Windows Event Viewer is available with any plan. Use one or more of the following methods:

In Defender for Endpoint Plan 2 or Microsoft Defender for Business, use the **Attack surface reduction rules report** in the Microsoft Defender portal. For complete information, see [Attack surface reduction (ASR) rules report](attack-surface-reduction-rules-report).

In Defender for Endpoint Plan 2, use Advanced hunting to find ASR rule events. For more information, see [ASR rule events in Advanced Hunting](attack-surface-reduction-rules-monitor#asr-rule-events-in-advanced-hunting).

In Defender for Endpoint Plan 2 or Defender for Business, use the Defender for Endpoint device timeline. For more information, see [Microsoft Defender for Endpoint device timeline](investigate-machines#investigate-device-timeline).

Otherwise, ASR rule events are available only in Windows Event Viewer on the local device. But you can use [Windows Event Forwarding](/en-us/windows/security/operating-system-security/device-management/use-windows-event-forwarding-to-assist-in-intrusion-detection) to centralize the ASR rule data collection.

Specifically, look for **Event ID 1122** in the **Applications and Services Logs** &gt; **Microsoft** &gt; **Windows** &gt; **Windows Defender** &gt; **Operational** log (events for rules in **Audit** mode). For a complete list of ASR rule event IDs and detailed steps, see [View attack surface reduction events in Windows Event Viewer](attack-surface-reduction-windows-events#browse-attack-surface-reduction-events-in-windows-event-viewer).

## Step 3: Configure ASR rule exclusions

After you review ASR rule data from **Audit** mode, you might find that some ASR rules block legitimate business apps or activity (known as *false positives*). You can add exclusions to prevent ASR rules from evaluating the affected files or folders.

For an overview of supported exclusion types for ASR rules, see [File and folder exclusions for ASR rules](attack-surface-reduction-rules-overview#file-and-folder-exclusions-for-asr-rules).

If you used an **Attack surface reduction** endpoint security policy in Microsoft Intune to deploy the ASR rules, use the same policy to configure ASR rule exclusions. For instructions, see [Configure ASR rules and exclusions in Intune using endpoint security policies](attack-surface-reduction-rules-configure#configure-asr-rules-and-exclusions-in-intune-using-endpoint-security-policies).

If you used a different method to deploy the ASR rules, use the same method to configure ASR rule exclusions:

- [Microsoft Configuration Manager](attack-surface-reduction-rules-configure#configure-asr-rules-and-global-asr-rule-exclusions-in-microsoft-configuration-manager)
- [Group Policy](attack-surface-reduction-rules-configure#configure-asr-rules-and-exclusions-in-group-policy)
- [Any MDM solution using the Policy CSP](attack-surface-reduction-rules-configure#configure-global-asr-rule-exclusions-in-any-mdm-solution-using-the-policy-csp)
- [PowerShell](attack-surface-reduction-rules-configure#configure-global-asr-rule-exclusions-in-powershell)

Tip

Rule exclusions are better than turning off rules or switching them back to **Audit** mode. Take advantage of **Warn** mode in available rules to limit disruptions without disabling the rule entirely. For more information, see [Modes for ASR rules](attack-surface-reduction-rules-overview#modes-for-asr-rules).