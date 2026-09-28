---
layout: Conceptual
title: Troubleshoot Microsoft Defender Antivirus performance issues with WPRUI - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-av-performance-issues-with-wprui
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot Microsoft Defender Antivirus performance issues with WPRUI
author: chrisda
ms.author: chrisda
ms.reviewer: yongrhee
ms.service: defender-endpoint
ms.topic: troubleshooting-general
ms.date: 2025-01-08T00:00:00.0000000Z
ms.subservice: ngp
ms.localizationpriority: medium
ai-usage: human-only
ms.collection:
- m365-security
ms.custom:
- partner-contribution
- sfi-image-nochange
locale: en-us
document_id: 0906dee4-200e-a19b-817f-7edd4398549b
document_version_independent_id: 0906dee4-200e-a19b-817f-7edd4398549b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-av-performance-issues-with-wprui.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-av-performance-issues-with-wprui
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-av-performance-issues-with-wprui.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 1307f7d3-fb19-e2a1-ab38-64003bf0ac63
---

# Troubleshoot Microsoft Defender Antivirus performance issues with WPRUI - Microsoft Defender for Endpoint | Microsoft Learn

Tip

First, review common reasons for performance issues such as high CPU usage in [Troubleshoot performance issues related to Microsoft Defender Antivirus real-time protection (RTP) or scans (scheduled or on-demand](troubleshoot-performance-issues)). Then, run the [Microsoft Defender Antivirus Performance Analyzer](tune-performance-defender-antivirus) to analyze the cause of high CPU usage in Microsoft Defender Antivirus (Antimalware Service Executable, Microsoft Defender Antivirus service, or MsMpEng.exe). If the Microsoft Defender Antivirus Performance Analyzer doesn't identify the root cause of high CPU utilization, run [Processor Monitor](troubleshoot-av-performance-issues-with-procmon) to narrow down or determine the root cause of the high CPU utilization in Microsoft Defender Antivirus. The final tool in your toolkit is to run the Windows Performance Recorder UI (WPRUI) or the Windows Performance Recorder (WPR command-line) as discussed in this article.

## Capture performance logs using Windows Performance Recorder

Windows Performance Recorder (WPR) is a powerful recording tool that creates Event Tracing for Windows recordings and allows you to include additional information in your submission to Microsoft support.

WPR is part of the Windows Assessment and Deployment Kit (Windows ADK) and can be downloaded from [Download and install the Windows ADK](/en-us/windows-hardware/get-started/adk-install). You can also download it as part of the Windows 10 Software Development Kit at [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk/).

Alternatively, follow the steps in [Capture performance logs using the WPR UI](troubleshoot-av-performance-issues-with-wprui), or use the command-line tool *wpr.exe*[Capture performance logs using the WPR CLI](troubleshoot-av-performance-issues-with-wprui). Both are available in Windows 8 and later versions.

There are two ways to capture the Windows Performance Recorder (WPRUI) trace:

1. Using the MDE Client Analyzer
2. Manually

## Using the MDE Client Analyzer

1. Download the [MDE Client Analyzer](overview-client-analyzer).
2. Run the MDE Client Analyzer using [Live Response or locally](run-analyzer-windows).

    Tip

    Before starting the trace, make sure the issue is reproducible. Additionally, close any applications that don't contribute to the reproduction of the issue.
3. Run the MDE Client Analyzer with the `-a` and `-v` switches.

    PowerShellCopy

    ```
    C:\Work\tools\MDEClientAnalyzer\MDEClientAnalyzer.cmd -a -v
    ```

## Manually

### Capture performance logs using the WPR UI

Tip

If multiple devices are experiencing this issue, use the one with the most RAM.

1. Download and install WPR.
2. Under *Windows Kits*, right-click **Windows Performance Recorder**.

    ![Screenshot showing the Start menu](media/wpr-01.png)
3. Select **More**. Select **Run as administrator**.
4. Right-click **Yes** when the User Account Control dialog box appears.

    ![Screenshot showing the UAC page.](media/wpt-yes.png)
