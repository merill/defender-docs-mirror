---
layout: Conceptual
title: Review and edit settings in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-portal-advanced-feature-settings
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: View and edit settings for the Microsoft Defender portal and advanced features in Defender for Business
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2025-09-23T00:00:00.0000000Z
ms.reviewer: efratka
ms.collection:
- SMB
- m365-security
- m365solution-mdb-setup
- highpri
- tier2
locale: en-us
document_id: 9b62523a-b38b-948b-f839-8e04aeb3670e
document_version_independent_id: 9b62523a-b38b-948b-f839-8e04aeb3670e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-portal-advanced-feature-settings.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-portal-advanced-feature-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-portal-advanced-feature-settings.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
platformId: d938a918-a744-a553-6ee8-746c795689b3
---

# Review and edit settings in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

You can view and edit settings, such as portal settings and advanced features, in the Microsoft Defender portal (https://security.microsoft.com). Use this article to get an overview of the various settings that are available and how to edit your Defender for Business settings.

## View settings for advanced features

In the Microsoft Defender portal (https://security.microsoft.com), go to **Settings** &gt; **Endpoints** &gt; **General** &gt; **Advanced features**.

The following table describes advanced feature settings.

| Setting | Description |
| --- | --- |
| **Automated Investigation**(turned on by default) | As alerts are generated, automated investigations can occur. Each automated investigation determines whether a detected threat requires action and then takes or recommends remediation actions. For example: <br>- Send a file to quarantine.<br>- Stop a process.<br>- Isolate a device.<br>- Blocking a URL.<br><br> While an investigation is running, any related alerts that arise are added to the investigation until it's complete. If an affected entity is seen elsewhere, the automated investigation expands its scope to include that entity, and the investigation process repeats.  You can view investigations on the **Incidents** page. Select an incident, and then select the **Investigations** tab.  By default, automated investigation and response capabilities are turned on organization wide. **We recommend keeping automated investigation turned on**. If you turn it off, real-time protection in Microsoft Defender Antivirus is affected, and your overall level of protection is reduced. [Learn more about automated investigations](/en-us/defender-endpoint/automated-investigations). |
| **Live Response** | Defender for Business includes the following types of manual response actions: <br>- Run antivirus scan<br>- Isolate device<br>- Stop and quarantine a file<br>- Add an indicator to block or allow a file<br><br>[Learn more about response actions](/en-us/defender-endpoint/respond-machine-alerts). |
| **Live Response for Servers** | (This setting is currently not available in Defender for Business.) |
| **Live Response unsigned script execution** | (This setting is currently not available in Defender for Business.) |
| **Enable EDR in block mode**(turned on by default) | Provides added protection from malicious artifacts when Microsoft Defender Antivirus isn't the primary antivirus product and is running in passive mode on a device. Endpoint detection and response (EDR) in block mode works behind the scenes to remediate malicious artifacts detected by EDR capabilities. The primary non-Microsoft antivirus product might miss these artifacts. [Learn more about EDR in block mode](/en-us/defender-endpoint/edr-in-block-mode). |
| **Allow or block a file**(turned on by default) | Enables you to allow or block a file by using [indicators](/en-us/defender-endpoint/indicator-file). This capability requires Microsoft Defender Antivirus to be in active mode and [cloud protection](/en-us/defender-endpoint/cloud-protection-microsoft-defender-antivirus) turned on.  Blocking a file prevents it from being read, written, or executed on devices in your organization. [Learn more about indicators for files](/en-us/defender-endpoint/indicator-file). |
| **Custom network indicators**(turned on by default) | Enables you to allow or block an IP address, URL, or domain by using [network indicators](/en-us/defender-endpoint/indicator-ip-domain). This capability requires Microsoft Defender Antivirus to be in active mode and [network protection](/en-us/defender-endpoint/enable-network-protection) turned on.  You can allow or block IPs, URLs, or domains based on your threat intelligence. You can also prompt users if they open a risky app, but the prompt doesn't stop them from using the app. [Learn more about network protection](/en-us/defender-endpoint/network-protection). |
| **Tamper protection**(we recommend you turn on this setting) | Tamper protection prevents malicious apps from doing actions such as: <br>- Disable virus and threat protection<br>- Disable real-time protection<br>- Turn off behavior monitoring<br>- Disable cloud protection<br>- Remove security intelligence updates<br>- Disable automatic actions on detected threats<br>Tamper protection essentially locks Microsoft Defender Antivirus to its secure, default values and prevents apps and unauthorized methods from changing your security settings.[Learn more about tamper protection](/en-us/defender-endpoint/tamper-protection-overview). |
| **Show user details**(turned on by default) | Enables people in your organization to see details, such as user pictures, names, titles, and departments. These details are stored in Microsoft Entra ID. [Learn more about user profiles in Microsoft Entra ID](/en-us/entra/fundamentals/how-to-manage-user-profile-info). |
| **Skype for Business integration**(turned on by default) | Integration with Microsoft Teams (or the former Skype for Business) enables one-click communication between people in your business. |
| **Web content filtering**(turned on by default) | Blocks access to websites that contain unwanted content and tracks web activity across all domains. See [Set up web content filtering](mdb-web-content-filtering). |
| **Microsoft Intune connection**(we recommend you turn on this setting if you have Intune) | If your organization's subscription includes Microsoft Intune (included in [Microsoft 365 Business Premium resources](/en-us/microsoft-365/business-premium/)), this setting enables Defender for Business to share information about devices with Intune. |
| **Device discovery**(turned on by default) | Enables your security team to find unmanaged devices that are connected to your company network. Unknown and unmanaged devices introduce significant risks to your network, whether it's an unpatched printer, a network device with a weak security configuration, or a server with no security controls.  Device discovery uses onboarded devices to discover unmanaged devices, so your security team can onboard the unmanaged devices and reduce your vulnerability. [Learn more about device discovery](/en-us/defender-endpoint/device-discovery). |
| **Preview features** | Microsoft is continually updating services such as Defender for Business to include new feature enhancements and capabilities. If you opt in to receive preview features, you're among the first to try upcoming features in the preview experience. [Learn more about preview features](/en-us/defender-xdr/preview). |

## View and edit other settings in the Microsoft Defender portal

In addition to security policies applied to devices, there are other settings you can view and edit in Defender for Business. For example, you specify the time zone to use, and you can onboard (or offboard) devices.

Note

You might see more settings in your organization than are listed in this article. This article highlights the most important settings that you should review in Defender for Business.

### Settings to review for Defender for Business

The following table describes settings you can view and edit in Defender for Business:

| Category | Setting | Description |
| --- | --- | --- |
| **Security center** | **Time zone** | Select the time zone to use for the dates and times displayed in incidents, detected threats, and automated investigation and remediation. You can either use UTC or your local time zone (*recommended*). |
| **Microsoft Defender XDR** | **Account** | View details such where your data is stored, your tenant ID, and your organization (org) ID. |
| **Microsoft Defender XDR** | **Preview features** | Turn on preview features to try upcoming features and new capabilities. You can be among the first to preview new features and provide feedback. |
| **Endpoints** | **Email notifications** | Set up or edit your email notification rules. When vulnerabilities are detected or an alert is created, the recipients specified in your email notification rules receive an email notification. [Learn more about email notifications](mdb-email-notifications). |
| **Endpoints** | **Device management** &gt; **Onboarding** | Onboard devices to Defender for Business by using a downloadable script. For more information, see [Onboard devices to Defender for Business](mdb-onboard-devices). |
| **Endpoints** | **Device management** &gt; **Offboarding** | Offboard (remove) devices from Defender for Business. Offboarded devices no longer send data to Defender for Business. Data from when the device was onboarded is retained. For more information, see [Offboarding a device](mdb-offboard-devices). |

### Access your settings in the Microsoft Defender portal

1. Go to the Microsoft Defender portal (https://security.microsoft.com/), and sign in.
2. Select **Settings**, and then select a category (such as **Security center**, **Microsoft Defender XDR**, or **Endpoints**).
3. In the list of settings, select an item to view or edit.