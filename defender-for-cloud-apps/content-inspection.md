---
layout: Conceptual
title: DLP content inspection - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/content-inspection
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
description: This article describes the process Defender for Cloud Apps follows when performing DLP content inspection on data in your cloud.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: MayaAbelson
ms.custom: sfi-ga-blocked, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 975b1c39-4133-2ff8-379b-eb7196056f4d
document_version_independent_id: 975b1c39-4133-2ff8-379b-eb7196056f4d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/content-inspection.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: content-inspection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/content-inspection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/8b896464-3b7d-4e1f-84b0-9bb45aeb5f64
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1d2d671-9549-46e8-918c-24349120dbf5
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: b293db62-df36-59db-9884-60ddb4d15e97
---

# DLP content inspection - Microsoft Defender for Cloud Apps | Microsoft Learn

Important

File policies retire on January 6, 2027. To maintain file-based data protection, [migrate to Microsoft Purview DLP or auto-labeling policies](migrate-file-policies-to-purview).

Data loss prevention (DLP) in Microsoft Defender for Cloud Apps uses content inspection to detect sensitive information in files. When content inspection is enabled, Defender for Cloud Apps analyzes files for text patterns defined by expressions. Text that meets these expressions is treated as a match and can be used to determine a policy violation.

You can use preset or custom expressions and define a threshold for when a match constitutes a violation. For example, you can set a threshold of 10 to alert when a file contains at least 10 credit card numbers.

Matched text is replaced with "X" characters, and the surrounding context (100 characters before and after the match) is masked. Numbers in the context are replaced with "#" and aren't stored. To expose the final four digits of a match, enable the **Unmask the last four characters of a match** setting in the file policy.

You can also define which file elements are inspected—content, metadata, or file name. By default, inspection applies to both content and metadata. Inspecting both content and metadata by default allows inspection of protected files, detection of sensitive data, enforcement of compliance, and application of governance controls, while reducing false positives and aligning enforcement with internal classification standards.

## Prerequisites

To inspect encrypted files, and enable scanning of labels a [Global Administrator](/en-us/entra/identity/enterprise-apps/configure-admin-consent-workflow) must first grant one‑time admin consent to Defender for Cloud Apps in Microsoft Entra ID.

Note

Microsoft recommends that you use roles with the fewest permissions. This strategy helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

To grant one-time admin consent, in the Defender portal go to **Settings &gt; Cloud Apps &gt; Microsoft Information Protection &gt; Inspect protected files**, and select **Grant permission**.

## Content inspection for protected files

Once consent is granted, Defender for Cloud Apps provisions the Microsoft Cloud App Security (Internal) app in your tenant. The app uses the Azure Rights Management Services &gt; Content.SuperUser permission to decrypt and inspect protected files.

The following app IDs apply based on your Microsoft cloud environment:

**App IDs**

| Environment | App ID |
| --- | --- |
| Public | 25a6a87d-1e19-4c71-9cb0-16e88ff608f1 |
| Fairfax | bd5667e4-0484-4262-a9db-93faa0893899 |
| GCCM | 23105e90-1dfc-497a-bb5d-8b18a44ba061 |

Note

App IDs are internal service principals used by Defender for Cloud Apps in Public, Fairfax, and GCC‑M environments to inspect and enforce DLP policies on protected files. Don't remove or disable these App IDs. Doing so breaks inspection and prevent DLP policies from applying to protected files. Always verify that the App ID for your environment is present and enabled.

## Configure Microsoft Information Protection settings

In order to give Defender for Cloud Apps the necessary permissions:

1. Go to **Settings** &gt; **Microsoft Information Protection**.
2. Under **Microsoft Information Protection settings**, configure one or both of the following options:

    - **Automatically scan new files for Microsoft Information Protection sensitivity labels and content inspection warnings.** When enabled, the App connector scans new files for embedded sensitivity labels from Microsoft Information Protection.
    - **Only scan files for Microsoft Information Protection sensitivity labels and content inspection warnings from this tenant.** When enabled, only sensitivity labels applied within your tenant are scanned. Labels applied by external tenants are disregarded.
3. After selecting your options, select **Save** to apply your changes.

## Configure file policies for protected files

To configure a file policy that inspects protected files, complete the following steps:

1. In the Defender portal, go to **Settings &gt; Cloud Apps &gt; Policies &gt; Policy management**.
2. Follow the steps to [create a new file policy](data-protection-policies#create-a-new-file-policy).
3. Select either **Apply to all files**, or **Apply to selected files** to specify which files to scan. This option is useful if you have an inner classification keyword standard that you want to exclude from the policy.
4. Select **Inspection method** &gt; **Data Classification Service** to enable content inspection for the policy.
5. Check both boxes - **Inspect protected files** and **Unmask the last 4 characters of a match**.

    ![Screenshot that shows the Data classification service inspection method.](media/content-inspection/inspection-method-data-classification-service.png)