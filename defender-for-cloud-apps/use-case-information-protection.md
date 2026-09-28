---
layout: Conceptual
title: Automatically apply sensitivity labels from Microsoft Purview Information Protection - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/use-case-information-protection
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
description: This tutorial describes how to automatically apply sensitivity labels from Microsoft Purview Information Protection in Microsoft Defender for Cloud Apps.
ms.date: 2023-08-08T00:00:00.0000000Z
ms.topic: tutorial
ms.reviewer: MayaAbelson
locale: en-us
document_id: 7c530975-8bbd-3553-bcd2-8cc4b04e54a5
document_version_independent_id: 7c530975-8bbd-3553-bcd2-8cc4b04e54a5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/use-case-information-protection.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: use-case-information-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/use-case-information-protection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://authoring-docs-microsoft.poolparty.biz/devrel/7428317a-e6c2-4461-ad3e-8a8ad3608734
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://authoring-docs-microsoft.poolparty.biz/devrel/e4f59707-f107-48f2-8d75-0afd91868cd7
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: 9d0a1399-7067-90a0-afe5-9f3269c33408
---

# Automatically apply sensitivity labels from Microsoft Purview Information Protection - Microsoft Defender for Cloud Apps | Microsoft Learn

Important

File policies retire on January 6, 2027. To maintain file-based data protection, [migrate to Microsoft Purview DLP or auto-labeling policies](migrate-file-policies-to-purview).

In a perfect world, all your employees understand the importance of information protection and work within your policies. But in a real world, it's probable a partner who works with accounting uploads a document to your OneDrive for Business repository with the wrong permissions. A week later you realize your enterprise's confidential information was leaked to your competition. Microsoft Defender for Cloud Apps helps you prevent this kind of disaster before it happens. This feature is available for Box, SharePoint and OneDrive for Business. Applying a sensitivity label is one of a long list of available [governance actions](governance-actions).

In this tutorial, you'll learn how to identify which public permissions are set on a document that's saved in your cloud storage, so you're alerted when a breach occurs. In addition, you can automatically apply your Microsoft Purview Information Protection **Confidential** sensitivity label to provide added encryption to files.

- Set up data protection
- Validate your policy

## Enhanced data-level encryption protection

Defender for Cloud Apps integration with Microsoft Purview Information Protection enables an added level of protection by automatically encrypting files. When Microsoft Purview Information Protection encrypts files, applications that support Microsoft Purview Information Protection like Microsoft 365, know how to open the files and honors permissions set in the sensitivity labels. Use labels to apply specific protection rules. For example, set a file that can be opened but not shared, printed, forwarded, or edited.

This strong level of protection travels with the file. The file is still protected if you send the file, copy it, or store it in your online storage app. If one of your employees loses a thumb drive with the file on it, the file will be locked. Should someone try to open the file, the file owner will receive an alert. With Defender for Cloud Apps, you can apply protection automatically. For example, set all files that have credit card numbers, or were uploaded by the finance department and are shared externally, to be automatically protected with a sensitivity label.

## The threat

A user in your organization saves confidential customer information files to OneDrive for Business and sets it to be shared with everyone in the organization. The user doesn't realize that not only their immediate team, but the entire support staff has access to that OneDrive for Business account. This access includes vendors, partners, and visitors who occasionally stop into the office. Any person with access to your organization's OneDrive for Business account now has access to that information. Not only can that access be dangerous for your organization, it can be against personal information regulations in many countries/regions, causing potential legal issues.

## The solution

Use Defender for Cloud Apps with Microsoft Purview Information Protection to embed classification and protection information for persistent protection that follows your data — so it stays protected no matter where it's stored or who it's shared with. This protection enables you to share data safely with coworkers, customers, and partners. Define who can access data and what they can do with it. For instance, allow users to view and edit files but not print or forward. You can also add other [governance actions](governance-actions) supported by Defender for Cloud Apps to the files such as remove collaborators and remove sharing abilities.

## Prerequisites

- [Enable Defender for Cloud Apps and Microsoft Purview Information Protection](azip-integration) for your tenant.

## Set up data protection

Let's set up a policy that looks for credit card numbers in files stored in your OneDrive for Business account. When files are found, automatically apply a sensitivity label and control what happens to all files with that label.

1. Start protecting the data you store in OneDrive for Business by setting up a policy that will encrypt any sensitive data stored in a specific OneDrive for Business folder:

    1. In the Microsoft Defender Portal, under **Cloud Apps**, select [**Policies**](control-cloud-apps-with-policies) -&gt; **Policy management**.
    2. Select **Create policy** &gt; **File policy**.
    3. On the **Create file policy** page, enter *OneDrive data protection* in the **Policy name** box.
    4. In the **Files matching all of the following** area, create a filter to target your proprietary and sensitive data. For example:

        1. Select **Add a filter** and then select the **Select a filter** option &gt; **Parent folder** &gt; **equals** &gt; **Select a folder**.
        2. In the **Select a folder** dialog, select a folder to watch, such as **Sales West**, and then select **Done**.
        3. Select **Add a filter** again and then select **Collaborators** &gt; **Groups** &gt; **contains** &gt; **Finance**
    5. Define the inspection method to look for files containing credit card information:

        1. From the **Inspection method** dropdown, select **Data Classification Service**.
        2. Select **Choose inspection type** &gt; **Sensitive information type** &gt; **Credit Card Number** &gt; **Done**. When selecting your sensitive information type, enter **credit** in the **Search** box and press **ENTER** to filter the types listed.
    6. In the **Governance actions** area, expand the **Microsoft OneDrive for Business** dropdown, and select **Apply sensitivity label**. Select the label you want to apply, such as **Confidential - Finance**.

        [Defender for Cloud Apps is integrated with Microsoft Purview Information Protection](azip-integration), which allows you to select from your existing list of sensitivity labels to be used to protect the data.
    7. Select **Create**.

## Investigate your matches

After setting up your policy to watch for credit card information in the selected folder, do the following to investigate any matches found:

1. In the Microsoft Defender XDR **Cloud apps** navigation menu, select **Policies &gt; Policy management**.
2. Select the policy you'd created earlier and then select **View policy matches**.
3. Review the matches that were triggered for the policy. Select any specific file to expand for more details, including any other policies matched by the selected file.

## Validate your policy

1. To simulate an alert, create a file with a simulated credit card number in the OneDrive for Business folder you'd defined in your policy.
2. Go to the policy report, where a new match should appear shortly.
3. You can select the match to see which files were protected. The match itself will be masked to protect the sensitive data.

Note

- Defender for Cloud Apps currently supports automatic application of sensitivity labels on Box, GSuite, SharePoint and OneDrive for business.
- When a document is labeled by Defender for Cloud Apps, visual markings, such as headers, footers, or watermarks, are not applied. For more information, see [Learn about sensitivity labels](/en-us/microsoft-365/compliance/sensitivity-labels).