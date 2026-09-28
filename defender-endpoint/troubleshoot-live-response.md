---
layout: Conceptual
title: Troubleshoot Microsoft Defender for Endpoint live response issues - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-live-response
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot issues that might arise when using live response in Microsoft Defender for Endpoint.
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
ms.date: 2025-03-26T00:00:00.0000000Z
locale: en-us
document_id: 70245194-f739-5d25-ffa4-ada4b0c55dd9
document_version_independent_id: 70245194-f739-5d25-ffa4-ada4b0c55dd9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-live-response.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-live-response
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-live-response.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 12c62a83-d84b-fc2d-be3c-de461f6346d6
---

# Troubleshoot Microsoft Defender for Endpoint live response issues - Microsoft Defender for Endpoint | Microsoft Learn

This page provides detailed steps to troubleshoot live response issues.

## File can't be accessed during live response sessions

If while trying to take an action during a live response session, you encounter an error message stating that the file can't be accessed, take the following steps to address the issue.

1. Copy the following script code snippet and save it as a PS1 file:

    ```powershell
    $copied_file_path=$args[0]
    $action=Copy-Item $copied_file_path -Destination $env:TEMP -PassThru -ErrorAction silentlyContinue
    
    if ($action){
         Write-Host "You copied the file specified in $copied_file_path to $env:TEMP Successfully"
    }
    
    else{
        Write-Output "Error occurred while trying to copy a file, details:"
        Write-Output  $error[0].exception.message
    
    }
    ```
2. Add the script to the live response library.
3. Run the script with one parameter: the file path of the file to be copied.
4. Navigate to your TEMP folder.
5. Run the action you wanted to take on the copied file.

## Slow live response sessions or delays during initial connections

Live response uses Defender for Endpoint sensor registration with WNS service in Windows. If you're having connectivity issues with live response, confirm the following details:

1. WpnService (Windows Push Notifications System Service) isn't disabled.
2. WpnService connectivity with WNS cloud isn't disabled via group policy or MDM setting. ['Turn off notifications network usage'](/en-us/windows/client-management/mdm/policy-csp-notifications) shouldn't be set to `1`.

Refer to the following articles to fully understand the WpnService service behavior and requirements:

- [Windows Push Notification Services (WNS) overview](/en-us/windows/apps/develop/notifications/push-notifications/wns-overview)
- [Enterprise firewall configurations to support WNS traffic](/en-us/windows/apps/develop/notifications/push-notifications/firewall-allowlist-config)