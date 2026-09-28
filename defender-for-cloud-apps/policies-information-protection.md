---
layout: Conceptual
title: Commonly used information protection policies - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/policies-information-protection
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
description: This article outlines the steps to configure many information protection policies in Defender for Cloud Apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: MayaAbelson
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: a7fc18d5-6374-81d8-0663-e47a5d2d8887
document_version_independent_id: a7fc18d5-6374-81d8-0663-e47a5d2d8887
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/policies-information-protection.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: policies-information-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/policies-information-protection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 08946705-f0f3-5810-003f-950e82a419a3
---

# Commonly used information protection policies - Microsoft Defender for Cloud Apps | Microsoft Learn

Important

File policies retire on January 6, 2027. To maintain file-based data protection, [migrate to Microsoft Purview DLP or auto-labeling policies](migrate-file-policies-to-purview).

This article shows how to create and configure Defender for Cloud Apps file and session policies for common information protection scenarios. These scenarios include detecting external sharing of sensitive data, encrypting data at rest, blocking downloads, and more. Each scenario lists its own prerequisites, such as connected apps or Microsoft Purview Information Protection integration.

Defender for Cloud Apps can monitor any file type. It supports more than 20 metadata filters, such as access level and file type. Several of the policies in this article use the Data Classification Service (DCS), which inspects file content to identify sensitive information types. For more information, see [File policies](data-protection-policies#file-policy-reference).

## Detect and prevent external sharing of sensitive data

Detect when files with personally identifying information or other sensitive data are stored in a Cloud service and shared with users who are external to your organization that violates your company's security policy and creates a potential compliance breach.

Some of the policies in this section use the Data Classification Service (DCS) as the inspection method to identify sensitive information in your files.

### Prerequisites

You must have at least one app connected using [app connectors to connect apps](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

To create a file policy that detects externally shared sensitive data:

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **File policy**.
2. Set the filter **Access Level** equals **Public (Internet) / Public / External**.
3. Under **Inspection method**, select **Data Classification Service (DCS)**, and under **Select type** select the type of sensitive information you want DCS to inspect.
4. Configure the **Governance** actions to be taken when an alert is triggered. For example, you can create a governance action that runs on detected file violations in Google Workspace in which you select the option to **Remove external users** and **Remove public access**.
5. Create the file policy.

## Detect externally shared confidential data

Detect when files labeled **Confidential** in a cloud service are shared with external users. This sharing violates company policies.

### Prerequisites

- You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).
- Enable [Microsoft Purview Information Protection integration](azip-integration).

### Steps

To create a file policy that detects externally shared confidential data:

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **File policy**.
2. Set the filter **Sensitivity label** to **Microsoft Purview Information Protection**. Select the **Confidential** label, or your company's equivalent.
3. Set the filter **Access Level** equals **Public (Internet) / Public / External**.
4. Optional: Set the **Governance** actions for files when a violation is detected. The available actions vary between services.
5. Create the file policy.

## Detect and encrypt sensitive data at rest

Detect files that contain personal data or other sensitive data shared in a cloud app. Then apply sensitivity labels to limit access to employees in your company.

### Prerequisites

- You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).
- Enable [Microsoft Purview Information Protection integration](azip-integration).

### Steps

This policy uses the Data Classification Service (DCS), which inspects file content for sensitive information types.

Use the following steps to create the policy:

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **File policy**.
2. Under **Inspection method**, select **Data Classification Service (DCS)**. Under **Select type**, select the type of sensitive data you want DCS to inspect.
3. Under **Governance actions**, check **Apply sensitivity label**. Select the label your company uses to restrict access to employees.

    Note

    The ability to apply a sensitivity label directly in Defender for Cloud Apps is currently only supported for Box, Google Workspace, SharePoint online and OneDrive for Business.
4. Create the file policy.

## Detect data access from an unauthorized location

Detect when files are accessed from an unauthorized location, based on your organization's common locations, to identify a potential data leak or malicious access.

### Prerequisites

