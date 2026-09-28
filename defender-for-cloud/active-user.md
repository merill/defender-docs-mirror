---
layout: Conceptual
title: Assign a recommendation to an active user - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/active-user
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how to assign recommendations to active users in Defender for Cloud to enhance security and streamline remediation processes.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 0bdf3a56-09cc-0635-bc17-d0b1a21584af
document_version_independent_id: 392da661-3a65-e44f-2048-a8f11530f90b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/active-user.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/active-user
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/active-user.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 6c9ff778-20b3-97e3-c97d-303d146df644
---

# Assign a recommendation to an active user - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud has an active user feature. It helps security admins find the users who most often fix recommendations. To keep cloud resources safe, admins need to track and address potential threats and related recommendations.

The active user feature suggests up to three users. Defender for Cloud bases its suggestions on each user's control plane activity on the resource, its resource group, or the subscription. This feature speeds up fixes and strengthens your security posture.

Admins can assign the recommendation to the best user from the suggested list. That user gets a notification and a due date, so no one has to figure out who is responsible. This approach saves time for security teams.

## Prerequisites

Before you start, make sure you meet these requirements:

- [Enable the Defender for Cloud Security Posture Management (Defender CSPM) plan](tutorial-enable-cspm-plan).
- Make sure you have one of the following roles and permissions:

    - Security Administrator
    - Owner
    - Contributor
- [Review cloud availability](support-matrix-defender-for-cloud).

## Assign a recommendation

To assign a recommendation to an active user:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Defender for Cloud** &gt; **Recommendations**.
3. Review the **Recommendation owner** column.

    [![Screenshot that shows the Recommended owner column on the Recommendations page.](media/active-user/recommended-owner.png)](media/active-user/recommended-owner.png#lightbox)
4. Select a recommendation that has a suggested owner.
5. In the **Recommendation owner and set due date** section, find the top suggested active user for the resource.

    [![Screenshot that shows the top suggested active user on the resource.](media/active-user/suggested-user.png)](media/active-user/suggested-user.png#lightbox)
6. Select **Assign owner & set due date**.
7. Review the activity details and confidence of the top three suggested users.

    [![Screenshot that shows the activity and confidence of the top three suggested users.](media/active-user/select-active-user.png)](media/active-user/select-active-user-zoom.png#lightbox)
8. To view more information about the user, select **More info**. You can see a user's name, email address, manager, department, role, and last activities.
9. (Recommended) Select an owner from the list of suggested users.
10. (Optional) Select **Add a user manually** if you don't want to assign any of the suggested users.
11. (Optional) Select a remediation time frame.
12. (Optional) Turn on the **Apply grace period** toggle.
13. (Optional) Set email notifications.
14. Select **Create**.

If you set an email notification, the user gets an email. The email includes the recommendation details and a link to view it in Defender for Cloud.