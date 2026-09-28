---
layout: Conceptual
title: Run remote MDE Client Analyzer traces via live response - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-remotely-with-client-analyzer
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Step-by-step guidelines to start and stop MDE Client Analyzer tracing on Windows devices via live response.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- mde-edr
ms.topic: troubleshooting
ms.subservice: edr
ms.date: 2026-01-13T00:00:00.0000000Z
locale: en-us
document_id: 08d6ac17-e44a-d319-1d08-5ae1409c4822
document_version_independent_id: 08d6ac17-e44a-d319-1d08-5ae1409c4822
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-remotely-with-client-analyzer.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-remotely-with-client-analyzer
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-remotely-with-client-analyzer.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 79de6589-044e-2934-63ab-69c0b324cab0
---

# Run remote MDE Client Analyzer traces via live response - Microsoft Defender for Endpoint | Microsoft Learn

On [Windows devices that support live response](live-response#supported-operating-systems), you can start and stop remote trace collection without signing in to the device. You can use this capability in the following scenarios:

- An issue happens only when the user is signed out.
- The specific environment where the issue happens is restricted. Direct user interaction for log collection isn't possible.

The rest of this article describes how to use live response to run the MDE Client Analyzer remotely on supported devices.

## Prerequisites

- Verify live response is enabled in Microsoft Defender for Endpoint. For instructions, see [Other requirements for live response](live-response#other-requirements).
- Download the latest version of the MDE Client Analyzer from https://aka.ms/Betamdeanalyzer.

## Step 1: Upload Files to your live response library

[Upload the following required files to your live response library](live-response#to-upload-a-file-in-the-library):

- `MDEClientAnalyzerPreview.zip`
- The following files extracted from the `Tools` folder of `MDEClientAnalyzerPreview.zip`:
    - `MDELiveAnalyzer.ps1`
    - `MDELiveAnalyzerPerf.ps1`

Other scripts for scenario-specific troubleshooting are also available in the `Tools` folder:

- `MDELiveAnalyzerAppCompat.ps1`
- `MDELiveAnalyzerAV.psl`
- `MDELiveAnalyzerNet.ps1`

## Step 2: Deploy the MDE Client Analyzer on the device

[Initiate a live response session on the device](live-response#initiate-a-live-response-session-on-a-device) and then run the following command in the session:

```dos
putfile MDEClientAnalyzerPreview.zip
```

The command output looks like this:

```dos
The file was uploaded to the device.
Path: C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Downloads\MDEClientAnalyzerPreview.zip
```

Tip

If you're uploading a newer version of the package, add the `-overwrite` switch to the `putfile` command.

## Step 3: Start trace collection on the device

In the live response session, run the following command to start background tracing:

```dos
run MDELiveAnalyzerPerf.ps1&
```

The command output looks like this:

```dos
[afb7f18a-8ad2-3b95-8eb3-6819159e253d]   (Just created)   Run MDELiveAnalyzerPerf.ps1&
```

Important

- Record the returned GUID value for session management. You use this value in a later step. This value is returned when calling a script with the `&` instruction.
- Adjust the script name for specific scenarios. For example, use `MDELiveAnalyzerNet.ps1` for network related troubleshooting scenarios.
- Wait a few minutes to ensure the analyzer initiates tracing before you go to the next step.

To verify the trace started successfully, do either of the following steps:

- Verify the existence of `WPR_initiated_sense_sense.etl` file in your live response session with the following `fileinfo` command:

    ```dos
    fileinfo C:\Windows\Temp\WPR_initiated_Sense_Sense.etl
    ```

    The output looks like this:

    ```dos
    {
      "C:\Windows\Temp\WPR_initiated_Sense_Sense.etl": {
        "error": O
        "path": "C:\Windows\Temp\WPR_initiated Sense Sense.etl",
        "size": 5373952,
        "downloaded" : false,
        "created": "2021-11-30 19:36:59",
        "modified": "2021-11-30 19:39:40",
        "mime type" : "application/octet-stream
        "compressed" : false,
        "executable_type": 0,
        "vendor": "",
        "directory_types": [
          "Temporary",
          "System"
        ],
        "read only": false,
        "hidden" : false,
        "3ha256": "f5ede3a2d3af8e125f8d238c4b3de80baa1ec4629887ef84e3e5b94b6925f9f9",
        "sha1": "50ff8c34e526b37e7c46c47b730e1dc29f23b9e5"
        "md5": "7def8ffbe58d6fcafb91a91fe2c338fa"
        "packed" : null,
        "ms verified" : false,
        "last access error": O,
        "last raw access error
        "file state": O,
        "file state display": [
          "Default"
        ],
        "digital signature" : null
    ...
    ```
- Use **Performance monitor** (run `perfmon.exe`) to verify **WPR\_initiated\_Sense\_Sense** is running under **Data Collector Sets** &gt; **Event Trace sessions** on the device as shown in the following screenshot:

    [![Screenshot of WPR_initiated_Sense_Sense running in Performance Monitor.](media/client-analyzer-performance-monitor.png)](media/client-analyzer-performance-monitor.png#lightbox)

## Step 4: Reproduce the issue on the device

Do the steps that trigger the problem on the device while the trace runs.

## Step 5: Stop trace collection on the device

After you reproduce the issue, run the following command in the live session to stop trace collection on the device:

```dos
Run MDELiveAnalyzer.ps1
```

The output looks like this:

```dos
Transcript started, output file is C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Temp\PSScriptOutputs\PSScript_Transcript_{0D5EC-4812-2A6A-81EC-C369F458}.txt
MDEClientAnalyzer EULA Accepted
Another non-interactive trace is already running... stopping log collection and exiting.
```

Bring the previous trace collection script from Step 3 to the foreground of the live session by using the GUID value from Step 3 in the following `fg` command. For example:

```dos
fg afb7f18a-8ad2-3b95-8eb3-6819159e253d
```

The output looks like this:

```dos
Transcript started, output file is C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Temp\PSScriptOutputs\PSScript_Transcript_{afb7f18a-8ad2-3b95-8eb3-6819159e253d}.txt
MDEClientAnalyzer EULA Accepted
2025-11-30 21:36:21Z [Informational] EDRCloud CnC 130017: Test connection to the Microsoft Defender for (CnC) cloud service URLs completed successfully. N/A
2025-11-30 21:36:21Z [Informational] EDRCloud Cyber 130018: Test connection to the Microsoft Defender for Endpoint (Cyber) cloud service URLs completed successfully. N/A
2025-11-30 21:36:21Z [Informational] EDRCloud AutoIR 130019: Test connection to the Microsoft Defender for Endpoint (AutoIR) cloud service URLs completed successfully. N/A
2025-11-30 21:36:21Z [Informational] AVCloud SampleUpload 130020: Test connection to the Microsoft Defender for Endpoint (SampleUpload) cloud service URLs completed successfully. N/A
2025-11-30 21:36:21Z [Informational] EDRCloud MdeConfigMgr 130021: Test connection to the Microsoft Defender for Endpoint (MdeConfigMgr) cloud service URLs completed successfully. N/A
2025-11-30 21:36:22Z [Informational] AVCloud 130011: Test connection to the Microsoft Defender Antivirus cloud service completed successfully. N/A
2025-11-30 21:36:22Z [Informational] AVCloud 130012: Current network connection is not metered. N/A
Running MpCmdRun -GetFiles...
Stopping any running WPR trace profiles
Stopping any running perfmon trace profiles
WARNING: Trace started... Note that you can stop this non-interactive mode by running 'MDEClientAnalyzer.cmd' from another window or session
Remaining seconds: 3599
Remaining seconds: 3272
Remaining seconds: 3271
Stop event was triggered!
Remaining seconds: 3270
Stopping any running trace profiles
Stopping and merging Defender Antivirus traces if running
Running MpCmdRun -GetFiles...
VERBOSE: Performing the operation "Copy File" on target "Item: C:\ProgramData\Microsoft\Windows Defender\Support\MpSupportFiles.cab Destination: C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Downloads\MDEClientAnalyzerResult\DefenderAV\MpSupportFiles.cab".
2025-11-30 21:46:29Z [Informational] CertRevocation 130010: Certificate validation for the Defender for Endpoint cloud service completed successfully. N/A
Evaluating cloud platform metadata...
Evaluating sensor condition...
Compressing results directory...
Result is available at C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Downloads\MDEClientAnalyzerResult.zip".
```

## Step 6: Download the trace results from the device

To retrieve the results from the device, run the following `getfile` command in the live session:

```dos
getfile "C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Downloads\MDECA\MDEClientAnalyzerResult.zip"
```