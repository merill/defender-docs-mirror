---
layout: Conceptual
title: Discover and protect sensitive information in your organization - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/tutorial-dlp
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
description: This tutorial describes the process to discover and protect sensitive information in Microsoft Defender for Cloud Apps.
ms.date: 2024-05-15T00:00:00.0000000Z
ms.topic: tutorial
ms.reviewer: MayaAbelson
locale: en-us
document_id: 2e493f4e-7835-642a-d337-abb9ae2479bb
document_version_independent_id: 2e493f4e-7835-642a-d337-abb9ae2479bb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/tutorial-dlp.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tutorial-dlp
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/tutorial-dlp.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: a45125d1-48ba-de60-22a0-cbc6dbfe0305
---

# Discover and protect sensitive information in your organization - Microsoft Defender for Cloud Apps | Microsoft Learn

Important

File policies retire on January 6, 2027. To maintain file-based data protection, [migrate to Microsoft Purview DLP or auto-labeling policies](migrate-file-policies-to-purview).

In a perfect world, all your employees understand the importance of information protection and work within your policies. In the real world, it's likely that a busy partner who frequently works with accounting information will inadvertently upload a sensitive document to your Box repository with incorrect permissions. A week later you realize your enterprise's confidential information was leaked to your competition.

To help you prevent this from happening, Microsoft Defender for Cloud Apps provides you with an expansive suite of DLP capabilities that cover the various data leak points that exist in organizations.

In this tutorial, you'll learn how to use Defender for Cloud Apps to discover potentially exposed sensitive data and apply controls to prevent their exposure:

- Discover your data
- Classify sensitive information
- Protect your data
- Monitor and report on your data

## How to discover and protect sensitive information in your organization

Our approach to information protection can be split into the following phases that allow you to protect your data through its full lifecycle, across multiple locations and devices.

![shadow IT lifecycle.](media/tutorial-dlp-solution.png)

### Phase 1: Discover your data

1. **Connect apps**: The first step in discovering which data is being used in your organization, is to connect cloud apps used in your organization to Defender for Cloud Apps. Once connected, Defender for Cloud Apps can scan data, add classifications, and enforce policies and controls. Depending on how apps are connected affects how, and when, scans and controls are applied. You can connect your apps in one of the following ways:

    - **Use an app connector**: Our app connectors use the APIs supplied by app providers. They provide greater visibility into and control over the apps used in your organization. Scans are performed periodically (every 12 hours) and in real time (triggered each time a change is detected). For more information and instructions on how to add apps, see [Connecting apps](enable-instant-visibility-protection-and-governance-actions-for-your-apps).
    - **Use conditional access app control**: Our Conditional Access app control solution uses a reverse proxy architecture that is uniquely integrated with Microsoft Entra Conditional Access, and allows you to apply controls to any app.

        Microsoft Edge users benefit from direct, in-browser protection. Conditional Access app control is applied in other browsers using a reverse proxy architecture. For more information, see [Protect apps with Microsoft Defender for Cloud Apps Conditional Access app control](proxy-intro-aad) and [In-browser protection with Microsoft Edge for Business (Preview)](in-browser-protection).
2. **Investigate**: After you connect an app to Defender for Cloud Apps using its API connector, Defender for Cloud Apps scans all the files it uses. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Files** to get an overview of the files shared by your cloud apps, their accessibility, and their status. For more information, see [Investigate files](file-filters).

### Phase 2: Classify sensitive information

1. **Define which information is sensitive**: Before looking for sensitive information in your files, you first need to define what counts as sensitive for your organization. As part of our [data classification service](dcs-inspection), we offer over 100 out-of-the-box sensitive information types, or you can [create your own](/en-us/microsoft-365/compliance/create-a-custom-sensitive-information-type) to suit to your company policy. **Defender for Cloud Apps is natively integrated with Microsoft Purview Information Protection** and the same sensitive types and labels are available throughout both services. So when you want to define sensitive information, head over to the Microsoft Purview Information Protection portal to create them, and once defined they'll be available in Defender for Cloud Apps. You can also use advanced classifications types such as fingerprint or Exact Data Match (EDM).

    For those of you that have already done the hard work of identifying sensitive information and applying the appropriate sensitivity labels, you can use those labels in your policies without having to scan the contents again.
2. **Enable Microsoft Information Protection integration**

    1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
    2. Under **Information Protection**, go to **Microsoft Information Protection**. Select **Automatically scan new files for Microsoft Information Protection sensitivity labels and content inspection warnings**.

    For more information, see [Microsoft Purview Information Protection integration](azip-integration).
