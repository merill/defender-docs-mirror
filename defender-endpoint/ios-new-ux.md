---
layout: Conceptual
title: User experiences in Microsoft Defender for Endpoint on iOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/ios-new-ux
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about major user experience changes for versions of Microsoft Defender for Endpoint on iOS.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: sunasing; denishdonga
ms.localizationpriority: medium
ms.date: 2026-07-22T00:00:00.0000000Z
ms.collection:
- m365-security
- tier3
- mde-ios
ms.topic: reference
ms.subservice: ios
ms.custom: sfi-image-nochange, msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: ad06eab2-824a-0244-aa25-1b3f7bd1ce7b
document_version_independent_id: ad06eab2-824a-0244-aa25-1b3f7bd1ce7b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/ios-new-ux.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ios-new-ux
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/ios-new-ux.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: bf62ad5e-01e2-0ce4-3240-86a7768e3846
---

# User experiences in Microsoft Defender for Endpoint on iOS - Microsoft Defender for Endpoint | Microsoft Learn

As part of our ongoing commitment to deliver exceptional user experiences, we're excited to announce a series of upcoming changes to the user interface and overall experience of our **Microsoft Defender for Endpoint** mobile app.

The new enhancements are designed to improve usability, streamline navigation, and ensure our app meets the evolving needs of our users.

## Key changes - November 2025

In this release, we've made it easier for users to share feedback, including logs, to the Microsoft Defender team. The changes include:

- A new bottom pane that makes it easier for users to share feedback and logs
- A new **Send logs to Microsoft** option that enables users to quickly send logs to Microsoft

### Bottom pane experience

When users select **Help and Feedback** in the left navigation pane (Screen 1, accessible by tapping the profile picture), a new bottom feedback pane opens (Screen 2). This pane has been updated to improve readability and make it easier for users to share feedback.

The **Send feedback** option in the updated bottom pane enables users to share positive or negative feedback, along with Microsoft Defender and authenticator logs, which will be accessible to the Microsoft Defender team. When a user selects **Send feedback**, they're redirected to a new screen (Screen 3) where they can include logs along with their feedback submission.

![Screenshots showing how to send feedback and logs from the Microsoft Defender mobile app options menu.](media/ios-new-ux/bottom-experience-ios.png)

### One-click *Send Logs* experience

A new **Send logs to Microsoft** option has been added directly to the left navigation pane (Screen 1). This enables users to quickly send logs to Microsoft. It redirects them to the logs submission page (Screen 2). This option is particularly useful when a support case has been created and a support engineer is assigned, providing a convenient way for users to submit logs. Because this option doesn't allow users to include written feedback, the Defender team won't have access to the logs unless the incident ID is explicitly shared via mail or support request. This option only collects logs from the Defender app - it won't include logs from the Authenticator app.

![Screenshots showing how to send logs directly to Microsoft from the Microsoft Defender mobile app options menu.](media/ios-new-ux/one-click-feedback-ios.png)

## Key changes - Previous

We're pleased to introduce the **Device Protection** feature card for our enterprise users that includes Web Protection, Device Health and Jail break feature that has been designed to be more user-friendly and accessible. The updated feature cards now include recommendation cards. The first recommendation card will prominently display any active alerts, ensuring you stay informed. Additionally, a list of features will now be presented in the form of tiles as a part of L2 screens enhancing ease of use and navigation.

**The main changes involved are**:

- Main dashboard changes
- List the features inside one feature card
- Detailed features experience
- Recommendation cards for alerts
- Onboarding screens

### Main Dashboard changes

The main Dashboard screen that appears for enterprise users as per our latest rollout of enhancements to the application.

[![Screenshot that shows the Microsoft Defender for Endpoint Mobile Dashboard on iOS devices before the new update.](media/mde-ios-main-dash-new.png)](media/mde-ios-main-dash-new.png#lightbox)

### List the features inside one feature card

One feature card called **Device Protection** lists Web Protection, Device Health, and Jail Break. Previously, the dashboard had one card for each set of capabilities. In the new experience, only the Device Protection card changes.

[![Screenshot that shows the Microsoft Defender for Endpoint Feature Card.](media/mde-ios-list-new.png)](media/mde-ios-list-new.png#lightbox)

### Detailed feature experience

We updated all the subordinating screens associated with the **Device Protection** feature

1. **Web Protection**

    [![Screenshot that shows the web protection feature on the Defender for Endpoint on iOS app.](media/mde-ios-web-protection-new.png)](media/mde-ios-web-protection-new.png#lightbox)
2. **Device Health**

    Note

    Microsoft is deprecating the Device Health feature. Deprecation begins in mid-July 2026 and finishes by late July 2026.

    [![Screenshot that shows the new device health feature on the Defender for Endpoint on iOS app.](media/mde-device-health-new.png)](media/mde-device-health-new.png#lightbox)

### Recommendation cards for alerts

The structure of the dashboard is updated to include a recommendation card that contains active alerts (if any). In case there are multiple alerts, resolving the top alert brings forward the next one. Recommendation cards are implemented to provide a more cohesive user experience. These cards are designed to display important alerts and notifications prominently on the dashboard. Here are a few examples:

1. **Web Protection**

    [![Screenshot that shows the web protection  recommendation card feature on the Defender for Endpoint on iOS app.](media/mde-ios-web-protection-rec-card.png)](media/mde-ios-web-protection-rec-card.png#lightbox)
2. **Device Health (iOS Update)**

    Note

    Starting late July 2026, the Device Health (iOS Update) recommendation card no longer appears.

    [![Screenshot that shows the device health recommendation card feature on the MDE iOS app.](media/mde-ios-device-health-rec-card.png)](media/mde-ios-device-health-rec-card.png#lightbox)

### Onboarding screens

This section details these changes:

- VPN Permission flow while Onboarding
- VPN Permission flow after Onboarding
- TVM EUPI Screen

### VPN permission flow while onboarding

This is the main VPN Permission screen that appears to the enterprise's users as per our latest rollout of enhancements in the application.

#### Before

[![Screenshot that shows the Microsoft Defender for Endpoint mobile iOS setup before the new update.](media/ios-vpn-before.png)](media/mde-ios-main-dash-new.png#lightbox)

#### Now

[![Screenshot that shows the Microsoft Defender for Endpoint mobile iOS setup after the new update.](media/ios-vpn-after.png)](media/mde-ios-main-dash-new.png#lightbox)

### VPN permission flow after onboarding

This screen is seen when the VPN configuration is deleted from user's device, and the VPN needs to be re-enabled.

[![Screenshot that shows the Microsoft Defender for Endpoint mobile iOS re-enable screen.](media/ios-vpn-re-enable.png)](media/mde-ios-list-new.png#lightbox)

### TVM EUPI screen

We've enhanced the TVM EUPI screen as made it align with our current code flow.

#### Before

[![Screenshot that shows the Microsoft Defender for Endpoint mobile iOS TVM EUPI screen before the new update.](media/ios-tvm-before.png)](media/mde-ios-main-dash-new.png#lightbox)

#### Now

[![Screenshot that shows the Microsoft Defender for Endpoint mobile iOS TVM EUPI after the new update.](media/ios-tvm-after.png)](media/mde-ios-main-dash-new.png#lightbox)