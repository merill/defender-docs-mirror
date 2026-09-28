---
layout: Conceptual
title: AMSI demonstrations with Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mde-demonstration-amsi
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Test AMSI detection in Microsoft Defender for Endpoint by using a benign sample. Learn how AMSI helps detect fileless and script-based threats and how to validate the engine safely.
author: limwainstein
ms.author: lwainstein
ms.reviewer: yongrhee
ms.localizationpriority: medium
ms.service: defender-endpoint
ms.subservice: ngp
ms.collection:
- m365-security
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom:
- msecd-doc-authoring-1016
- partner-contribution
ai-usage: ai-assisted
locale: en-us
document_id: ea14a0d5-6d44-f376-c27f-f025b5d002ea
document_version_independent_id: ea14a0d5-6d44-f376-c27f-f025b5d002ea
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mde-demonstration-amsi.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mde-demonstration-amsi
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mde-demonstration-amsi.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 2014f1f2-22a3-fc09-6f60-8c852328f0b1
---

# AMSI demonstrations with Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint uses the [Antimalware Scan Interface (AMSI)](amsi-on-mdav) to provide better protection against fileless malware, dynamic script-based attacks, and other nontraditional cyber threats. This article explains how to test the AMSI engine by using a benign sample.

## Prerequisites

Before you begin, make sure the following prerequisites are met:

- Microsoft Defender Antivirus (as primary) must be enabled, along with the following capabilities:
    - Real-Time Protection (RTP)
    - Behavior Monitoring (BM)
    - Turn on script scanning

### Supported operating systems

The following operating systems support this AMSI test scenario:

- Windows 10 and later
- Windows Server 2016 and later

## Testing AMSI with Defender for Endpoint

In this article, you can choose from three engines to test AMSI:

- PowerShell
- VBScript
- JavaScript

### Test AMSI with PowerShell

Perform the following steps to test AMSI by using PowerShell:

1. Save the following PowerShell script as `AMSI_PoSh_script.ps1`:

    ```powershell
    $testString = "AMSI Test Sample: " + "7e72c3ce-861b-4339-8740-0ac1484c1386"
    Invoke-Expression $testString
    ```
2. On your device, open PowerShell as an administrator.
3. Type `Powershell -ExecutionPolicy Bypass AMSI_PoSh_script.ps1`, and then press **Enter**.

    The expected PowerShell output is as follows:

    ```powershell
       Invoke-Expression : At line:1 char:1
    
       + AMSI Test Sample: 7e72c3ce-861b-4339-8740-8ac1484c1386
    
       + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    
       This script contains malicious content and has been blocked by your antivirus software.
    
       At C:\Users\Admin\Desktop\AMSI_PoSh_script.ps1:3 char:1
    
       + Invoke-Expression $testString
    
       + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    
       + CategoryInfo          : ParserError: (:) [Invoke-Expression], ParseException
    
       + FullyQualifiedErrorId : ScriptContainedMaliciousContent,Microsoft.PowerShell.Commands.InvokeExpressionCommand
        ```
    
    ```

### Testing AMSI with VBScript

Use the following steps to test AMSI with VBScript:

1. Save the following VBScript as `AMSI_vbscript.vbs`:

    ```vbscript
    REM Save this sample AMSI vbscript as AMSI_vbscript.vbs
    Dim result
    result = eval("AMSI Test Sample: " + "7e72c3ce-861b-4339-8740-0ac1484c1386")
    WScript.Echo result
    ```
2. On your Windows device, open Command Prompt as an administrator.
3. Type `wscript AMSI_vbscript.vbs`, and then press **Enter**.

    The expected VBScript output is as follows:

    ```vbscript
    Windows Script Host
    
    Script: C:\Users\Admin\Desktop\AMSI_vbscript.vbs
    
    Line: 3
    
    Char: 1
    
    Error: This script contains malicious content and has been blocked by your antivirus software.: 'eval'
    
    Code: 800A802D
    
    Source: Microsoft VBScript runtime error
    ```

### Testing AMSI with JavaScript

1. Save the following JavaScript as `AMSI_jscript.js`:

    ```javascript
    // Save the following file as AMSI_jscript.js
    var result = eval("AMSI Test Sample: " + "7e72c3ce-861b-4339-8740-0ac1484c1386")
    WScript.Echo(result);
    ```
2. On your Windows device, open Command Prompt as an administrator.
3. Type `cscript AMSI_jscript.js`, and then select **Enter**. The expected JavaScript output is as follows:

    ```javascript
    C:\tools>cscript AMSI_jscript.js
    Microsoft (R) Windows Script Host Version 10.0
    Copyright (C) Microsoft Corporation. All rights reserved.
    CScript Error: Loading script "C:\test\AMSI_jscript.js" failed (Operation did not complete successfully because the file contains a virus or potentially unwanted software. ).
    ```

### Verifying the test results

In your protection history, the following sample output confirms that AMSI detected and blocked the test payload:

```text
Threat blocked

