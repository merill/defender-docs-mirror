---
layout: Conceptual
title: Set up web content filtering in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-web-content-filtering
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to set up, view, and edit your web content filtering policy in Microsoft Defender for Business.
author: chrisda
ms.author: chrisda
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.service: defender-business
ms.localizationpriority: medium
ms.reviewer: nehabha
ms.collection:
- SMB
- m365-security
- tier1
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: bdd4d8df-ca89-b50c-1346-ba07d8060fc8
document_version_independent_id: bdd4d8df-ca89-b50c-1346-ba07d8060fc8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-web-content-filtering.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-web-content-filtering
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-web-content-filtering.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 4d5dd7bb-eebc-f2bf-cac2-6acbaea7a235
---

# Set up web content filtering in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

Web content filtering enables your security team to track and regulate access to websites based on content categories. When you set up your web content filtering policy, you enable web protection for your organization.

Web content filtering is available on the major web browsers, with blocks performed by Windows Defender SmartScreen (Microsoft Edge) and Network Protection (Chrome, Firefox, Brave, and Opera). For more information, see [Prerequisites for web content filtering](/en-us/defender-endpoint/web-content-filtering#prerequisites).

In Defender for Business, you can have one web content filtering policy applied to all users.

## Set up web content filtering

Before you begin, make sure your environment meets the [prerequisites for web content filtering](/en-us/defender-endpoint/web-content-filtering#prerequisites).

Use the following steps to create a web content filtering policy:

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings** &gt; **Endpoints** &gt; **Rules** &gt; **Web content filtering**, and then select **+ Add policy**.
2. Specify a name and description for your policy.
3. Select the web content filtering categories to block (for example, **Adult content**, **High bandwidth**, **Legal liability**, or **Leisure**). Don't select **Uncategorized**. Use the expand icon to fully expand each parent category, and then select specific web content categories.

    To set up an audit-only policy that doesn't block any websites, don't select any categories.
4. Apply the policy to all users. (Scoping to specific devices isn't available in Defender for Business.)
5. Review the summary and save the policy. The policy refresh might take up to two hours to apply to your organization's devices.

Tip

To learn more about web content filtering, see [Web content filtering](/en-us/defender-endpoint/web-content-filtering).

## Categories for web content filtering

Not all websites in the following categories are malicious. However, these websites might cause problems for your company due to compliance regulations, bandwidth usage, or other concerns.

You can start with an audit-only policy to better understand whether your security team should block any website categories. You can edit your policy later.

The following table describes web content categories you can choose for your web content filtering policy:

| Category | Description |
| --- | --- |
| **Adult content** | Sites that are related to cults, gambling, nudity, pornography, sexually explicit material, or violence |
| **High bandwidth** | Download sites, image sharing sites, or peer-to-peer hosts |
| **Legal liability** | Sites that include child abuse images, promote illegal activities, foster plagiarism or school cheating, or that promote harmful activities |
| **Leisure** | Sites that provide web-based chat rooms, online gaming, web-based email, or social networking |
| **Uncategorized** | Sites that have no content or that are newly registered.  As a best practice, don't select **Uncategorized**. |