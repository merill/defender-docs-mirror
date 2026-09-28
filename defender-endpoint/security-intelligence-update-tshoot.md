---
layout: Conceptual
title: Security Intelligence update troubleshooting from Microsoft Update source - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/security-intelligence-update-tshoot
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to troubleshoot security intelligence updates from your Microsoft Update source.
author: limwainstein
ms.author: lwainstein
ms.date: 2025-05-08T00:00:00.0000000Z
ms.topic: troubleshooting
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
ms.collection: 
ms.custom:
- partner-contribution
ms.reviewer: yongrhee
locale: en-us
document_id: 1fccfd02-6784-3f27-0541-ed8e64dee39c
document_version_independent_id: 1fccfd02-6784-3f27-0541-ed8e64dee39c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/security-intelligence-update-tshoot.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-intelligence-update-tshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/security-intelligence-update-tshoot.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 3eac49c0-d084-17df-f4bb-7427b3e84662
---

# Security Intelligence update troubleshooting from Microsoft Update source - Microsoft Defender for Endpoint | Microsoft Learn

Use this article to learn how to troubleshoot security intelligence updates for Microsoft Defender Antivirus when the first source is from Microsoft Update (formerly known as Windows Update). Follow these steps to troubleshoot issues with getting your security intelligence updates:

1. Make sure that the URLs needed for security intelligence updates are allowed thru the firewall or proxy. See the Defender for Endpoint URL spreadsheets in [Configure your network environment to ensure connectivity with Defender for Endpoint service](configure-environment).

    If you're only using Microsoft Defender Antivirus, see the **Windows Update** section in [Manage connection endpoints for Windows 11 Enterprise](/en-us/windows/privacy/manage-windows-11-endpoints).
2. Make sure that the URLs you reviewed during the previous step aren't SSL inspected. Otherwise, you might see the following error in the event log:

    ```properties
    
    Source: Windows Defender
    
    Event ID: 2001 
    
    Microsoft Defender Antivirus has encountered an error trying to update security intelligence.
    
    Error code: 0x80072ee7
    
    Error description: The server name or address could not be resolved.
    
    ```

    What is error code `0x80072ee7`?

    ```properties
    
    C:\>err 0x80072ee7
    
    # as an HRESULT: Severity: FAILURE (1), Facility: 0x7, Code 0x2ee7
    
    # for hex 0x2ee7 / decimal 12007 :
    
    ERROR_INTERNET_NAME_NOT_RESOLVED                              inetmsg.h
    
    ERROR_INTERNET_NAME_NOT_RESOLVED                              wininet.h
    
    ```
3. Make sure that the services needed for Windows Update are started. These services include:

    - Windows Update service
    - Background Intelligence Transfer Service (BITS)
4. If you're using a [Fallback order](manage-protection-updates-microsoft-defender-antivirus) policy, make sure that *Microsoft Update* (`MicrosoftUpdateServer`) is the first item in the list.
5. Gather diagnostic data from the [Microsoft Defender for Endpoint Client Analyzer tool](overview-client-analyzer).

    - If you have Microsoft Defender for Endpoint Plan 2 and access to Live Response, you can gather the diagnostic data remotely. See [Collect support logs in Microsoft Defender for Endpoint using live response](troubleshoot-collect-support-log).
    - If you have Microsoft Defender for Endpoint Plan 1 or only Microsoft Defender Antivirus, you can gather the diagnostic data using the client analyzer on Windows. See [Run the client analyzer on Windows](run-analyzer-windows).
    - If either method doesn't work for you, use Microsoft Defender Antivirus diagnostic data collection. See [Collect Microsoft Defender Antivirus diagnostic data](collect-diagnostic-data).
6. When you have your diagnostic data, convert the `WindowsUpdate.etl` logs into a human readable format by using the PowerShell command, [Get-WindowsUpdateLog](/en-us/powershell/module/windowsupdate/get-windowsupdatelog). Use that information to troubleshoot issues with security intelligence updates.