Detected: Virus: Win32/MpTest!amsi

Status: Cleaned

This threat or app was cleaned or quarantined before it became active on your device.

Details: This program is dangerous and replicates by infecting other files.

Affected items:

amsi: \Device\HarddiskVolume3\Windows\System32\WindowsPowershell\v1.0\powershell.exe

or

amsi: C:\Users\Admin\Desktop\AMSI_vbscript.vbs

or

amsi: C:\Users\Admin\Desktop\AMSI_jscript.js

and/or you might see:

Threat blocked

Detected: Virus: Win32/MpTest!amsi

Status: Cleaned

This threat or app was cleaned or quarantined before it became active on your device.

Details: This program is dangerous and replicates by infecting other files
```

### Get the list of Microsoft Defender Antivirus threats

You can view detected threats by using the Event log or PowerShell.

#### Use the Event log

Use the following steps to view detected threats in Event Viewer:

1. Go to **Start**, and search for `EventVwr.msc`. Open Event Viewer in the list of results.
2. Go to **Applications and Services Logs** &gt; **Microsoft** &gt; **Windows** &gt; **Windows Defender operational events**.
3. Look for `event ID 1116`. You should see the following information:

    ```powershell
    
    Microsoft Defender Antivirus has detected malware or other potentially unwanted software.
    
    For more information please see the following: https://go.microsoft.com/fwlink/?linkid=37020&name=Virus:Win32/MpTest!amsi&t
    
    Name: Virus:Win32/MpTest!amsi
    
    ID: 2147694217
    
    Severity: Severe
    
    Category: Virus
    
    Path: \Device\HarddiskVolume3\Windows\System32\WindowsPowerShell\v1.0\powershell.exe or C:\Users\Admin\Desktop\AMSI_jscri
    
    Detection Origin: Local machine or Unknown
    
    Detection Type: Concrete
    
    Detection Source: System
    
    User: NT AUTHORITY\SYSTEM
    
    Process Name: C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe or C:\Windows\System32\cscript.exe or C:\Windows\Sy
    
    Security intelligence Version: AV: 1.419.221.0, AS: 1.419.221.0, NIS: 1.419.221.0
    
    Engine Version: AM: 1.1.24080.9, NIS: 1.1.24080.9
    ```

#### Use PowerShell

Use PowerShell to list detected threats by following these steps:

1. On your device, open PowerShell.
2. Type the following command: `Get-MpThreat`.

    You might see the following results:

    ```powershell
    CategoryID     : 42
    
    DidThreatExecute : True
    
    IsActive       : True
    
    Resources      :
    
    RollupStatus   : 97
    
    SchemaVersion  : 1.0.0.0
    
    SeverityID     : 5
    
    ThreatID       : 2147694217
    
    ThreatName     : Virus:Win32/MpTest!amsi
    
    TypeID         : 0
    
    PSComputerName :
    ```