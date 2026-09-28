---
layout: Conceptual
title: Set up email notifications for your security team - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-email-notifications
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Set up email notifications to tell your security team about alerts and vulnerabilities in Defender for Business.
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.service: defender-business
ms.localizationpriority: medium
ms.reviewer: nehabha
ms.date: 2024-06-19T00:00:00.0000000Z
ms.collection:
- m365-security
- m365solution-mdb-setup
- highpri
- tier1
locale: en-us
document_id: 463b8710-8c69-b446-765f-2977c83855aa
document_version_independent_id: 463b8710-8c69-b446-765f-2977c83855aa
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-email-notifications.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-email-notifications
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-email-notifications.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: eac84425-454b-0d56-6a72-8a1a470173f2
---

# Set up email notifications for your security team - Microsoft Defender for Business | Microsoft Learn

This article describes how to set up email notifications for your security team.

![Visual depicting step 4 - set up email notifications for your security team.](media/mdb-setup-step4.png)

When you can set up email notifications for your security team, they can be notified via email whenever any alerts are generated, or new vulnerabilities are discovered.

## What to do

1. Learn about types of email notifications.
2. View and edit email notification settings.
3. Proceed to your next steps.

## Types of email notifications

When you set up email notifications, you can choose from the following types:

- **Vulnerabilities**: When new exploits or vulnerability events are detected.
- **Alerts & vulnerabilities**: When detected threats on devices generate alerts, or when new exploits or vulnerability events are detected.

Tip

**Email notifications aren't the only way your security team can find out about new alerts or vulnerabilities**. For example:

- Whenever your security team signs into the Microsoft Defender portal, they see cards highlighting new threats, alerts, and vulnerabilities. Defender for Business is designed to highlight important information that your security team cares about as soon as they sign in.
- The **Incidents** page. To learn more, see [View and manage incidents in Defender for Business](mdb-view-manage-incidents).

## View and edit email notifications

To view or edit email notification settings for your company, follow these steps:

1. Go to the Microsoft Defender portal (https://security.microsoft.com) and sign in.
2. In the navigation pane, select **Settings**, and then select **Endpoints**. Then, under **General**, select **Email notifications**.
3. Review the information on the **Alerts** and **Vulnerabilities** tabs.

    - If you don't see any items listed on the **Alerts** tab, you can create a rule for people to be notified when alerts are generated. To get help with this task, see [Create rules for alert notifications](/en-us/defender-xdr/configure-email-notifications).
    - If you don't see any items listed on the **Vulnerabilities** tab, you can create a rule for people to be notified whenever a new vulnerability is discovered. To get help with this task, see [Create rules for vulnerability events](/en-us/defender-endpoint/configure-vulnerability-email-notifications).
    - If you do have rules created, select a rule to edit it. You can also delete a rule.

Important

When you set up email notifications in Defender for Business, you must assign the notification rules to specific users. Defender for Business doesn't use [role-based access control like Defender for Endpoint does](/en-us/defender-endpoint/rbac).

You can't apply email notifications to device groups in Defender for Business.