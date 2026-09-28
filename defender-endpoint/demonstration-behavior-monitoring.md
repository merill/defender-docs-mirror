---
layout: Conceptual
title: Test behavior monitoring in Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/demonstration-behavior-monitoring
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to run behavior-monitoring demonstrations on Windows and macOS and verify the resulting Microsoft Defender Antivirus detections.
ms.service: defender-endpoint
ms.subservice: ngp
author: limwainstein
ms.author: lwainstein
ms.reviewer: yongrhee
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1015
ms.topic: how-to
ms.date: 2026-09-17T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 3cf5e41a-9556-7709-2a7d-903aff981f94
document_version_independent_id: 3cf5e41a-9556-7709-2a7d-903aff981f94
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/demonstration-behavior-monitoring.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: demonstration-behavior-monitoring
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/demonstration-behavior-monitoring.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: d9abb2a5-905e-66a5-b59c-bd3ce788b28a
---

# Test behavior monitoring in Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn

Behavior monitoring in Microsoft Defender Antivirus monitors applications, services, files, and processes for suspicious activity. Use the demonstrations in this article to confirm that behavior monitoring blocks known test behaviors on Windows or macOS and records the resulting detections.

## Prerequisites

- Use a supported Windows or macOS device. For supported operating systems and onboarding requirements, see [Minimum requirements for Microsoft Defender for Endpoint](minimum-requirements).
- On Windows, [verify that real-time protection is enabled](configure-real-time-protection-microsoft-defender-antivirus) and [query the behavior monitoring status](behavior-monitor#query-the-behavior-monitoring-status-from-powershell).
- On macOS, complete the [behavior monitoring prerequisites](behavior-monitor-macos#prerequisites), and then [verify that behavior monitoring is enabled](behavior-monitor-macos#verifying-behavior-monitoring-is-enabled).
- To review the resulting alert in the Microsoft Defender portal, the device must be onboarded to Defender for Endpoint.

## Test behavior monitoring on Windows

Use the Windows demonstration to confirm that behavior monitoring blocks the test behavior and records the detection.

### Run the Windows test command

Open PowerShell and run the following Microsoft behavior-monitoring test command:

```powershell
powershell.exe -NoExit -Command "powershell.exe hidden 12154dfe-61a5-4357-ba5a-efecc45c34c4"
```

PowerShell returns an expected `CommandNotFoundException`:

```console
hidden : The term 'hidden' is not recognized as the name of a cmdlet, function, script, script file, or operable program.  Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
At line:1 char:1
+hidden 12154dfe-61a5-4357-ba5a-efecc45c34c4
+""""""
CategoryInfo             : ObjectNotFound: (hidden:String) [], CommandNotFoundException
FullyQualifiedErrorId : CommandNotFoundException
```

### Review the Windows detection

Open the Windows Security app, select **Virus & threat protection**, and then select **Protection history**. For detailed instructions, see [Review threat detection history in the Windows Security app](microsoft-defender-security-center-antivirus).

The detection displays the threat name `Behavior:Win32/BmTestOfflineUI` with a blocked or removed status. The detection details resemble the following output:

```console
Threat blocked
Detected: Behavior:Win32/BmTestOfflineUI
Status: Removed
A threat or app was removed from this device.
Date: 6/7/2024 11:51 AM
Details: This program is dangerous and executes command from an attacker.
Affected items:
behavior: process: C:\Windows\System32\WindowsPowershell\v1.0\powershell.exe, pid:6132:118419370780344
process: pid:6132,ProcessStart:133621698624737241
Learn more    Actions
```

On the **Alerts** page in the Microsoft Defender portal at https://security.microsoft.com/alerts, look for an alert titled **Suspicious 'BmTestOfflineUI' behavior was blocked**.

Open the alert to review the detection tree and the message **Defender detected and terminated active 'Behavior:Win32/BmTestOfflineUI' in process 'powershell.exe' during behavior monitoring**. For information about reviewing alerts, see [Investigate alerts in Microsoft Defender for Endpoint](investigate-alerts).

## Test behavior monitoring on macOS

To confirm that behavior monitoring blocks the macOS test behavior and records the detection, follow these steps:

1. In a text editor, create a Bash script with the following content:

    ```bash
    #! /usr/bin/bash
    echo " " >> /tmp/9a74c69a-acdc-4c6d-84a2-0410df8ee480.txt
    echo " " >> /tmp/f918b422-751c-423e-bfe1-dbbb2ab4385a.txt
    sleep 5
    ```
2. Save as `BM_test.sh`.
3. Run the following command to make the bash script executable:

    ```bash
    sudo chmod u+x BM_test.sh
    ```
4. Run the bash script:

    ```bash
    sudo bash BM_test.sh
    ```

    The terminal reports that the process was killed. For example:

    `zsh: killed      sudo bash BM_test.sh`
5. Run the following command to confirm that Defender for Endpoint quarantined the test file and recorded the threat:

    ```bash
    mdatp threat list
    ```

    The result includes the threat name `Behavior: MacOS/MacOSChangeFileTest`, the type `behavior`, and the status `quarantined`, as shown in the following example:

    ```console
    ID: "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
    
    Name: Behavior: MacOS/MacOSChangeFileTest
    
    Type: "behavior"
    
    Detection time: Tue May 7 20:23:41 2024
    
    Status: "quarantined"
    ```
6. If the device is onboarded to Microsoft Defender for Endpoint Plan 1, Plan 2, or Microsoft Defender for Business, go to the **Alerts** page in the Microsoft Defender portal at https://security.microsoft.com/alerts. Look for an alert titled **Suspicious 'MacOSChangeFileTest' behavior was blocked**.

    For information about reviewing the alert, see [Investigate alerts in Microsoft Defender for Endpoint](investigate-alerts).