3. **Create policies to identify sensitive information in files**: Once you know the kinds of information you want to protect, it's time to create policies to detect them. Start by creating the following policies:

    **File policy** Use this type of policy to scan the content of files stored in your API connected cloud apps in near real-time and data at rest. Files are scanned using one of our supported inspection methods including **Microsoft Purview Information Protection encrypted content** thanks to its **native integration** with Defender for Cloud Apps.

    1. In the Microsoft Defender Portal, under **Cloud Apps**, select **Policies** -&gt; **Policy management**.
    2. Select **Create Policy**, and then select **File policy**.
    3. Under **Inspection method**, choose and configure one of the following classification services:

        - **[Data Classification Services](dcs-inspection)**: Uses classification decisions you've made across Microsoft 365, Microsoft Purview Information Protection, and Defender for Cloud Apps to provide a unified labeling experience. This is the preferred content inspection method as it provides a consistent and unified experience across Microsoft products.
    4. For highly sensitive files, select **Create an alert for each matching file** and choose the alerts you require, so that you're informed when there are files with unprotected sensitive information in your organization.
    5. Select **Create**.

    **Session policy** Use this type of policy to scan and protect files in real time on access to:

    - **Prevent data exfiltration**: Block the download, cut, copy, and print of sensitive documents on, for example, unmanaged devices.
    - **Protect files on download**: Require documents to be labeled and protected with Microsoft Purview Information Protection. This action ensures the document is protected and user access is restricted in a potentially risky session.
    - **Prevent the upload of unlabeled files**: Require a file to have the right label and protection before a sensitive file is uploaded, distributed, and used by others. With this action, you can ensure that unlabeled files with sensitive content are blocked from being uploaded until the user classifies the content.

    1. In the Microsoft Defender Portal, under **Cloud Apps**, select **Policies** -&gt; **Policy management**.
    2. Select **Create Policy**, and then select **Session policy**.
    3. Under **Session control type**, choose one of the options with DLP.
    4. Under **Inspection method**, choose and configure one of the following classification services:

        - **[Data Classification Services](dcs-inspection)**: Uses classification decisions you've made across Microsoft 365, Microsoft Purview Information Protection, and Defender for Cloud Apps to provide a unified labeling experience. This is the preferred content inspection method as it provides a consistent and unified experience across Microsoft products.
    5. For highly sensitive files, select **Create an alert** and choose the alerts you require, so that you're informed when there are files with unprotected sensitive information in your organization.
    6. Select **Create**.

You should create as many policies as required to detect sensitive data in compliance with your company policy.

### Phase 3: Protect your data

So now you can detect files with sensitive information, but what you really want to do is protect that information from potential threats. Once you're aware of an incident, you can manually remediate the situation or you can use one of the automatic governance actions provided by Defender for Cloud Apps for securing your files. Actions include, but aren't limited to, Microsoft Purview Information Protection native controls, API provided actions, and real-time monitoring. The kind of governance you can apply depends on the type of policy you're configuring, as follows:

1. **[File policy governance](governance-actions#file-governance-actions) actions**: Uses the cloud app provider's API and our native integrations to secure files, including:

    - Trigger alerts and send email notifications about the incident
    - Manage labels applied to a file to enforce native Microsoft Purview Information Protection controls
    - Change sharing access to a file
    - Quarantine a file
    - Remove specific file or folder permissions in Microsoft 365
    - Move a file to the trash folder
2. **Session policy controls**: Uses reverse proxy capabilities to protect files, such as:

    - Trigger alerts and send email notifications about the incident
    - Explicitly allowing the download or upload of files and monitors all related activities.
    - Explicitly block the download or upload of files. Use this option to protect your organization's sensitive files from exfiltration or infiltration from any device, including unmanaged devices.
    - Automatically apply a sensitivity label to files that match the policy's file filters. Use this option to protect the download of sensitive files.

    For more information, see [Create Microsoft Defender for Cloud Apps session policies](session-policy-aad).

### Phase 4: Monitor and report on your data

Your policies are all in place to inspect and protect your data. Now, you'll want to [check your dashboard](daily-activities-to-protect-your-cloud-environment#check-the-dashboard) daily to see what new alerts have been triggered. It's a good place to keep an eye on the health of your cloud environment. Your dashboard helps you get a sense of what's happening and, if necessary, launch an [investigation](investigate).

One of the most effective ways of monitoring sensitive file incidents, is to head over to the **Policies** page, and review the matches for policies you've configured. Additionally, if you configured alerts, you should also consider regularly monitoring file alerts by heading over to the **Alerts** page, specifying the category as **DLP**, and reviewing which file-related policies are being triggered. Reviewing these incidents can help you fine-tune your policies to focus on threats that are of interest to your organization.

In conclusion, managing sensitive information in this way ensures that data saved to the cloud has maximal protection from malicious exfiltration and infiltration. Also, if a file is shared or lost, it can only be accessed by authorized users.