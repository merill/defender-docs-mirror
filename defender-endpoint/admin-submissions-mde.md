---
layout: Conceptual
title: Submit files in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/admin-submissions-mde
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to submit suspicious files and file hashes from Microsoft Defender for Endpoint to Microsoft for analysis using the unified submissions experience.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.topic: how-to
ms.collection:
- m365-security
- tier3
ms.custom: FPFN, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: de590c6c-dd28-bede-3d63-6c8bd46dbd73
document_version_independent_id: de590c6c-dd28-bede-3d63-6c8bd46dbd73
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/admin-submissions-mde.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: admin-submissions-mde
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/admin-submissions-mde.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: d92d7d7d-76fa-6fc5-5652-e2c6f85d036c
---

# Submit files in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

In Microsoft Defender for Endpoint, admins can use the unified submissions feature to submit files and file hashes (SHAs) to Microsoft for review. The unified submissions experience is a one-stop shop for submitting emails, URLs, email attachments, and files in one, easy-to-use submission experience. Admins can use the Microsoft Defender portal or the Microsoft Defender for Endpoint Alert page to submit suspicious files.

## What do you need to know before you begin?

The new unified submissions experience is available in subscriptions that include Microsoft Defender XDR or Microsoft Defender for Endpoint Plan 2. You need to assign permissions before you can perform the procedures in this article. Use one of the following options:

**Microsoft Defender for Endpoint** permissions:

- Submit files / file hashes: *"Alerts investigation" or "Manage security settings in Security Center"*
- View submissions: "*View Data - Security operations"*

**Microsoft Defender unified RBAC** permissions:

- Submit files / file hashes: *"Alerts (Manage)" or "Core security settings (manage)"*
- View submissions: *"Security data basics (read)"*

For more information about how you can submit spam, phish, URLs, and email attachments to Microsoft, see [Use the Submissions page to submit suspected spam, phish, URLs, legitimate email getting blocked, and email attachments to Microsoft](/en-us/defender-office-365/submissions-admin).

## Submit a file or file hash to Microsoft from the Defender portal

Use the following steps to submit a file or file hash to Microsoft from the Submissions page in the Defender portal.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Investigation & response** &gt; **Actions & submissions** &gt; **Submissions**. Or, to go directly to the **Submissions** page, use https://security.microsoft.com/reportsubmission.
2. On the **Submissions** page, select the **Files** tab.
3. On the **Files** tab, select ![](media/defender-portal-icon-create.png)**Add new submission**.
4. ![Screenshot showing how to add a new submission.](/en-us/defender/media/unified-admin-submission-new.png)
5. In the **Submit items to Microsoft for review** flyout that opens, select **Files** or **File hash** from the **Select the submission type** dropdown list.

    - If you selected **Files**, configure the following options:

        - Select **Browse files**. In the dialog that opens, find and select the file, and then select **Open**. Repeat this step as many times as necessary. To remove an entry from the flyout, select ![](media/defender-portal-icon-close.png)next to the entry.
            - The maximum total size of all files is 500 MB.
            - Use the password 'infected' to encrypt archive files.
        - **The file should have been categorized as**: Select one of the following values:
            - **Malware** (false negative)
            - **Unwanted software**
            - **Clean** (false positive)
        - **Choose the priority**: Select one of the following values:
            - **Low - bulk file or file hash submission**
            - **Medium - standard submission**
            - **High - needs immediate attention** (max three per day)
        - **Notes for Microsoft (optional)**: Enter an optional note.
        - **Share feedback and relevant content with Microsoft**: Read the privacy statement and then select this option.

        ![Screenshot showing how to submit files.](/en-us/defender/media/unified-admin-submission-file.png)
    - If you selected **File hash**, configure the following options:

        - In the empty box, enter the file hash value (for example, `2725eb73741e23a254404cc6b5a54d9511b9923be2045056075542ca1bfbf3fe`) and then press the ENTER key. Repeat this step as many times as necessary. To remove an entry from the flyout, select ![](media/defender-portal-icon-close.png) next to the entry.
        - **The file should have been categorized as**: Select one of the following values:
            - **Malware** (false negative)
            - **Unwanted software**
            - **Clean** (false positive)
        - **Notes for Microsoft (optional)**: Enter an optional note.
        - **Share feedback and relevant content with Microsoft**: Read the privacy statement and then select this option.

        ![Screenshot showing how to submit files hashes.](/en-us/defender/media/unified-admin-submission-file-hash.png)

    When you're finished in the **Submit items to Microsoft for review** flyout, select **Submit**.

Back on the **Files** tab of the **Submissions** page, the submission is shown.

To view the details of the submission, select the submission by clicking anywhere in the row other than the check box next to the **Submission name**. The details of the submission are in the details flyout that opens.

## Report items to Microsoft from the Alerts page in the Defender portal

Use the following steps to report items to Microsoft from the Alerts page in the Defender portal.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Investigation & response** &gt; **Incidents & alerts** &gt; **Alerts**. Or, to go directly to the **Alerts** page, use https://security.microsoft.com/alerts.
2. On the **Alerts** page, find the alert that contains the file you want to report. For example, you can select ![](media/defender-portal-icon-filter.png)**Filter**, and then select **Service/detection sources** &gt; **Microsoft Defender for Endpoint**.
3. Select the alert from the list by clicking anywhere in the row other than the check box next to the **Alert name** value.
4. In the details flyout that opens, select ![](media/defender-portal-icon-more-actions.png) &gt; **Submit items to Microsoft for review**.

    a. ![Screenshot showing how to submit items from an alerts queue.](/en-us/defender/media/unified-admin-submission-alerts-queue.png)
5. The options that are available in the **Submit items to Microsoft for review** flyout that opens are the same as described in Submit a file or file hash to Microsoft from the Defender portal.

    The only difference is an **Include alert story** option that you can select to attach a JSON file that helps Microsoft investigate the submission.

    ![Screenshot showing how to specify a submission type and fill in required fields.](/en-us/defender/media/unified-admin-submission-alert-queue-flyout.png)

    When you're finished in the **Submit items to Microsoft for review** flyout, select **Submit**.

The submission is available on the **Files** tab of the **Submissions** page at https://security.microsoft.com/reportsubmission?viewid=file.