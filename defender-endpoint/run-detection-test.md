---
layout: Conceptual
title: Run a detection test on a device recently onboarded to Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/run-detection-test
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Run the detection test script on a device recently onboarded to the Microsoft Defender for Endpoint service to verify that it's properly added.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection:
- m365-security
- tier1
ms.topic: how-to
ms.subservice: onboard
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: a21eb553-65e1-22c6-9cd5-f7f60110ab51
document_version_independent_id: a21eb553-65e1-22c6-9cd5-f7f60110ab51
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/run-detection-test.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: run-detection-test
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/run-detection-test.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: aad7a743-914a-41da-7c5c-bd37a33b424b
---

# Run a detection test on a device recently onboarded to Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

When you add a device to the Microsoft Defender for Endpoint service for management, it's referred to as onboarding. Onboarding allows devices to report signals about their health status to Microsoft Defender for Endpoint.

Verifying that a device is added to the service successfully is a critical step in the entire deployment process. It helps ensure that all the devices expected are being managed.

This article explains how to run a PowerShell detection test on a recently onboarded device to confirm that it's properly reporting to the Defender for Endpoint service.

## Prerequisites

### Supported operating systems

The following operating systems are supported for the onboarding verification detection test:

- Windows Server 2012 R2
- Windows Server 2016 and later
- Azure Stack HCI OS, version 23H2 and later

## Verify Microsoft Defender for Endpoint onboarding of a device using a PowerShell detection test

Run the following PowerShell script on a newly onboarded device to verify that the device is properly reporting to the Defender for Endpoint service.

1. On the device, open Command Prompt as an administrator.
2. At the prompt, copy and run the following command. This command simulates a malicious download-and-execute pattern so that Microsoft Defender for Endpoint can detect it and confirm that the device is reporting correctly:

    ```powershell
    powershell.exe -NoExit -ExecutionPolicy Bypass -WindowStyle Hidden $ErrorActionPreference = 'silentlycontinue';(New-Object System.Net.WebClient).DownloadFile('http://127.0.0.1/1.exe', 'C:\\test-MDATP-test\\invoice.exe');Start-Process 'C:\\test-MDATP-test\\invoice.exe'
    ```

    The Command Prompt window closes automatically. If the script runs successfully, a new alert appears in the Microsoft Defender portal for the onboarded device in about 10 minutes.

    Note

    You can also [Configure extension file exclusions for Microsoft Defender Antivirus](microsoft-defender-antivirus-exclusions-configure) to perform this test. You'll receive a notification on the endpoint and an alert in the Microsoft Defender portal.