You must have at least one app connected using [app connectors to connect apps](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

To create the activity policy, perform the following steps:

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **Activity policy**.
2. Set the filter **Activity type** to the file and folder activities that interest you, such as **View**, **Download**, **Access**, and **Modify**.
3. Set the filter **Location** does not equal, and then enter the countries/regions from which your organization expects activity.

    - Optional: You can use the opposite approach and set the filter to **Location** equals if your organization blocks access from specific countries/regions.
4. Optional: Create **Governance** actions to be applied to detected violation (availability varies between services), such as **Suspend user**.
5. Create the Activity policy.

## Detect and protect confidential data store in a non-compliant SharePoint site

Detect files that are labeled as confidential and are stored in a non-compliant SharePoint site.

### Prerequisites

Sensitivity labels are configured and used inside the organization.

### Steps

Perform the following steps to detect and protect confidential data in a non-compliant SharePoint site:

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **File policy**.
2. Set the filter **Sensitivity label** to **Microsoft Purview Information Protection** equals the **Confidential** label, or your company's equivalent.
3. Set the filter **Parent folder** does not equal, and then under **Select a folder** choose all the compliant folders in your organization.
4. Under **Alerts** select **Create an alert for each matching file**.
5. Optional: Set the **Governance** actions to be taken on files when a violation is detected. The governance actions available vary between services. For example, Set **Box** to **Send policy-match digest to file owner** and **Put in admin quarantine**.
6. Create the file policy.

## Detect externally shared source code

Detect when files that contain content that might be source code are shared publicly or are shared with users outside of your organization.

### Prerequisites

You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

Use the following steps to create the policy from the template:

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **File policy**.
2. Select and apply the policy template **Externally shared source code**.
3. Optional: Customize the list of file **Extensions** to match your organization's source code file extensions.
4. Optional: Set the **Governance** actions to be taken on files when a violation is detected. The governance actions available vary between services. For example, in Box, **Send policy-match digest to file owner** and **Put in admin quarantine**.
5. Create the file policy.

## Detect unauthorized access to group data

Detect when certain files that belong to a specific user group are being accessed excessively by a user who is not part of the group, which could be a potential insider threat.

### Prerequisites

You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

Perform the following steps to detect unauthorized access to group data:

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **Activity policy**.
2. Under **Act on**, select **Repeated activity** and customize the **Minimum repeated activities** and set a **Timeframe** to comply with your organization's policy.
3. Set the filter **Activity type** to the file and folder activities that interest you, such as **View**, **Download**, **Access**, and **Modify**.
4. Set the filter **User** to **From group** equals and then select the relevant user groups.

    Note

    [User groups can be imported manually](user-groups) from supported apps.
5. Set the filter **Files and folders** to **Specific files or folders** equals and then choose the files and folders that belong to the audited user group.
6. Set the **Governance** actions to be taken on files when a violation is detected. The governance actions available vary between services. For example, you can choose to **Suspend user**.
7. Create the file policy.

## Detect publicly accessible S3 buckets

Detect and protect against potential data leaks from AWS S3 buckets.

### Prerequisites

You must have an AWS instance connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

Perform the following steps to detect publicly accessible S3 buckets:

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **File policy**.
2. Select and apply the policy template **Publicly accessible S3 buckets (AWS)**.
3. Set the **Governance** actions to be taken on files when a violation is detected. The governance actions available vary between services. For example, set AWS to **Make private** which would make the S3 buckets private.
4. Create the file policy.

## Detect and protect GDPR related data across file storage apps

Detect files in cloud storage apps that contain personal data or other sensitive data subject to GDPR. Then apply sensitivity labels to limit access to authorized personnel.

### Prerequisites

- You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).
- [Microsoft Purview Information Protection integration](azip-integration) is enabled and GDPR label is configured in Microsoft Purview

### Steps

