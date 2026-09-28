---
layout: Conceptual
title: Integrate Microsoft Defender for Cloud Apps with external security solutions - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/additional-integrations
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
description: Integrate Microsoft Defender for Cloud Apps with third-party threat intelligence feeds, MDM/MTD solutions, and UEBA solutions to enrich investigations and apply device-aware session controls.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 70ea009a-8493-1d25-2c05-ae25b035c72d
document_version_independent_id: 70ea009a-8493-1d25-2c05-ae25b035c72d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/additional-integrations.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: additional-integrations
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/additional-integrations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: e28aedf9-f196-e954-8997-b2eaa5be6b10
---

# Integrate Microsoft Defender for Cloud Apps with external security solutions - Microsoft Defender for Cloud Apps | Microsoft Learn

You can integrate Microsoft Defender for Cloud Apps with your other security investments to leverage and enhance an integrated protection ecosystem. For example, you can integrate with external mobile device management solutions, UEBA solutions, and external threat intelligence feeds.

The Defender for Cloud Apps robust platform allows you to integrate with a wide variety of external security solutions, including:

- **Threat Intelligence (TI) feeds (Bring Your Own TI)** You can use the Defender for Cloud Apps [IP address range API](api-data-enrichment) to add new risky IP address ranges identified by third-party TI solutions. Once defined, IP address ranges allow you to tag, categorize, and customize how logs and alerts are displayed and investigated.
- **Mobile Device Management (MDM) / Mobile Threat Defense (MTD) solutions** Defender for Cloud Apps provides real-time, granular session controls. A critical factor in the assessment and protection of sessions is the device used by the user, which helps build a comprehensive identity. A device's management status can be identified either directly through the device management status in [Microsoft Entra ID](/en-us/azure/active-directory/conditional-access/overview), [Microsoft Intune](/en-us/mem/intune/protect/mobile-threat-defense), or more generically through the analysis of client certificates that allow integration with a variety of third-party MDM and MTD solutions.

    Defender for Cloud Apps can leverage signals from external MDM and MTD solutions to apply session controls based on a [device's management status](session-policy-aad).
- **UEBA solutions** You can use multiple UEBA solutions to cater for different workloads and scenarios, where each UEBA solution relies on multiple data sources to identify suspicious and anomalous user behavior. Additionally, external UEBA solutions can be integrated with Microsoft's security ecosystem through Microsoft Entra ID Protection.

    Once an external UEBA solution is integrated with Microsoft Entra ID Protection, policies can be used to identify risky users, apply adaptive controls, and automatically remediate dangerous users by setting the user's risk level to high. Once a user is set to high, the relevant policy actions are enforced, such as resetting a user's password, requiring MFA authentication, or forcing a user to use a managed device.

    Defender for Cloud Apps allows security teams to automatically or manually confirm a user as compromised to ensure fast remediation of compromised users.

    For more information, see [How does Microsoft Entra ID use my risk feedback](/en-us/azure/active-directory/identity-protection/howto-identity-protection-risk-feedback#how-does-azure-ad-use-my-risk-feedback).

## Get support

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).