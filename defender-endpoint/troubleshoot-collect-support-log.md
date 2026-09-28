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
2. Initiate a [Live Response session](live-response#initiate-a-live-response-session-on-a-device) on the machine you need to investigate.
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
- As described in [Live response command examples](live-response-command-examples), you might want to use the `&` symbol at the end of the command to collect logs as a background action:

    ```console
    Run MDELiveAnalyzer.ps1&
    ```

## Linux

The XMDE Client Analyzer tool can be downloaded as a [binary](https://go.microsoft.com/fwlink/?linkid=2297517) or [Python](https://aka.ms/XMDEClientAnalyzer) package that can be extracted and executed on Linux machines. Both versions of the XMDE Client Analyzer can be executed during a Live Response session.

### Prerequisites

- For installation the `unzip` package is required.
- For execution the `acl` package is required.

Important

Window uses the Carriage Return and Line Feed invisible characters to represent the end of one line and beginning of a new line in a file, but Linux systems uses only the Line Feed invisible character at the end of its file lines. When using the following scripts, if done on Windows, this difference can result in errors and failures of the scripts to run. A potential solution to this is to utilize the Windows Subsystem for Linux and the `dos2unix` package to reformat the script so it aligns with the Unix and Linux format standard.

### Installing the XMDE Client Analyzer

Both versions of XMDE Client Analyzer, binary and Python, a self-contained package that must be downloaded and extracted before executing. For more information, see [Troubleshoot sensor health using Microsoft Defender for Endpoint Client Analyzer](overview-client-analyzer)

Due to the limited commands available in Live Response the steps detailed must be executed in a bash script, and by splitting the installation and execution portion of these commands it's possible to run the install script once, while running the execution script multiple times.

Important

The example scripts assume the machine has direct internet access and can retrieve the XMDE Client Analyzer from Microsoft. If the machine does not have direct internet access then the installation scripts will need to be updated to fetch the XMDE Client Analyzer from a location the machines can access successfully.

#### Binary Client Analyzer Install Script

The following script performs the first six steps of the [Running the Binary version of the Client Analyzer](overview-client-analyzer). When complete, the XMDE Client Analyzer binary is available from the `/tmp/XMDEClientAnalyzerBinary/ClientAnalyzer` directory.

1. Create a bash file `InstallXMDEClientAnalyzer.sh` and paste the following content into it.

    ```bash
    #! /usr/bin/bash
    
    echo "Starting Client Analyzer Script. Running As:"
    whoami
    
    echo "Getting XMDEClientAnalyzerBinary"
    wget --quiet -O /tmp/XMDEClientAnalyzerBinary.zip https://go.microsoft.com/fwlink/?linkid=2297517
    echo 'C65A4E4C6851D130942BFACD147A9D18B8A92B4F50FACF519477FD1C41A1C323 /tmp/XMDEClientAnalyzerBinary.zip' | sha256sum -c
    
    echo "Unzipping XMDEClientAnalyzerBinary.zip"
    unzip -q /tmp/XMDEClientAnalyzerBinary.zip -d /tmp/XMDEClientAnalyzerBinary
    
    echo "Unzipping SupportToolLinuxBinary.zip"
    unzip -q /tmp/XMDEClientAnalyzerBinary/XMDEClientAnalyzer/SupportToolLinuxBinary.zip -d /tmp/XMDEClientAnalyzerBinary/ClientAnalyzer
    
    echo "MDESupportTool installed at /tmp/XMDEClientAnalyzerBinary/ClientAnalyzer"
    
    ```

#### Python Client Analyzer Install Script

The following script performs the first six steps of the [Running the Python version of the Client Analyzer](overview-client-analyzer). When complete, the XMDE Client Analyzer Python scripts are available from the `/tmp/XMDEClientAnalyzer` directory.

1. Create a bash file `InstallXMDEClientAnalyzer.sh` and paste the following content into it.

    ```bash
    #! /usr/bin/bash
    
    echo "Starting Client Analyzer Install Script. Running As:"
    whoami
    
    echo "Getting XMDEClientAnalyzer.zip"
    wget --quiet -O XMDEClientAnalyzer.zip https://aka.ms/XMDEClientAnalyzer 
    echo '07E6A7B89E28A78309D5B6F1E25E4CDFBA9CA141450E422D76441C03AD3477E7 XMDEClientAnalyzer.zip' | sha256sum -c  
    
    echo "Unzipping XMDEClientAnalyzer.zip"
    unzip -q XMDEClientAnalyzer.zip -d /tmp/XMDEClientAnalyzer  
    
    echo "Setting execute permissions on mde_support_tool.sh script"
    cd /tmp/XMDEClientAnalyzer 
    chmod a+x mde_support_tool.sh  
    
    echo "Performing final support tool setup"
    ./mde_support_tool.sh
    
    ```

#### Running the Client Analyzer Install Scripts

1. Initiate a [Live Response session](live-response#initiate-a-live-response-session-on-a-device) on the machine you need to investigate.
2. Select **Upload file to library**.
3. Select **Choose file**.
4. Select the downloaded file named `InstallXMDEClientAnalyzer.sh`, and then select **Confirm**.
5. While still in the LiveResponse session, use the following commands to install the analyzer:

    ```console
    run InstallXMDEClientAnalyzer.sh
    ```

### Running the XMDE Client Analyzer

Live Response doesn't support running the XMDE Client Analyzer or Python directly, so an execution script is necessary.

Important

The following scripts assume the XMDE Client Analyzer was installed using the same locations from the scripts mentioned earlier. If your organization has chosen to install the scripts into a different location, then the following scripts need to be updated to align with your organization's chosen installation location.

#### Binary Client Analyzer Run Script

The Binary Client Analyzer accepts command line parameters to perform different analysis tests. To provide similar capabilities during Live Response the execution script takes advantage of the `$@` bash variable to pass all input parameters provided to the script to the XMDE Client Analyzer.

1. Create a bash file `MDESupportTool.sh` and paste the following content into it.

    ```bash
    #! /usr/bin/bash
    
    echo "cd /tmp/XMDEClientAnalyzerBinary/ClientAnalyzer"
    cd /tmp/XMDEClientAnalyzerBinary/ClientAnalyzer
    
    echo "Running MDESupportTool"
    ./MDESupportTool $@
    
    ```

#### Python Client Analyzer Run Script

The Python Client Analyzer accepts command line parameters to perform different analysis tests. To provide similar capabilities during Live Response the execution script takes advantage of the `$@` bash variable to pass all input parameters provided to the script to the XMDE Client Analyzer.

1. Create a bash file `MDESupportTool.sh` and paste the following content into it.

    ```bash
    #! /usr/bin/bash  
    
    echo "cd /tmp/XMDEClientAnalyzer"
    cd /tmp/XMDEClientAnalyzer 
    
    echo "Running mde_support_tool"
    ./mde_support_tool.sh $@
    
    ```

#### Running the Client Analyzer Script

Note

If you have an active Live Response session you can skip Step 1.

1. Initiate a [Live Response session](live-response#initiate-a-live-response-session-on-a-device) on the machine you need to investigate.
2. Select **Upload file to library**.
3. Select **Choose file**.
4. Select the downloaded file named `MDESupportTool.sh`, and then select **Confirm**.
5. While still in the Live Response session, use the following commands to run the analyzer and collect the resulting file.

    ```
    run MDESupportTool.sh -parameters "--bypass-disclaimer -d"
    GetFile "/tmp/your_archive_file_name_here.zip"
    ```