5. Next, download the [Microsoft Defender for Endpoint analysis](https://github.com/YongRhee-MDE/Scripts/blob/master/MDAV.wprp) profile and save as `MDAV.wprp` to a folder such as `C:\temp`.
6. In the WPR dialog box, select **More options**.

    ![Screenshot showing the page where you can select more options](media/wpr-03.png)
7. Select **Add Profiles...** and browse to the path of the `MDAV.wprp` file.
8. A new profile named Microsoft Defender for Endpoint analysis should appear under Custom measurements.

    ![Screenshot showing the in-file.](media/wpr-infile.png)

    Warning

    If your Windows Server has 64 GB of RAM or more, use the custom measurement `Microsoft Defender for Endpoint analysis for large servers` instead of `Microsoft Defender for Endpoint analysis`. Otherwise, your system might consume a high amount of nonpaged pool memory or buffers, leading to system instability. To address this, explore **Resource Analysis** to choose profiles to add. This custom profile provides the necessary context for in-depth performance analysis.
9. To use the custom measurement Microsoft Defender for Endpoint verbose analysis profile in the WPR UI:

    1. Ensure no profiles are selected under the *First-level triage*, *Resource Analysis* and *Scenario Analysis* groups.
    2. Select **Custom measurements**.
    3. Select **Microsoft Defender for Endpoint analysis**.
    4. Select **Verbose** under *Detail* level.
    5. Select **File** or **Memory** under Logging mode.

    Important

    Select **File** to use the file logging mode if you can directly reproduce the performance issue. Most issues fall under this category. However, if you can't directly reproduce the issue, select **Memory** to use the memory logging mode. This prevents the trace log from inflating excessively due to long run times.
10. Now you're ready to collect data. Close all unnecessary applications. Select **Hide options** to keep the space occupied by the WPR window small.

    ![Screenshot showing the Hide options.](media/wpr-08.png)
11. Select **Start**.

    ![Screenshot showing the Record system information page.](media/wpr-09.png)
12. Reproduce the issue.

    Tip

    Limit the data collection to a maximum of five minutes. Ideally, aim for two to three minutes, as a significant amount of data is being collected.
13. Select **Save**.

    ![Screenshot showing the Save option.](media/wpr-10.png)
14. Fill in **Type in a detailed description of the problem:** with information about the problem and how you reproduced the issue.

    ![Screenshot showing the pane in which you fill.](media/wpr-12.png)
15. Select **File Name:** to determine where your trace file is saved. By default, it's saved to `%user%\Documents\WPR Files\`.
16. Select **Save**.

    ![Screenshot showing the WPR gathering general trace.](media/wpr-13.png)
17. After the trace has been merged and saved, right-click **Open folder**.

    ![Screenshot that displays the notification that WPR trace has been saved.](media/wpr-14.png)
18. Include both the file and the folder in your submission to Microsoft Support.

    ![Screenshot showing the details of the file and the folder.](media/wpr-15.png)

### Capture performance logs using the WPR CLI

To collect a WPR trace using the command-line tool wpr.exe:

1. Download **[Microsoft Defender for Endpoint analysis](https://github.com/YongRhee-MDE/Scripts/blob/master/MDAV.wprp)** performance trace profile as `MDAV.wprp` in a local directory such as `C:\traces`.
2. Right-click the **Start Menu** icon and select **Windows PowerShell (Admin)** or **Command Prompt (Admin)** to open an Admin command prompt window.
3. Select **Yes** in the User Account Control dialog box.
4. At the **Command Prompt (Admin)**, run the following command to start a Microsoft Defender for Endpoint performance trace:

    ```console
    
    wpr.exe -start C:\traces\MDAV.wprp!WD.Verbose -filemode
    
    ```

    Warning

    If your Windows Server has 64 GB of RAM or more, use profiles `WDForLargeServers.Light` and `WDForLargeServers.Verbose` instead of profiles `WD.Light` and `WD.Verbose`, respectively. Otherwise, your system consumes a high amount of nonpaged pool memory or buffers, leading to system instability.
5. Reproduce the issue.

    Tip

    Limit the data collection to a maximum of five minutes. Ideally, aim for two to three minutes, as a significant amount of data is being collected.
6. At the **Command Prompt (Admin)**, run the following command to start a Microsoft Defender for Endpoint performance trace:

    ```console
    wpr.exe -stop merged.etl "Timestamp when the issue was reproduced, in HH:MM:SS format" "Description of the issue" "Any error that popped up"
    ```
7. Wait until the trace is merged.
8. Include both the file and the folder in your submission to Microsoft Support.