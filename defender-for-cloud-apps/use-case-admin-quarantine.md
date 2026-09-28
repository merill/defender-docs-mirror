---
layout: Conceptual
title: Protect files with admin quarantine - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/use-case-admin-quarantine
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
description: This tutorial describes the scenario for using admin quarantine to control data breaches.
ms.date: 2025-08-20T00:00:00.0000000Z
ms.topic: tutorial
ms.reviewer: MayaAbelson
locale: en-us
document_id: 07d6d03d-c5a4-124e-81c4-de89c4f7708c
document_version_independent_id: 07d6d03d-c5a4-124e-81c4-de89c4f7708c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/use-case-admin-quarantine.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: use-case-admin-quarantine
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/use-case-admin-quarantine.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
platformId: 92fa3bf3-7500-0822-e7d8-0e7030d7d68e
---

# Protect files with admin quarantine - Microsoft Defender for Cloud Apps | Microsoft Learn

Important

File policies retire on January 6, 2027. To maintain file-based data protection, [migrate to Microsoft Purview DLP or auto-labeling policies](migrate-file-policies-to-purview).

[File policies](data-protection-policies) are a great tool for finding threats to your information protection policies. For instance, create file policies that find places where users stored sensitive information, credit card numbers, and third-party ICAP files in your cloud.

In this tutorial, you'll learn how to use Microsoft Defender for Cloud Apps to detect unwanted files stored in your cloud that leave you vulnerable, and take immediate action to stop them in their tracks and lock down the files that pose a threat by using **Admin quarantine** to protect your files in the cloud, remediate problems, and prevent future leaks from occurring.

- Understand how quarantine works
- Set up admin quarantine

## Understand how quarantine works

Note

- For a list of apps that support admin quarantine, see the list of [governance actions](governance-actions).
- Files labeled by Defender for Cloud Apps can't be quarantined.
- Defender for Cloud Apps admin quarantine actions is limited to 100 actions per day.
- Sharepoint sites that are renamed either directly or as part of domain rename can't be used as a folder location for admin quarantine.

1. When a file matches a policy, the **Admin quarantine** option is available for the file.
2. Set an automated quarantine action in the policy.

    [![quarantine automatically.](media/quarantine-automated.png)](media/quarantine-automated.png#lightbox)
3. When **Admin quarantine** is applied, the following things occur behind the scenes:

    1. The original file is moved to the admin quarantine folder you set.
    2. The original file is deleted.
    3. A tombstone file is uploaded to the original file location.

        ![quarantine tombstone.](media/quarantine-tombstone.png)
    4. The user can only access the tombstone file. In the file, they can read the custom guidelines provided by IT and the correlation ID to give IT to release the file.
4. When you receive the alert that a file has been quarantined, go to **Policies** -&gt; **Policy Management**. Then select the **Information Protection** tab. In the row with your file policy, choose the three dots at the end of the line, and select **View all matches**. This brings you the report of matches, where you can see the matching and quarantined files:

    [![Quarantined files.](media/quarantine-alerts.png)](media/quarantine-alerts.png#lightbox)
5. After a file is quarantined, use the following process to remediate the threat situation:

    1. Inspect the file in the quarantined folder on SharePoint online.
    2. You can also look at the audit logs to deep dive into the file properties.
    3. If you find the file is against corporate policy, run the organization's Incident Response (IR) process.
    4. If you find that the file is harmless, you can restore the file from quarantine. At that point the original file is released, and copied back to the original location. The tombstone is deleted, and the user can access the file.

        ![quarantine restore.](media/quarantine-restore.png)
6. Validate that the policy runs smoothly. Then, you can use the automatic governance actions in the policy to prevent further leaks and automatically apply an Admin quarantine when the policy is matched.

Note

When you restore a file:

- Original shares aren't restored, default folder inheritance applied.
- The restored file contains only the most recent version.
- The quarantine folder site access management is the customer's responsibility.

## Set up admin quarantine

1. Set file policies that detect breaches. Examples of these types of policies include:

    - A metadata only policy such as a sensitivity label in SharePoint Online
    - A native data loss prevention (DLP) policy such as a policy that searches for credit card numbers
    - An ICAP third-party policy such as a policy that looks for Vontu
2. Set a quarantine location:

    1. For Microsoft 365 SharePoint or OneDrive for Business, you can't put files in admin quarantine as part of a policy until you set it up:

        ![quarantine warning.](media/quarantine-warning.png)

        To set admin quarantine settings, in the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Information Protection**, choose **Admin quarantine**. Provide a site for the quarantine folder location and a user notification that your user will receive when their file is quarantined.

        [![quarantine settings.](media/quarantine-settings.png)](media/quarantine-settings.png#lightbox)

        Note

        Defender for Cloud Apps creates a quarantine folder on the selected site.
    2. For Box, the quarantine folder location and user message can't be customized. The folder location is the drive of the admin who connected Box to Defender for Cloud Apps and the user message is: This file was quarantined to your administrator's drive because it might violate your company's security and compliance policies. Contact your IT administrator for help.