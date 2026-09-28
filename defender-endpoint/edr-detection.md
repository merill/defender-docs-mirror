---
layout: Conceptual
title: EDR detection test for verifying device's onboarding and reporting service - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/edr-detection
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Run the EDR detection test to confirm a device is correctly onboarded and reporting to Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1016
ms.topic: how-to
ms.subservice: edr
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 9fea344c-a4b1-9729-8ae8-72cccebee32c
document_version_independent_id: 9fea344c-a4b1-9729-8ae8-72cccebee32c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/edr-detection.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: edr-detection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/edr-detection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 31ea3380-465a-cd7b-4008-f0a0e771812a
---

# EDR detection test for verifying device's onboarding and reporting service - Microsoft Defender for Endpoint | Microsoft Learn

## Prerequisites

Before you run the EDR detection test, make sure your environment meets these requirements:

- Windows client devices must be running Windows 11, Windows 10 version 1709 build 16273 or newer, Windows 8.1, or Windows 7 SP1.
- Windows server devices must be running Windows Server 2008 R2 SP1, Windows Server 2012 R2 and later, or Azure Stack HCI OS, version 23H2 and later.
- Linux servers must be running a supported version (see [Prerequisites for Microsoft Defender for Endpoint on Linux](mde-linux-prerequisites))
- Devices must be onboarded to Defender for Endpoint

Endpoint detection and response (EDR) in Microsoft Defender for Endpoint provides advanced, near real-time, actionable detections. Security analysts can prioritize alerts effectively, gain visibility into the full scope of a breach, and take response actions to remediate threats. You can run an EDR detection test to verify that the device is properly onboarded and reporting to the service. This article describes how to run an EDR detection test on a newly onboarded device.

## Run an EDR detection test

Use the following platform-specific procedures to run the EDR detection test.

### Run the EDR detection test on Windows

Tip

The Windows device must be listening for requests on TCP port 80 for the following commands to work. You can verify by running the following PowerShell command: `Test-NetConnection 127.0.0.1 -Port 80`.

In a Command Prompt window, run the following command to download and launch a test file that triggers an EDR detection:

```dos
powershell.exe -NoExit -ExecutionPolicy Bypass -WindowStyle Hidden $ErrorActionPreference='silentlycontinue';(New-Object System.Net.WebClient).DownloadFile('http://127.0.0.1/1.exe', 'C:\\test-WDATP-test\\invoice.exe');Start-Process 'C:\\test-WDATP-test\\invoice.exe'
```

If the command runs successfully and the test file executes, the Windows EDR detection test is marked as completed and a new alert appears within a few minutes.

### Run the EDR detection test on Linux

Perform the following steps to run the EDR detection test on Linux.

1. Download the MDE Linux EDR DIY package to an onboarded Linux server so you can extract and run the test script locally. For more information, see the [MDE Linux EDR DIY test script](https://aka.ms/MDE-Linux-EDR-DIY).

    ```bash
    curl -o ~/Downloads/MDE-Linux-EDR-DIY.zip -L https://aka.ms/MDE-Linux-EDR-DIY
    ```
2. Extract the downloaded archive to access the DIY test script and supporting files.

    ```bash
    unzip ~/Downloads/MDE-Linux-EDR-DIY.zip
    ```
3. Make the script executable so it can be launched from the terminal:

    ```bash
    chmod +x ./mde_linux_edr_diy.sh
    ```
4. Run the DIY script to start the EDR test scenario and verify endpoint detection behavior:

    ```bash
    ./mde_linux_edr_diy.sh
    ```

    After a few minutes, a detection should be raised in the [Microsoft Defender portal](https://security.microsoft.com). Look at the alert details, machine timeline, and perform your typical investigation steps.

### Run the EDR detection test on macOS

Perform the following steps to run the EDR detection test on macOS.

1. In your browser, Microsoft Edge for Mac or Safari, download *MDATP macOS DIY.zip* from the [macOS EDR DIY test file download page](https://aka.ms/mdatpmacosdiy) and extract the zipped folder.

    The following prompt appears:

> 
> Do you want to allow downloads on "mdatpclientanalyzer.blob.core.windows.net"? You can change which websites can download files in **Websites Preferences**.
2. Select **Allow** to permit downloads from "mdatpclientanalyzer.blob.core.windows.net".
3. Open **Downloads**.
4. You must be able to see **MDATP MacOS DIY**.

    Tip

    If you double-click **MDATP MacOS DIY**, you'll get the following message:

> 
> **"MDATP MacOS DIY" cannot be opened because the developer cannot be verified.** macOS cannot verify that this app is free from malware.**[Move to Trash]** **[Done]**
5. In the developer-verification warning dialog, click **Done**.
6. Right-click **MDATP MacOS DIY**, and then click **Open**.

    The system displays the following message:

> 
> **macOS cannot verify the developer of MDATP MacOS DIY. Are you sure you want to open it?** By opening this app, you will be overriding system security which can expose your computer and personal information to malware that may harm your Mac or compromise your privacy.
7. In the macOS security confirmation dialog, click **Open**.

    The system displays the following message:

> 
> Microsoft Defender for Endpoint - macOS EDR DIY test file Corresponding alert will be available in the MDATP portal.
8. In the EDR DIY test file dialog, click **Open**.

    In few minutes, an alert *macOS EDR Test Alert* is raised.
9. Go to Microsoft Defender portal (https://security.microsoft.com/).
10. Go to the **Alert** Queue.

    ![Screenshot that shows a macOS EDR test alert that shows severity, category, detection source, and a collapsed menu of actions](media/b8db76c2-c368-49ad-970f-dcb87534d9be.png)

    The macOS EDR test alert shows severity, category, detection source, and a collapsed menu of actions. Look at the alert details and the device timeline, and perform the regular investigation steps.