---
layout: Conceptual
title: Microsoft Defender for Endpoint Cloud-delivered protection demonstration - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/defender-endpoint-demonstration-cloud-delivered-protection
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: See how Cloud-delivered protection can automatically detect and delete malicious files.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.reviewer: yongrhee
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- demo
ms.topic: article
ms.subservice: ngp
ms.date: 2025-10-20T00:00:00.0000000Z
locale: en-us
document_id: bd69c535-62c4-403a-e3b2-4f585e0002cf
document_version_independent_id: bd69c535-62c4-403a-e3b2-4f585e0002cf
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/defender-endpoint-demonstration-cloud-delivered-protection.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-endpoint-demonstration-cloud-delivered-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/defender-endpoint-demonstration-cloud-delivered-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19ec6774-09b8-473e-a17e-b17b518bbad7
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ade36b61-c646-4bd8-87ee-f3a843461962
platformId: 4d4fac6c-483e-0c3e-c08c-c49d7757afff
---

# Microsoft Defender for Endpoint Cloud-delivered protection demonstration - Microsoft Defender for Endpoint | Microsoft Learn

Cloud-delivered protection for Microsoft Defender Antivirus, also referred to as Microsoft Advanced Protection Service (MAPS), provides you with strong, fast protection in addition to our standard real-time protection.

## Prerequisites

- Microsoft Defender Real-time protection is enabled
- Cloud-delivered protection is enabled by default, however you may need to re-enable it if it has been disabled as part of previous organizational policies. For more information, see [Enable cloud-delivered protection in Microsoft Defender Antivirus](/en-us/windows/threat-protection/windows-defender-antivirus/enable-cloud-protection-windows-defender-antivirus?ocid=wd-av-demo-cloud-middle).
- You can also download and use the [PowerShell script](https://www.powershellgallery.com/packages/WindowsDefender_InternalEvaluationSettings/) to enable this setting and others on Windows 10 and Windows 11.

### Supported operating systems

- Windows 11
- Windows 10
- Windows 8.1
- Windows 7 SP1

### Scenario

1. Download and extract the [zipped folder that contains the test file](https://go.microsoft.com/fwlink/?linkid=2298135). The password is *infected*.

    Important

    The test file isn't malicious, it's just a harmless file simulating a virus.
2. If you see file blocked by Microsoft Defender SmartScreen, select on "View downloads" button.

    ![SmartScreen blocks an unsafe download, and provides a button to select to view the **Downloads** list details.](media/cloud-delivered-protection-smartscreen-block.png)
3. In Downloads menu right select on the blocked file and select on **Download unsafe file**.

    ![Lists the download as unsafe, but provides an option to proceed with the download](media/cloud-delivered-protection-smartscreen-block-view-downloads.png)
4. Navigate to the location where the file was downloaded. Attempt to open or execute the file by double clicking it. You should see that Microsoft Defender Antivirus found a virus and deleted the file.

    Note

    In some cases, you might also see **Threat Found** notification from Microsoft Defender Security Center.

    ![Microsoft Defender Antivirus Threats found notification provides options to get details](media/cloud-delivered-protection-smartscreen-threat-found-notification.png)
5. If the file executes, or if you see that it was blocked by Microsoft Defender SmartScreen, cloud-delivered protection isn't working. For more information, see [Configure and validate network connections for Microsoft Defender Antivirus](/en-us/windows/threat-protection/windows-defender-antivirus/configure-network-connections-windows-defender-antivirus?ocid=wd-av-demo-cloud-middle).