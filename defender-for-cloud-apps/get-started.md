---
layout: Conceptual
title: Get started - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/get-started
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
description: This quickstart outlines the process for getting Defender for Cloud Apps up and running so you have cloud app use, insight, and control.
ms.date: 2025-07-24T00:00:00.0000000Z
ms.topic: quickstart
ms.custom: sfi-image-nochange
locale: en-us
document_id: 6dda3bb3-f0b8-9f4b-b027-becd2d5a0392
document_version_independent_id: 6dda3bb3-f0b8-9f4b-b027-becd2d5a0392
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/get-started.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: get-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/get-started.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 31d50837-4c6b-ef07-8dd4-f75107ef68a8
---

# Get started - Microsoft Defender for Cloud Apps | Microsoft Learn

This quickstart describes how to start working with Microsoft Defender for Cloud Apps on the Microsoft Defender Portal.

Defender for Cloud Apps can help you use the benefits of cloud applications while maintaining control of your corporate resources. Defender for Cloud Apps improves your visibility into cloud activity and helps increase protection over your corporate data.

Tip

As a companion to this article, we recommend using the [Microsoft Defender for Cloud Apps automated setup guide](https://go.microsoft.com/fwlink/?linkid=2251562) when signed in to the Microsoft 365 admin center. This guide will customize your experience based on your environment. To review best practices without signing in and activating automated setup features, go to the Microsoft 365 setup portal.

## Prerequisites

To set up Defender for Cloud Apps, you must at least be a Security Administrator in Microsoft Entra ID or Microsoft 365.

Users with admin roles have the same admin permissions across any cloud apps your organization is subscribed to, regardless of where you've assigned the role. For more information, see [Assign admin roles](/en-us/microsoft-365/admin/add-users/assign-admin-roles) and [Assigning administrator roles in Microsoft Entra ID](/en-us/azure/active-directory/roles/permissions-reference).

Microsoft Defender for Cloud Apps is a security tool and therefore doesn't require Microsoft 365 productivity suite licenses. For Microsoft 365 Cloud App Security (Microsoft Defender for Cloud Apps only for Microsoft 365), see [What are the differences between Microsoft Defender for Cloud Apps and Microsoft 365 Cloud App Security?](editions-cloud-app-security-o365).

Microsoft Defender for Cloud Apps depends on the following Microsoft Entra ID applications to function properly. Do not disable these applications in Microsoft Entra ID:

- Microsoft Defender for Cloud Apps - APIs (or API Connectors (1st Party)) (ID: 972bb84a-1d27-4bd3-8306-6b8e57679e8c)
- Microsoft Defender for Cloud Apps - Customer Experience (ID: ac6dbf5e-1087-4434-beb2-0ebf7bd1b883)
- Microsoft Defender for Cloud Apps - Information Protection (ID: 9ba4f733-be8f-4112-9c4a-e3b417c44e7d)
- Microsoft Defender for Cloud Apps - MIP Server (ID: 0858ddce-8fca-4479-929b-4504feeed95e)
- Microsoft Defender for Cloud Apps - Data Loss Prevention - SPO (ID: 71559765-2fa9-4207-b59f-a8bd85269d4a)

## Access Defender for Cloud Apps

1. Obtain a Defender for Cloud Apps license for each user you want protected by Defender for Cloud Apps. For more information, see the [Microsoft 365 licensing datasheet](https://aka.ms/M365EnterprisePlans).

    A Defender for Cloud Apps trial is available as part of a Microsoft 365 E5 trial, and you can purchase licenses from the Microsoft 365 admin center &gt; **Marketplace**. For more information, see [Try or buy Microsoft 365](/en-us/microsoft-365/commerce/try-or-buy-microsoft-365) or [Get support for Microsoft 365 for business](/en-us/microsoft-365/admin/get-help-support).

    Note

    Microsoft Defender for Cloud Apps is a security tool and therefore doesn't require Microsoft 365 productivity suite licenses. For more information, see [What are the differences between Microsoft Defender for Cloud Apps and Microsoft 365 Cloud App Security?](editions-cloud-app-security-o365).
2. Access Defender for Cloud Apps on the **[Microsoft Defender Portal](https://security.microsoft.com)** under **Cloud Apps**. For example:

    [![Screenshot of the Defender for Cloud Apps Cloud Discovery page.](media/get-started/defender-for-cloud-apps-intro.png)](media/get-started/defender-for-cloud-apps-intro.png#lightbox)

## Step 1: Set instant visibility, protection, and governance actions for your apps

**How to page**: [Set instant visibility, protection, and governance actions for your apps](enable-instant-visibility-protection-and-governance-actions-for-your-apps)

**Required task**: Connect apps

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **Connected Apps**, select **App Connectors**.
3. Select the **+Connect an app** to add an app and then select an app.
4. Follow the configuration steps to connect the app.

**Why connect an app?** After you connect an app, you can gain deeper visibility so you can investigate activities, files, and accounts for the apps in your cloud environment.

## Step 2: Protect sensitive information with DLP policies

**How to page**: [Protect sensitive information with DLP policies](policies-information-protection)

**Recommended tasks**

- Enable file monitoring and create file policies

Important

File policies retire on January 6, 2027. To maintain file-based data protection, [migrate to Microsoft Purview DLP or auto-labeling policies](migrate-file-policies-to-purview).

- To enable File monitoring of Microsoft 365 files, you are required to use a relevant Entra Admin ID, such as Application Administrator or Cloud Application Administrator. For more details, see [Microsoft Entra built-in roles](/en-us/entra/identity/role-based-access-control/permissions-reference).

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **Information Protection**, select **Files**.
3. Select **Enable file monitoring** and then select **Save**.
4. If you use sensitivity labels from Microsoft Purview Information Protection, under **Information Protection**, select **Microsoft Information Protection**.
5. Select the required settings and then select **Save**.
6. In Step 3, create [File policies](data-protection-policies) to meet your organizational requirements.

**Migration recommendation** We recommend using Defender for Cloud Apps sensitive information protection in parallel with your current Cloud Access Security Broker (CASB) solution. Start by [connecting the apps you want to protect](enable-instant-visibility-protection-and-governance-actions-for-your-apps) to Microsoft Defender for Cloud Apps. Since API connectors use out-of-band connectivity, no conflict will occur. Then progressively migrate your [policies](control-cloud-apps-with-policies) from your current CASB solution to Defender for Cloud Apps.

Note

For third-party apps, verify that the current load does not exceed the app's maximum number of allowed API calls.

## Step 3: Control cloud apps with policies

**How to page**: [Control cloud apps with policies](control-cloud-apps-with-policies)

**Required task**: Create policies

### To create policies

1. In the Microsoft Defender Portal, under **Cloud Apps**, choose **Policies** -&gt; **Policy templates**.
2. Choose a policy template from the list, and then select the **+** icon to create the policy.
3. Customize the policy (select filters, actions, and other settings), and then choose **Create**.
4. Under **Cloud Apps**, choose **Policies** -&gt; **Policy management**, to choose the policy and see the relevant matches (activities, files, alerts).

Tip

To cover all your cloud environment security scenarios, create a policy for each **risk category**.

### How can policies help your organization?

You can use policies to help you monitor trends, see security threats, and generate customized reports and alerts. With policies, you can create governance actions, and set data loss prevention and file-sharing controls.

## Step 4: Set up cloud discovery

**How to page**: [Set up cloud discovery](set-up-cloud-discovery)

**Required task**: Enable Defender for Cloud Apps to view your cloud app use

1. [Integrate with Microsoft Defender for Endpoint](mde-integration) to automatically enable Defender for Cloud Apps to monitor your Windows 10 and Windows 11 devices inside and outside your corporation.
2. If you use [Zscaler, integrate](zscaler-integration) it with Defender for Cloud Apps.
3. To achieve full coverage, create a continuous cloud discovery report

    1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
    2. Under **Cloud Discovery**, choose **Automatic log upload**.
    3. On the **Data sources** tab, add your sources.
    4. On the **Log collectors** tab, configure the log collector.

**Migration recommendation** We recommend using Defender for Cloud Apps discovery in parallel with your current CASB solution. Start by configuring automatic firewall log upload to Defender for Cloud Apps [log collectors](discovery-docker). If you use Defender for Endpoint, in the Defender portal, make sure you [turn on the option](mde-integration#how-to-integrate-microsoft-defender-for-endpoint-with-defender-for-cloud-apps) to forward signals to Defender for Cloud Apps. Configuring cloud discovery won't conflict with the log collection of your current CASB solution.

### To create a snapshot cloud discovery report

1. In the Microsoft Defender Portal, under **Cloud Apps**, choose **Cloud discovery**.
2. In the top right-hand corner, select **Actions** -&gt; **Create Cloud Discovery snapshot report**.

### Why should you configure cloud discovery reports?

Having visibility into shadow IT in your organization is critical. After your logs are analyzed, you can easily find which cloud apps are being used, by which people, and on which devices.

## Step 5: Personalize your experience

**How to page**: [Personalize your experience](mail-settings)

**Recommended task**: Add your organization details

### To enter email settings

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **System**, select **Mail settings**.
3. Under **Email sender identity**, enter your email addresses and display name.
4. Under **Email design**, upload your organization's email template.

### To set admin notifications

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Microsoft Defender XDR**.
2. Select **Email notifications**.
3. Configure the methods you want to set for system notifications.

### To customize the score metrics

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **Cloud Discovery**, choose **Score metrics**.
3. Configure the importance of various risk values.
4. Choose **Save**.

Now the risk scores given to discovered apps are configured precisely according to your organization needs and priorities.

### Why personalize your environment?

Some features work best when they're customized to your needs. Provide a better experience for your users with your own email templates. Decide what notifications you receive and customize your risk score metric to fit your organization's preferences.

## Step 6: Organize the data according to your needs

**How to page**: [Working with IP ranges and tags](ip-tags)

**Recommended task**: Configure important settings

### To create IP address tags

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **System**, select **IP address ranges**.
3. Select **+ Add IP address range** to add an IP address range.
4. Enter the IP range **Name**, **IP address ranges**, **Category**, and **Tags**.
5. Choose **Create**.

    Now you can use IP tags when you create policies, and when you filter and create continuous reports.

### To create continuous reports

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **Cloud Discovery**, choose **Continuous reports**.
3. Choose **Create report**.
4. Follow the configuration steps.
5. Choose **Create**.

Now you can view discovered data based on your own preferences, such as business units or IP ranges.

### To add domains

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **System**, choose **Organization details**.
3. Add your organization's internal domains.
4. Choose **Save**.

### Why should you configure these settings?

These settings help give you better control of features in the console. With IP tags, it's easier to create policies that fit your needs, to accurately filter data, and more. Use Data views to group your data into logical categories.