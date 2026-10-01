---
layout: Conceptual
title: Manage Devices in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-manage-devices
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to add, remove, and manage devices in Defender for Business, which provides endpoint protection for small and medium sized businesses.
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2026-07-03T00:00:00.0000000Z
ms.reviewer: nehabha
ms.collection:
- SMB
- m365-security
- m365-initiative-defender-business
- tier1
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 77fbc04b-58ab-7424-b183-a8ae0e54c07e
document_version_independent_id: 77fbc04b-58ab-7424-b183-a8ae0e54c07e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-manage-devices.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-manage-devices
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-manage-devices.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
platformId: 4478af19-08f5-c157-88eb-0c37feb3403c
---

# Manage Devices in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

In Defender for Business, you can manage devices as follows:

- View a list of onboarded devices to see their risk level, exposure level, and health state
- Take action on a device that has threat detections
- View the state of Microsoft Defender Antivirus
- Onboard a device to Defender for Business
- Offboard a device from Defender for Business

## View the list of onboarded devices

Use the following steps to view onboarded devices on the **Device inventory** page.

![Screenshot of device inventory](media/mdb-device-inventory.png)

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Assets** &gt; **Devices**. Or, go directly to the **Device inventory**[page](https://security.microsoft.com/machines).
2. On the **Device inventory** page, you can see the list of devices and view some information about them.
3. Select a device from the list to open the details pane for the device, where you can learn more about the status of the device and take actions.

If no devices are listed, see [Onboard devices to Defender for Business](mdb-onboard-devices).

## Take action on a device that has threat detections

Use the following steps to take available response actions on a device that has threat detections.

![Screenshot of a selected device with details and actions available.](media/mdb-selected-device.png)

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Assets** &gt; **Devices**. Or, go directly to the **Device inventory**[page](https://security.microsoft.com/machines).
2. On the **Device inventory** page, select a device from the list.
3. In the details pane that opens, select ![](media/defender-portal-icon-more-actions.png)**More**, and then select an available action, for example, **Run antivirus scan** or **Initiate Automated Investigation**.

## View the state of Microsoft Defender Antivirus

Microsoft Defender Antivirus is a key component of next-generation protection in Defender for Business. To view the state of Microsoft Defender Antivirus, you have several options:

- Use the [Device health report](mdb-reports#device-health-report).
- Use methods such as PowerShell, Group Policy, or the Windows Security app as described in [How to confirm the state of Microsoft Defender Antivirus](/en-us/defender-endpoint/microsoft-defender-antivirus-compatibility#how-to-confirm-the-state-of-microsoft-defender-antivirus).

Microsoft Defender Antivirus has one of the following states on devices:

- **Active mode** (*recommended*): Defender Antivirus is the exclusive antivirus app on a device onboarded to Defender for Business. It scans files and remediates threats. You can view detection information in the Microsoft Defender portal and in the Windows Security app on Windows devices.

    We recommend active mode so devices onboarded to Defender for Business get all of the following types of protection:

    - **Real-time protection**: Locates and stops malware from running on devices.
    - **Cloud protection**: Works with Defender Antivirus and the Microsoft Cloud to identify new threats, sometimes even before a single device is affected.
    - **Network protection**: Helps protect against phishing scams, exploit-hosting sites, and malicious content on the internet.
    - **Web content filtering**: Regulates access to websites based on content categories, such as adult content, high bandwidth, and legal liability, across all browsers.
    - **Protection from potentially unwanted applications**: For example:

        - Advertising software.
        - Bundled software that offers to install other, unsigned software.
        - Evasion software that attempts to evade security features.
- **Passive mode**: A non-Microsoft antivirus or antimalware product is installed on a device onboarded to Defender for Business. Defender Antivirus can detect threats and can receive security intelligence and platform updates. Defender Antivirus doesn't remediate threats.

    You can automatically switch to active mode by uninstalling the non-Microsoft antivirus or antimalware product.
- **Disabled mode**: Also known as *uninstalled mode*. A non-Microsoft antivirus or antimalware product is installed on a device that isn't onboarded to Defender for Business. Defender Antivirus isn't currently running on the device. It might be automatically disabled or manually disabled. Defender Antivirus can't detect or remediate threats on the device.

    You can switch to active mode by completing the following steps:

    1. Uninstall the non-Microsoft antivirus or antimalware solution.
    2. Onboard the device to Defender for Business.

### What to expect when Microsoft Defender Antivirus detects threats

When Microsoft Defender Antivirus detects a threat, the following things happen:

- Users receive [notifications in Windows](https://support.microsoft.com/windows/feeca47f-0baf-5680-16f0-8801db1a8466).
- Detections are listed in the [Windows Security app](/en-us/windows/security/operating-system-security/system-security/windows-defender-security-center/windows-defender-security-center) on the **Protection history** page.
- If you [secured your Windows devices](/en-us/microsoft-365/admin/security-and-compliance/m365bp-devices-enrollment), the threat detections and insights are available on the **Threats and antivirus** page in the [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home#/activethreats).

    Tip

    In Microsoft 365 Business Premium, if you have more than 800 devices [enrolled in Microsoft Intune](/en-us/intune/intune-service/fundamentals/deployment-guide-enrollment), you're prompted to view threat detections and insights from Microsoft Intune instead of from the **Threats and antivirus** page.

In most cases, users don't need to take any further action. As soon as a malicious file or program is detected on a device, Microsoft Defender Antivirus blocks it and prevents it from running. Plus, newly detected threats are added to the antivirus and anti-malware engine so that other devices and users are also protected.

If a user needs to take action, for example, approve the removal of a malicious file, the action is shown in the notification they receive. To learn more about actions that Microsoft Defender Antivirus takes on a user's behalf, or actions users might need to take, see [Protection History](https://support.microsoft.com/office/f1e5fd95-09b4-46d1-b8c7-1059a1e09708).

To learn more about different threats, see [Microsoft Security Intelligence Threats](https://www.microsoft.com/wdsi/threats) where you can take the following actions:

- View current information about top threats.
- View the latest threats for a specific region.
- Search the threat encyclopedia for details about a specific threat.

## Onboard a device

To onboard a device to Defender for Business, see [Onboard devices to Defender for Business](mdb-onboard-devices).

## Offboard a device

To remove a device from Defender for Business, see [Offboarding a device](mdb-offboard-devices).