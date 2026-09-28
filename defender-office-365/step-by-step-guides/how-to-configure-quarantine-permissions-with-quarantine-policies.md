---
layout: Conceptual
title: How to configure quarantine permissions and policies - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/how-to-configure-quarantine-permissions-with-quarantine-policies
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: The steps to configure quarantine policies and permissions across different groups, including AdminOnlyPolicy, limited access, full access, and providing security admins and users with a simple way to manage false positive folders.
ms.service: defender-office-365
author: chrisda
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 4e36444b-f035-f2a6-8efe-fef3ae8a01ca
document_version_independent_id: 4e36444b-f035-f2a6-8efe-fef3ae8a01ca
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/how-to-configure-quarantine-permissions-with-quarantine-policies.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/how-to-configure-quarantine-permissions-with-quarantine-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/how-to-configure-quarantine-permissions-with-quarantine-policies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 47bfb241-a270-352c-2233-8f03617eaeaf
---

# How to configure quarantine permissions and policies - Microsoft Defender for Office 365 | Microsoft Learn

Providing security admins and users with a simple way to manage false positive folders is vital, given the increased demand for a more aggressive security posture with the evolution of hybrid work. Taking a prescriptive approach, admins and users can manage false positive folders effectively with the guidance in this article.

Tip

For a short video aimed at admins trying to set quarantine permissions and policies, see [Configure quarantine permissions and policies](https://www.youtube.com/watch?v=vnar4HowfpY). If you are an end user, see this [overview of quarantine permissions and policies](https://www.youtube.com/watch?v=s-vozLO43rI).

## Prerequisites

Before you begin, make sure you have the following:

- Sufficient permissions (Security Administrator role)
- 5 minutes to perform the following procedures.

## Deciding between built-in or custom quarantine policies

Custom quarantine policies let admins decide which items users can triage in the ***False positive*** folder. Admins can also allow users to request the *release* of those items from the folder.

1. Decide what verdicts category (bulk, spam, phish, high confidence phish, or malware) of items you want your user to triage and not triage.
2. For each verdict category that you don't want users to triage, assign messages in that category to the **AdminOnlyPolicy**. As for the category you want users to triage with limited access, you can *create a custom policy* with a request release access and assign users to that verdict category.
3. It's **strongly recommended** that malware and high confidence phish items be assigned to **AdminOnlyPolicy**, regular confidence phish items be assigned *limited access with request release*, while bulk and spam can be left as full access for users.

Important

For more information on how to create granular custom quarantine policies, see [Quarantine policies](../quarantine-policies).

## Assigning quarantine policies and enabling notification with organization branding

When your security team has decided on which categories of items that users can triage (or not), and they've created the corresponding quarantine policies, admins should assign the corresponding quarantine policies to the appropriate users and enable notifications.

1. Identify the users, groups, or domains that you would like to include in the *full access* category vs. the *limited access* category, versus the *Admin-Only* category.
2. Sign in to the [Microsoft Security portal](https://security.microsoft.com).
3. On the left nav, under **Email & collaboration**, select **Policies & rules**.
4. Select **Threat policies**.
5. Select each of the following: **Anti-spam policies**, **Anti-phishing policy**, **Anti-Malware policy**.
6. Select **Create policy** and choose **Inbound**.
7. Add policy Name, users, groups, or domains to apply the policy to, and **Next**.
8. In the **Actions** tab, select **Quarantine message** for categories. You notice another panel for *select quarantine policy*. Use the dropdown to select the custom quarantine policy you created in Deciding between built-in or custom quarantine policies.
9. Move on to the **Review** section and select the **Confirm** button to create the new policy.
10. For each remaining policy (**Anti-phishing policy**, **Anti-Malware policy**, and **Safe Attachment policy**), select **Create policy** &gt; **Inbound**, add the policy name and recipients, select **Quarantine message** with your custom quarantine policy in the **Actions** tab, and then select **Confirm** in the **Review** section.

Tip

For more detailed information about configuring anti-spam, anti-phishing, and Safe Attachments policies, see:

- [Configure spam filter policies](../anti-spam-policies-configure)
- [Configure anti-phishing policies if you don't have Microsoft Defender for Office 365](../anti-phishing-policies-eop-configure)
- [Configure anti-phishing policies in Microsoft Defender for Office 365](../anti-phishing-policies-mdo-configure)
- [Set up Safe Attachments policies in Microsoft Defender for Office 365](../safe-attachments-policies-configure)