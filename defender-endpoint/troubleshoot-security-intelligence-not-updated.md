---
layout: Conceptual
title: Troubleshoot Microsoft Defender Antivirus Security intelligence not getting updated - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-security-intelligence-not-updated
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to troubleshoot Microsoft Defender Antivirus Security intelligence not getting updated.
author: chrisda
ms.author: chrisda
ms.date: 2025-01-10T00:00:00.0000000Z
ms.topic: troubleshooting
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
ms.collection: 
ms.custom:
- partner-contribution
- sfi-image-nochange
ms.reviewer: 
locale: en-us
document_id: d7f3f9fb-fba6-eac6-6294-d0c1bbe8d303
document_version_independent_id: d7f3f9fb-fba6-eac6-6294-d0c1bbe8d303
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-security-intelligence-not-updated.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-security-intelligence-not-updated
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-security-intelligence-not-updated.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: eb91b58c-2066-ca80-7eea-be53db815a9a
---

# Troubleshoot Microsoft Defender Antivirus Security intelligence not getting updated - Microsoft Defender for Endpoint | Microsoft Learn

## Symptom

When you update Microsoft Defender Antivirus security intelligence, you might see the error **Protection definition update failed**.

![Screenshot of Protection definition update failed.](media/protection-definition-update-failed.png)

These error codes might also appear:

- 0x8024402c
- 0x80240022
- 0X80004002
- 0x80070422
- 0x80072efd
- 0x80070005
- 0x80072f78
- 0x80072ee2
- 0x8007001B

The following screenshot shows the error **Signature Update failed**.

[![Screenshot showing signature update failed.](media/signature-update-failed.png)](media/signature-update-failed.png#lightbox)

## Solution

1. Check the URLs required for the Security intelligence updates. You can get them via the firewall and/or proxy. See [Configure your network environment to ensure connectivity with Defender for Endpoint service](configure-environment).
2. Verify that Microsoft Defender Antivirus is your primary antivirus. If you have a non-Microsoft antivirus solution that uses the Windows Security Center (WSC) API, it disables Microsoft Defender Antivirus. When Microsoft Defender Antivirus is disabled, updates can't occur.
3. If Microsoft Defender Antivirus is the primary antivirus and the services are running, follow these steps:

    1. Verify you can manually update Security Intelligence manually by downloading and installing updates from https://www.microsoft.com/wdsi/defenderupdates.
    2. If manual updates work, try updating through the Microsoft Malware Protection Center (MMPC).

        1. In an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**), run the following commands.

            Tip

            The first command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, it goes to `%ProgramFiles%\Microsoft Defender`.

            ```dos
            (set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1
            
            MpCmdRun.exe -SignatureUpdate -MMPC
            ```

            For more information, see [Manage the sources for Microsoft Defender Antivirus protection updates](manage-protection-updates-microsoft-defender-antivirus).
    3. If The MpCmdRun command works, the issue might caused by one of the following issues:

        - The Security intelligence [fallback order](manage-protection-updates-microsoft-defender-antivirus#fallback-order) is set to a WSUS server without **Security intelligence** approved updates.

            Review `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\WUServer (REG_SZ)`. Once you find the WUServer, verify that WSUS server has the MDAV security intelligence [(KB2267602 for MDAV and KB2461484 for SCEP)](microsoft-defender-antivirus-updates#security-intelligence-updates) approved.
        - The specified UNC share might be stale.

            Review [Manage how and where Microsoft Defender Antivirus receives updates](manage-protection-updates-microsoft-defender-antivirus#create-a-unc-share-for-security-intelligence).
        - The Windows Update service is having issues.

            Review [Guidance for troubleshooting Windows Update issues](/en-us/troubleshoot/windows-client/installing-updates-features-roles/troubleshoot-windows-update-issues) and [Troubleshoot problems updating Windows](https://support.microsoft.com/Windows/Deployment/Updates-Lifecycle/troubleshoot-problems-updating-windows).