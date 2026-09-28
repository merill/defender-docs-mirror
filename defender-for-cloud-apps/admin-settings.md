---
layout: Conceptual
title: Configure admin notifications - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/admin-settings
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
description: Configure admin notification settings in Defender for Cloud Apps to control whether administrators receive email alerts for policy violations.
ms.date: 2026-06-16T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Naama-Goldbart
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: f99e2fc0-f675-999e-118d-ea9f9141cc5c
document_version_independent_id: f99e2fc0-f675-999e-118d-ea9f9141cc5c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/admin-settings.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: admin-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/admin-settings.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: f4e6f39d-978e-82db-d7f8-40c6d7b66d14
---

# Configure admin notifications - Microsoft Defender for Cloud Apps | Microsoft Learn

Microsoft Defender for Cloud Apps allows you to customize admin email notification settings. As an administrator, you can configure which policy violation alerts trigger email notifications and set the minimum severity level for those notifications. Email notifications are sent to the email alias associated with your administrator account. Notifications aren't sent for Microsoft Entra IPC events.

## Customize admin email notification settings

Use the following steps to customize your admin email notification settings in the Microsoft Defender Portal:

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **My account**, select **My email notifications**.
3. In the **My email notifications** page, set the email notification preferences for emails you receive from the system. You can set the severity that determines which alerts and violations you want to receive emails. The severity is set per policy. When violations are triggered, you receive email notification depending on the setting here and the Severity setting in the policy that was violated. Emails are sent to the alias associated with the administrator user account you used to sign in to Defender for Cloud Apps.

    Note

    - Notifications are not sent for Microsoft Entra IPC events.

    ![Screenshot of the email notification settings page showing severity and notification preference options.](media/notification-settings.png)
4. When you're done, select **Save**.