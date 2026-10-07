---
layout: Conceptual
title: Collect support logs in Microsoft Defender for Endpoint using live response - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-collect-support-log
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to collect logs using live response to troubleshoot Microsoft Defender for Endpoint issues
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-edr
ms.topic: troubleshooting
ms.subservice: edr
ms.date: 2025-07-04T00:00:00.0000000Z
locale: en-us
document_id: 4a0799b4-8ed7-4320-6b91-21986c3d2c98
document_version_independent_id: 4a0799b4-8ed7-4320-6b91-21986c3d2c98
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-collect-support-log.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-collect-support-log
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-collect-support-log.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 6410953e-80ba-f560-6b41-08a61bd92eef
---

# Collect support logs in Microsoft Defender for Endpoint using live response - Microsoft Defender for Endpoint | Microsoft Learn

When contacting support, you might be asked to provide the output package of the Microsoft Defender for Endpoint Client Analyzer tool.

This article provides instructions on how to run the tool via Live Response on Windows and on Linux machines.

## Windows

1. Download and fetch the required scripts available from within the **Tools** subdirectory of the [Microsoft Defender for Endpoint Client Analyzer](https://aka.ms/MDEClientAnalyzerPreview).

    For example, to get the basic sensor and device health logs, fetch `..\Tools\MDELiveAnalyzer.ps1`.

    - If you require additional logs related to Microsoft Defender Antivirus, then use `..\Tools\MDELiveAnalyzerAV.ps1`.
    - If you require [Microsoft Endpoint Data Loss Prevention](/en-us/purview/endpoint-dlp-learn-about) related logs, then use `..\Tools\MDELiveAnalyzerDLP.ps1`.
    - If you require network and [Windows Filter Platform](/en-us/windows-hardware/drivers/network/windows-filtering-platform-architecture-overview) related logs, then use `..\Tools\MDELiveAnalyzerNet.ps1`.
    - If you require [Process Monitor](/en-us/sysinternals/downloads/procmon) logs, then use `..\Tools\MDELiveAnalyzerAppCompat.ps1`.
2. Initiate a [Live Response session](/en-us/defender-endpoint/live-response#initiate-a-live-response-session-on-a-device) on the machine you need to investigate.
3. Select **Upload file to library**.

    [![The upload file](media/upload-file.png)](media/upload-file.png#lightbox)
4. Select **Choose file**. [![The choose file button-1](media/choose-file.png)](media/choose-file.png#lightbox)
5. Select the downloaded file named `MDELiveAnalyzer.ps1`, and then select on **Confirm**.

    [![The choose file button-2](media/analyzer-file.png)](media/analyzer-file.png#lightbox)

    Repeat this step for the `MDEClientAnalyzerPreview.zip` file.
6. While still in the LiveResponse session, use the following commands to run the analyzer and collect the resulting file.

    ```console
    Putfile MDEClientAnalyzerPreview.zip
    Run MDELiveAnalyzer.ps1
    GetFile "C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Downloads\MDECA\MDEClientAnalyzerResult.zip"
    ```

    [![Image of commands.](media/analyzer-commands.png)](media/analyzer-commands.png#lightbox)

### Additional information

- The latest *preview* version of MDE Client Analyzer can be downloaded at https://aka.ms/MDEClientAnalyzerPreview.
- For more information on gathering data locally on a machine in case the machine isn't communicating with Microsoft Defender for Endpoint cloud services, or doesn't appear in Microsoft Defender for Endpoint portal as expected, see [Verify client connectivity to Microsoft Defender for Endpoint service URLs](verify-connectivity).
- As described in [Live response command examples](/en-us/defender-endpoint/live-response-command-examples), you might want to use the `&` symbol at the end of the command to collect logs as a background action:

    ```console
    Run MDELiveAnalyzer.ps1&
    ```

## Linux

Use either the binary Live Response action pair, which doesn't require Python, or the Python action pair. Each installer downloads and validates the required Client Analyzer package on the device.

### Prerequisites

- The binary actions require `curl`, `find`, `mktemp`, `od`, `sha256sum`, `stat`, `unzip`, and standard POSIX shell utilities. They don't require `python3`.
- The Python actions require `python3` in addition to the common prerequisites.
- The device must be able to reach the Microsoft download endpoint over HTTPS. If it can't, use the local workflow in [Run the client analyzer on Linux](/en-us/defender-endpoint/run-analyzer-linux) with a package location that the device can reach.

Choose one of the following workflows for the collection.

### Option 1: Binary Client Analyzer

#### Install the binary Client Analyzer

1. Download the two binary action files:

    - [InstallXMDEClientAnalyzer.sh](https://github.com/microsoft/mdatp-xplat/blob/master/linux/LiveResponse/ClientAnalyzer/InstallXMDEClientAnalyzer.sh)
    - [MDESupportTool.sh](https://github.com/microsoft/mdatp-xplat/blob/master/linux/LiveResponse/ClientAnalyzer/MDESupportTool.sh)
2. If you prepare the action files on Windows, convert them to Unix line endings.
3. Upload both files to the Live Response library. Each action is self-contained.
4. Start a [Live Response session](/en-us/defender-endpoint/live-response#initiate-a-live-response-session-on-a-device), and run the installer without parameters:

    ```console
    run InstallXMDEClientAnalyzer.sh
    ```
5. Copy the workspace ID printed by the installer. It has the format `mde-client-analyzer-binary-` followed by 16 lowercase hexadecimal characters.

#### Run the binary Client Analyzer

Run the matching support action with exactly the workspace ID from the installer:

```console
run MDESupportTool.sh -parameters "mde-client-analyzer-binary-<workspace-id>"
```

The action selects the appropriate amd64 or arm64 package and starts diagnostic collection.

### Option 2: Python Client Analyzer

#### Install the Python Client Analyzer

1. Download the two Python action files:

    - [InstallXMDEPythonClientAnalyzer.sh](https://github.com/microsoft/mdatp-xplat/blob/master/linux/LiveResponse/ClientAnalyzer/InstallXMDEPythonClientAnalyzer.sh)
    - [MDEPythonSupportTool.sh](https://github.com/microsoft/mdatp-xplat/blob/master/linux/LiveResponse/ClientAnalyzer/MDEPythonSupportTool.sh)
2. If you prepare the action files on Windows, convert them to Unix line endings.
3. Upload both files to the Live Response library. Each action is self-contained.
4. Start a [Live Response session](/en-us/defender-endpoint/live-response#initiate-a-live-response-session-on-a-device), and run the installer without parameters:

    ```console
    run InstallXMDEPythonClientAnalyzer.sh
    ```
5. Copy the workspace ID printed by the installer. It has the format `mde-client-analyzer-python-` followed by 16 lowercase hexadecimal characters.

#### Run the Python Client Analyzer

Run the matching support action with exactly the workspace ID from the installer:

```console
run MDEPythonSupportTool.sh -parameters "mde-client-analyzer-python-<workspace-id>"
```

The action starts diagnostic collection.

### Retrieve the diagnostic package

The runner prints its private run-directory path before it starts the Client Analyzer. After the action finishes, retrieve the generated diagnostic archive from that directory. Use the archive filename reported by the analyzer.

```output
Client Analyzer run directory: /var/tmp/<workspace-id>/runs/run-<run-id>
```

```console
GetFile "<run-directory>/<diagnostic-archive>.zip"
```

Successful workspaces aren't automatically removed by these actions, and the actions don't define a fixed cleanup interval. Retrieve the archive promptly, and follow your organization's `/var/tmp` retention and cleanup policy. If the analyzer reports an error, use the error output and the [Run the client analyzer on Linux](/en-us/defender-endpoint/run-analyzer-linux) guidance to troubleshoot the device.

### Security and lifecycle

- The installer creates a randomized private workspace below `/var/tmp`, validates the downloaded package and entrypoint, and writes a completion record only after setup succeeds.
- The runner revalidates the workspace, completion record, ownership, permissions, and entrypoint digest immediately before execution.
- Rerun the installer if the workspace is removed by a local cleanup policy or the runner reports a validation failure.
- Replace both action files for the selected package in the Live Response library when a new version is published. Previously uploaded files and downloaded packages don't update automatically.

This guidance applies only to Linux Live Response actions.