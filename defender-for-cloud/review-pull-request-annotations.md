---
layout: Conceptual
title: Review Pull Request Annotations in GitHub and Azure DevOps - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/review-pull-request-annotations
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
description: Learn how to review and act on Defender for Cloud pull request annotations in GitHub and Azure DevOps to identify and resolve security issues.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: ea5eaea0-47a7-b8c6-140c-c3a9726cabf1
document_version_independent_id: 39e0e576-1c43-24db-5766-9295dfd067ff
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/review-pull-request-annotations.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/review-pull-request-annotations
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/review-pull-request-annotations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://authoring-docs-microsoft.poolparty.biz/devrel/5bd2b3fa-c186-4b92-a3c8-09f22a249d37
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/7eba7926-b7b2-4a7a-bf89-e6ac53b3e7f6
platformId: 836be7eb-4d48-efcb-64e7-0c2a469edd77
---

# Review Pull Request Annotations in GitHub and Azure DevOps - Microsoft Defender for Cloud | Microsoft Learn

You can review and act on Defender for Cloud pull request annotations in GitHub and Azure DevOps. Use these annotations to resolve security issues before you merge code.

## Resolve security issues in GitHub

**To resolve security issues in GitHub**:

1. Scroll through the pull request page to find an affected file with an annotation.
2. Follow the remediation steps in the annotation. If you choose not to remediate the annotation, select **Dismiss alert**.
3. Select a reason to dismiss:

    - **Won't fix**: The alert is noted but won't be fixed.
    - **False positive**: The alert isn't valid.
    - **Used in tests**: The alert isn't in the production code.

## Resolve security issues in Azure DevOps

After you configure Defender for Cloud pull request annotations, you can view all detected issues.

**To resolve security issues in Azure DevOps**:

1. Sign in to [Azure DevOps](https://azure.microsoft.com/products/devops).
2. Go to **Pull requests** and select a pull request.

    ![Screenshot showing where to go to navigate to pull requests.](media/tutorial-enable-pr-annotations/pull-requests.png)
3. Select **Files** and find an affected line with an annotation.
4. Follow the remediation steps in the annotation.
5. Select **Active** to change the status of the annotation and access the dropdown menu.
6. Select an action to take:

    - **Active**: The default status for new annotations.
    - **Pending**: The finding is being worked on.
    - **Resolved**: The finding is addressed.
    - **Won't fix**: The finding is noted but won't be fixed.
    - **Closed**: The discussion in this annotation is closed.

DevOps security in Defender for Cloud reactivates an annotation if the security issue isn't fixed in a new iteration.