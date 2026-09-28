---
layout: Conceptual
title: Weekly operational guide - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/ops-guide/ops-guide-weekly
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
description: This article provides weekly operational recommendations to help security operations teams to plan and run security activities.
ms.date: 2023-11-28T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 3ecbc4e9-83e1-780a-9803-348ec498b686
document_version_independent_id: 3ecbc4e9-83e1-780a-9803-348ec498b686
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/ops-guide/ops-guide-weekly.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ops-guide/ops-guide-weekly
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/ops-guide/ops-guide-weekly.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: 7d89c872-2c50-ac3f-7ca4-2a352537a1a0
---

# Weekly operational guide - Microsoft Defender for Cloud Apps | Microsoft Learn

This article lists weekly operational activities that we recommend you perform with Microsoft Defender for Cloud Apps.

## Review SaaS security posture management

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select **Secure Score**.

**Persona**: Security and Compliance administrators, SOC analysts

SaaS Security Posture Management (SSPM) capabilities in Microsoft Defender for Cloud Apps enable you to get deeper visibility, automatically identify SaaS app misconfigurations, and help you remediate those misconfigurations to improve your organizational security.

Defender for Cloud Apps SSPM features are integrated into Microsoft Defender so that security teams can see their holistic security posture across the enterprise with Microsoft Secure Score.

To view Secure Score recommendations per product, in Microsoft Defender XDR, select **Secure Score** &gt; **Recommended actions**, and group the list by **Product**.

## Check app connectors, log collectors, and SIEM agent health

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select **Settings &gt; Cloud apps**.

**Persona**: Security and Compliance administrators, SOC analysts

System alerts are raised when a connector, agent, or log collector fails and it's impossible to send a notification to a Defender for Cloud Apps administrator. We recommend checking for system alerts regularly to monitor the health of your app connectors, log collectors, and SIEM agents.

If you're using a SIEM agent, system alerts can be sent directly to your SIEM system. In Microsoft Defender XDR, select **Settings &gt; Cloud apps &gt; System &gt; SIEM Agents**, and [configure your SIEM agent](../siem). In the **Data Types** section, select **Alerts**, and make sure the **Alert type filter** contains system alerts.

We also recommend reviewing the following settings to ensure that they're correct and up to date:

| Status to check | Where to check in the Defender portal |
| --- | --- |
| **App connectors** | **Settings &gt; Cloud apps &gt; Connected apps &gt; App Connectors** |
| **Conditional Access App Control apps** | **Settings &gt; Cloud apps &gt; Connected apps &gt; Conditional Access App Control apps** |
| **Automatic log upload** | **Settings &gt; Cloud apps &gt; Cloud Discovery &gt; Automatic log upload** |
| **API tokens** | **Settings &gt; Cloud apps &gt; System &gt; API tokens** |

For more information, see:

- [Connect apps to get visibility and control with Microsoft Defender for Cloud Apps](../enable-instant-visibility-protection-and-governance-actions-for-your-apps)
- [Protect apps with Microsoft Defender for Cloud Apps conditional access app control](../proxy-intro-aad)
- [Configure automatic log upload for continuous reports](../discovery-docker)
- [Managing API tokens](../api-authentication)

## Track new changes in Microsoft Defender XDR

**Where**: In the Microsoft 365 admin center, select **Health &gt; Message center**

**Persona**: Security administrators

The Microsoft 365 **Message center** helps you to keep track of upcoming changes, including new features, planned maintenance, or other important announcements that might affect your Defender for Cloud Apps environment.

For more information, see [Track new and changed features in the Microsoft 365 Message center](/en-us/microsoft-365/admin/manage/message-center).

## Review the governance log

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), under **Cloud apps**, select **Governance log**.

**Persona**: Security and Compliance administrators

The Governance log provides a status record of each task that you configure Defender for Cloud Apps to run, including both manual and automatic tasks. These tasks include tasks configured in policies, governance actions that you set on files and users, and any other action you set Defender for Cloud Apps to take.

For more information, see [Governing connected apps](../governance-actions).