Use the following steps to create the GDPR-related data protection policy:

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **File policy**.
2. Under **Inspection method**, select **Data Classification Service (DCS)**. Under **Select type**, select one or more GDPR-related information types. Examples include EU debit card number, EU drivers license number, EU national/regional identification number, EU passport number, EU SSN, and EU tax identification number.
3. Set the **Governance** actions for files when a violation is detected. Select **Apply sensitivity label** for each supported app.

    Note

    Currently, **Apply sensitivity label** is only supported for Box, Google Workspace, SharePoint online and OneDrive for business.
4. Create the file policy.

## Block downloads for external users in real time

Prevent company data from being exfiltrated by external users, by blocking file downloads in real time, using the Defender for Cloud Apps [session controls](proxy-intro-aad).

### Prerequisites

Make sure your app is a SAML-based app that uses Microsoft Entra ID for single sign-on, or is onboarded to Defender for Cloud Apps for Conditional Access app control.

For more information on supported apps, see [Supported apps and clients](proxy-intro-aad#supported-apps-and-clients).

### Steps

Perform the following steps to block downloads for external users in real time:

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **Session policy**.
2. Under **Session control type**, select **Control file download (with inspection)**.
3. Under **Activity filters**, select **User** and set it to **From group** equals **External users**.

    Note

    You don't need to set any app filters to enable this policy to apply to all apps.
4. You can use the **File filter** to customize the file type. This gives you more granular control over what type of files the session policy controls.
5. Under **Actions**, select **Block**. You can select **Customize block message** to set a custom message to be sent to your users so they understand the reason the content is blocked and how they can enable it by applying the right sensitivity label.
6. Select **Create**.

## Enforce read-only mode for external users in real time

Prevent company data from being exfiltrated by external users, by blocking print and copy/paste activities in real time, using the Defender for Cloud Apps [session controls](proxy-intro-aad).

### Prerequisites

Make sure your app is a SAML-based app that uses Microsoft Entra ID for single sign-on, or is onboarded to Defender for Cloud Apps for Conditional Access app control.

For more information on supported apps, see [Supported apps and clients](proxy-intro-aad#supported-apps-and-clients).

### Steps

Perform the following steps to enforce read-only mode for external users:

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **Session policy**.
2. Under **Session control type**, select **Block activities**.
3. In the **Activity source** filter:

    1. Select **User** and set **From group** to **External users**.
    2. Select **Activity type** equals **Print** and **Cut/copy item**.

    Note

    You don't need to set any app filters to enable this policy to apply to all apps.
4. Optional: Under **Inspection method**, select the type of inspection to apply and set the necessary conditions for the DLP scan.
5. Under **Actions**, select **Block**. You can select **Customize block message** to set a custom message to be sent to your users so they understand the reason the content is blocked and how they can enable it by applying the right sensitivity label.
6. Select **Create**.

## Block upload of unclassified documents in real time

Prevent users from uploading unprotected data to the cloud, by using the Defender for Cloud Apps [session controls](proxy-intro-aad).

### Prerequisites

- Make sure your app is a SAML-based app that uses Microsoft Entra ID for single sign-on, or is onboarded to Defender for Cloud Apps for Conditional Access app control.

For more information on supported apps, see [Supported apps and clients](proxy-intro-aad#supported-apps-and-clients).

- Sensitivity labels from Microsoft Purview Information Protection must be configured and used inside your organization.

### Steps

Use the following procedure to block uploads of unclassified documents in real time:

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **Session policy**.
2. Under **Session control type**, select **Control file upload (with inspection)** or **Control file download (with inspection)**.

    Note

    You don't need to set any filters to enable this policy to apply to all users and apps.
3. Select the file filter **Sensitivity label** does not equal and then select the labels your company uses to tag classified files.
4. Optional: Under **Inspection method**, select the type of inspection to apply and set the necessary conditions for the DLP scan.
5. Under **Actions**, select **Block**. You can select **Customize block message** to set a custom message to be sent to your users so they understand the reason the content is blocked and how they can enable it by applying the right sensitivity label.
6. Select **Create**.

Note

For the list of file types that Defender for Cloud Apps currently supports for sensitivity labels from Microsoft Purview Information Protection, see [Microsoft Purview Information Protection integration prerequisites](azip-integration#prerequisites).