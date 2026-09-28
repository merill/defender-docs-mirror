---
layout: Conceptual
title: Manage the live response file library in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-libraries-live-response
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use Microsoft Defender for Endpoint to configure libraries for live response.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 841c6967-6846-b53f-3c99-e8500153ee00
document_version_independent_id: 841c6967-6846-b53f-3c99-e8500153ee00
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-libraries-live-response.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-libraries-live-response
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-libraries-live-response.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 7c4a4041-de5b-4774-6d3e-abcfdb09f1f1
---

# Manage the live response file library in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

The **Library management** page in the Microsoft Defender portal allows you to manage files used during Microsoft Defender for Endpoint live response sessions. You can also add, view, and delete files in the library, instead of uploading them during a live response session.

The **Library management** page describes how to view, add, and manage files in the live response library.

For more information about live response, see [Investigate entities on devices using live response](live-response).

## View the list of files

The **Library management** page shows a list of files used during live response sessions on your endpoints.

[![Screenshot of the library management page - viewing details for a file](media/configure-libraries-live-response/library-management-view-all-files.png)](media/configure-libraries-live-response/library-management-view-all-files.png#lightbox)

To view the list of files available for live response:

1. In the Microsoft Defender portal, navigate to **Settings** &gt; **Endpoints** &gt; **Library management**.
2. Review the following information for each file:
    - **Name**: The name of the file.
    - **Type**: The file extension, representing the file type.
    - **Created by**: The user who uploaded the file.
    - **Creation date**: The date the file was uploaded.
    - **Updated by**: The user who last updated the file.
    - **Last updated date**: The date the file was last updated.
    - **Has parameters**: Indicates whether the file has parameters that can be configured during a live response session.
    - **Parameters description**: A description of the parameters for the file.

## Upload files

To add a new file for live response:

1. Select **Upload** from the menu.
2. In the **Upload file to library** page, select **Upload file to library** on the right.

    The file name is displayed in the **File content** field.
3. In the **File description** field, optionally type a description for the file.
4. If you're uploading an updated version of an existing file, select **Overwrite file**. This replaces the existing file with the new version.
5. To add a description for the parameters of the file, select **File parameters**, and in the **Parameters description** field, type a description.
6. Select **Submit** to upload the file.

    The file is visible in the list of files. You can now use this file during live response sessions.

## View file details

To view a file's details, select **View details** from the menu, or right-click the file, and select **View details**. A detailed pane opens, displaying information about the file, including its parameters and usage history.

![Screenshot of the library management page - viewing file details](media/configure-libraries-live-response/library-management-file-details.png)

## View and analyze files

Note

You need a [Microsoft Security Copilot license](https://www.microsoft.com/security/pricing/microsoft-security-copilot) to analyze files. Without this license, you can only view files.

To view and analyze a file:

1. Right-click the file and select **View file** or double-click the file row.
2. Select **Download** to download the file, or **Analyze** to open Copilot script analysis.

    The analysis describes what the script does, including its methods and output.

    [![Screenshot of the library management page - view and analyze a file](media/configure-libraries-live-response/library-management-view-analyze-file.png)](media/configure-libraries-live-response/library-management-view-analyze-file.png#lightbox)

## Manage files in the library

The library provides options to Upload, Refresh, View details, View file, Analyze, Download, Delete, and Filter files:

| Option | Description | Available from |
| --- | --- | --- |
| **Upload** | Upload a new file or an updated version of an existing file. | Top menu |
| **Refresh** | Refresh the list of files to see the most up-to-date information. | Top menu |
| **View details** | View detailed information about a selected file. | Top menu, right-click menu |
| **View file** | View the file's contents. | Top menu, right-click menu |
| **Analyze** | Analyze a file to get a description of the actions the script takes. | View file window |
| **Download** | Download a selected file to your local device. | Top menu, right-click menu, view file window |
| **Delete** | Remove a selected file from the list. | Top menu, right-click menu |
| **Filter** | Filter the list of files based on specific criteria, such as type or creation date. | Top menu |

## View audit logs for library management actions

Library management actions are tracked in the Microsoft Defender [audit log](/en-us/defender-xdr/microsoft-xdr-auditing). Defender tracks actions such as upload, download, delete, or listing files, and you can view details on these actions in the audit log. This provides visibility into how library files are managed across your organization.

To view audit logs for library management actions:

1. In the Microsoft Defender portal, select **Settings** &gt; **Audit**.
2. Search for audit logs using the following criteria:

    - **Activities - friendly names**: **Ran live response session**
    - **Record Types**: **MSDEResponseActions**

    [![Screenshot of the audit log search criteria for library management actions](media/configure-libraries-live-response/library-management-audit-search.png)](media/configure-libraries-live-response/library-management-audit-search.png#lightbox)
3. Review the results to see the library management actions performed, including the user, timestamp, and a description of the action. For example, the action description may be: **Library management - downloaded file** or **Library management - created file**, with specific details about the file involved in the action.

    [![Screenshot of the audit log showing library management actions](media/configure-libraries-live-response/library-management-audit-result.png)](media/configure-libraries-live-response/library-management-audit-result.png#lightbox)