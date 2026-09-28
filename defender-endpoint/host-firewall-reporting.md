---
layout: Conceptual
title: Host firewall reporting in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/host-firewall-reporting
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Host and view firewall reporting in Microsoft Defender portal.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.date: 2025-12-18T00:00:00.0000000Z
ms.topic: concept-article
author: paulinbar
ms.author: painbar
ms.subservice: asr
ms.collection:
- m365-security
- tier2
- mde-asr
ms.custom:
- admindeeplinkDEFENDER
- sfi-image-nochange
locale: en-us
document_id: 57ed5ab0-a156-0e66-6f40-c559184b86ad
document_version_independent_id: 57ed5ab0-a156-0e66-6f40-c559184b86ad
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/host-firewall-reporting.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: host-firewall-reporting
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/host-firewall-reporting.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: bb75ffcc-7314-3177-69f4-3dcd31f76403
---

# Host firewall reporting in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Firewall reporting in the [Microsoft Defender portal](https://security.microsoft.com) enables you to view Windows firewall reporting from a centralized location.

## What do you need to know before you begin?

- You open the Microsoft Defender portal at https://security.microsoft.com. To go directly to the **Firewall** page, use https://security.microsoft.com/firewall.
- You need to be assigned permissions before you can do the procedures in this article. In [Microsoft Entra ID](/en-us/entra/identity/role-based-access-control/manage-roles-portal) you need to be a member of the **Global Administrator**^\*^ or **Security Administrator** roles.

    Important

    ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.
- Your devices must be running Windows 10 or later, or Windows Server 2012 R2 or later. For Windows Server 2012 R2 and Windows Server 2016 to appear in firewall reports, these devices must be onboarded using the modern unified solution package. For more information, see [New functionality in the modern unified solution for Windows Server 2012 R2 and 2016](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2).
- To onboard devices to the Microsoft Defender for Endpoint service, see [onboarding guidance](onboard-configure).
- For the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139) to start receiving data, you must enable **Audit Events** for Windows Defender Firewall with Advanced Security. See the following articles:

    - [Audit Filtering Platform Packet Drop](/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/audit-filtering-platform-packet-drop)
    - [Audit Filtering Platform Connection](/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/audit-filtering-platform-connection)
- Enable these events by using Group Policy Object Editor, Local Security Policy, or the auditpol.exe commands. For more information, see [documentation about auditing and logging](/en-us/windows/win32/fwp/auditing-and-logging). The two PowerShell commands are as follows:

    - `auditpol /set /subcategory:"Filtering Platform Packet Drop" /failure:enable`
    - `auditpol /set /subcategory:"Filtering Platform Connection" /failure:enable`

    Here's an example query:

    ```powershell
    param (
        [switch]$remediate
    )
    try {
    
        $categories = "Filtering Platform Packet Drop,Filtering Platform Connection"
        $current = auditpol /get /subcategory:"$($categories)" /r | ConvertFrom-Csv    
        if ($current."Inclusion Setting" -ne "failure") {
            if ($remediate.IsPresent) {
                Write-Host "Remediating. No Auditing Enabled. $($current | ForEach-Object {$_.Subcategory + ":" + $_.'Inclusion Setting' + ";"})"
                $output = auditpol /set /subcategory:"$($categories)" /failure:enable
                if($output -eq "The command was successfully executed.") {
                    Write-Host "$($output)"
                    exit 0
                }
                else {
                    Write-Host "$($output)"
                    exit 1
                }
            }
            else {
                Write-Host "Remediation Needed. $($current | ForEach-Object {$_.Subcategory + ":" + $_.'Inclusion Setting' + ";"})."
                exit 1
            }
        }
    
    }
    catch {
        throw $_
    } 
    ```

## The process

Note

Make sure to follow the instructions from previous the section and properly configure your devices to participate in the preview program.

- After events are enabled, Microsoft Defender for Endpoint begins to monitor data, which includes:

    - Remote IP
    - Remote Port
    - Local Port
    - Local IP
    - Computer Name
    - Process across inbound and outbound connections
- Admins can now see Windows host firewall activity [here](https://security.microsoft.com/firewall). Additional reporting can be facilitated by downloading the [Custom Reporting script](https://github.com/microsoft/MDATP-PowerBI-Templates/tree/master/Firewall) to monitor the Windows Defender Firewall activities using Power BI.

    It can take up to 12 hours before the data is reflected.

## Supported scenarios

- Firewall reporting
- From "Computers with a blocked connection" to device (requires Defender for Endpoint Plan 2)
- Drill into advanced hunting (preview refresh) (requires Defender for Endpoint Plan 2)

### Firewall reporting

Here are some examples of the firewall report pages in the [Microsoft Defender portal](https://security.microsoft.com). The **Firewall** page contains the **Inbound**, **Outbound**, and **App** tabs. You access this page at **Reports** &gt; **Endpoints** section &gt; **Firewall** or directly at https://security.microsoft.com/firewall.

[![The Host firewall reporting page](media/host-firewall-reporting-page.png)](media/host-firewall-reporting-page.png#lightbox)

### From "Computers with a blocked connection" to device

Note

This feature requires Defender for Endpoint Plan 2.

Cards support interactive objects. You can drill into the activity of a device by clicking on the device name, which will launch the Microsoft Defender portal in a new tab, and take you directly to the **Device Timeline** tab.

[![The Computers with a blocked connection page](media/firewall-reporting-blocked-connection.png)](media/firewall-reporting-blocked-connection.png#lightbox)

You can now select the **Timeline** tab, which will give you a list of events associated with that device.

After clicking on the **Filters** button on the upper right-hand corner of the viewing pane, select the type of event you want. In this case, select **Firewall events** and the pane will be filtered to Firewall events.

[![The Filters button](media/firewall-reporting-filters-button.png)](media/firewall-reporting-filters-button.png#lightbox)

### Drill into advanced hunting (preview refresh)

Note

This feature requires Defender for Endpoint Plan 2.

Firewall reports support drilling from the card directly into **Advanced Hunting** by clicking the **Open Advanced hunting** button. The query is prepopulated.

[![The Open Advanced hunting button](media/firewall-reporting-advanced-hunting.png)](media/firewall-reporting-advanced-hunting.png#lightbox)

The query can now be executed, and all related Firewall events from the last 30 days can be explored.

For more reporting, or custom changes, the query can be exported into Power BI for further analysis. Custom reporting can be facilitated by downloading the [Custom Reporting script](https://github.com/microsoft/MDATP-PowerBI-Templates/tree/master/Firewall) to monitor the Windows Defender Firewall activities using Power BI.