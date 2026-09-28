---
layout: Conceptual
title: Protect any apps in use in your organization in real time - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/tutorial-proxy
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
description: This tutorial provides instructions for using access and session controls to monitor and control access to apps and their data.
ms.date: 2024-05-15T00:00:00.0000000Z
ms.topic: tutorial
locale: en-us
document_id: fc0f2d77-15a2-2bb6-dea5-2be9005cdd1c
document_version_independent_id: fc0f2d77-15a2-2bb6-dea5-2be9005cdd1c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/tutorial-proxy.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tutorial-proxy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/tutorial-proxy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 618a72a2-86a2-b81c-118f-f186114b21ec
---

# Protect any apps in use in your organization in real time - Microsoft Defender for Cloud Apps | Microsoft Learn

The apps you sanction employees to use, often store some of your most sensitive corporate data and secrets. In the modern workplace, users access these apps in many risky situations. These users could be partners in your organization over who you have little visibility, or employees using unmanaged devices or coming from public IP addresses. Due to the wide range of risks in this landscape, a zero-trust strategy must be employed. Often, it's not enough to know about breaches and data loss in these apps after the fact; therefore, many information protection and cyberthreat scenarios must be addressed or prevented in real time.

In this tutorial, you'll learn how to use access and session controls to monitor and control access to apps and their data. Adaptively managing access to your data and mitigating against threats allows Defender for Cloud Apps to protect your most sensitive assets. Specifically, we'll cover the following scenarios:

- Monitor user activities for anomalies
- Protect your data when it's exfiltrated
- Prevent unprotected data from being uploaded to your apps

## How to protect your organization from any app in real time

Use this process to roll out real-time controls in your organization.

### Phase 1: Monitor user activities for anomalies

Microsoft Entra ID apps are automatically deployed for Conditional Access app control, and are monitored in real time for immediate insights into their activities and related information. Use this information to identify anomalous behavior.

Use the Defender for Cloud Apps' [Activity Log](activity-filters) to monitor and characterize app use in your environment, and understand their risks. Narrow the scope of activities listed by using [search, filters, and queries](activity-filters-queries) to quickly identify risky activities.

### Phase 2: Protect your data when it's exfiltrated

A primary concern for many organizations is how to prevent data exfiltration before it happens. Two of the biggest risks are unmanaged devices (that may not be protected with a pin or may contain malicious apps) and guest users where your IT department has little visibility and control.

Now that your apps are deployed, you can easily configure policies to mitigate both of these risks by leveraging our native integrations with Microsoft Intune for device management, Microsoft Entra ID for user groups, and Microsoft Purview Information Protection for data protection.

- **Mitigate unmanaged devices**: Create a [session policy to label](session-policy-aad#create-a-defender-for-cloud-apps-session-policy) and protect highly confidential files meant for users in your organization only.
- **Mitigate guest users**: Create a [session policy to apply custom permissions](session-policy-aad#protect-download) to any file that is downloaded by guest users. For example, you can set permissions so that guest users can only access a protected file.

### Phase 3: Prevent unprotected data from being uploaded to your apps

In addition to preventing data exfiltration, organizations often want to make sure that data that is infiltrated to cloud apps is also secure. A common use case is when a user attempts to upload files that are not labeled correctly.

For any of the apps you've configured above, you can configure a session policy to prevent the upload of files that are not labeled correctly, as follows:

1. Create a session policy to [block uploads of incorrectly labeled files](session-policy-aad#protect-upload).
2. Configure a policy to display a [block message with instructions on how to correct the label and try again](session-policy-aad#educate-users-to-protect-sensitive-files).

Protecting file uploads in this way ensures that data saved to the cloud has the correct access permissions applied. In the event that a file is shared or lost, it can only be accessed by authorized users.

## Learn more

- Try our interactive guide: [Protect and control information with Microsoft Defender for Cloud Apps](https://mslearn.cloudguides.com/guides/Protect%20and%20control%20information%20with%20Microsoft%20Cloud%20App%20Security)