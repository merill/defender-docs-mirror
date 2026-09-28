---
layout: Conceptual
title: Go to the Action center to view and approve your automated investigation and remediation tasks - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/m365d-action-center
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Use the Action center to view details about automated investigation and approve pending actions
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1014
- autoir
- admindeeplinkDEFENDER
- sfi-ga-nochange
ms.reviewer: evaldm, isco
ai-usage: ai-assisted
locale: en-us
document_id: c1838ec3-0c11-4f5a-c746-e0314047b55c
document_version_independent_id: c1838ec3-0c11-4f5a-c746-e0314047b55c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/m365d-action-center.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: m365d-action-center
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/m365d-action-center.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: 54ccde70-5a71-58ac-c4ee-3c4cedacb459
---

# Go to the Action center to view and approve your automated investigation and remediation tasks - Microsoft Defender XDR | Microsoft Learn

Important

As of September 1, 2026, automated Investigation and Response (AIR) will no longer run as a separate investigation experience or be available for manual triggering in Microsoft Defender for Endpoint alerts and remediations.

- AIR detection and response capabilities for Defender for Endpoint are already included in Microsoft Defender for Endpoint's default antivirus protection stack and run automatically. For on-demand investigations, run a full antivirus scan as needed.
- This change applies only to Microsoft Defender for Endpoint. AIR capabilities for Defender for Office 365 remain available.

The Action center provides a "single pane of glass" experience for incident and alert tasks such as:

- Approving pending remediation actions.
- Viewing an audit log of already approved remediation actions.
- Reviewing completed remediation actions.

Because the Action center provides a comprehensive view of Microsoft Defender XDR at work, your security operations team can operate more effectively and efficiently.

## How the unified Action center works

The unified Action center ([Action center](https://security.microsoft.com/action-center)) lists pending and completed remediation actions for your devices, email & collaboration content, and identities in one location.

[![The unified Action center in the Microsoft Defender portal.](media/m3d-action-center-unified.png)](media/m3d-action-center-unified.png#lightbox)

The unified Action center brings together remediation actions across Microsoft Defender for Endpoint and Microsoft Defender for Office 365. It defines a common language for all remediation actions and provides a unified investigation experience. Your security operations team has a "single pane of glass" experience to view and manage remediation actions.

You can use the unified Action center if you have appropriate permissions and one or more of the following subscriptions:

- [Microsoft Defender for Endpoint](/en-us/defender-endpoint/microsoft-defender-endpoint)
- [Microsoft Defender for Office 365](/en-us/defender-office-365/mdo-about)
- [Microsoft Defender XDR](microsoft-365-defender)

Tip

To learn more, see [Microsoft Defender XDR prerequisites](prerequisites).

You can navigate to the list of actions pending approval in two different ways:

- Go to the [Action center in the Microsoft Defender portal](https://security.microsoft.com/action-center); or
- In the [Microsoft Defender portal](https://security.microsoft.com) homepage, in the Automated investigation & response card, select **View pending actions**.

## Use the Action center

Use the following steps to open and work with the Action center:

1. Go to [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139) and sign in.
2. In the navigation pane under **Actions and submissions**, choose **Action center**. Or, in the Automated investigation & response card in the homepage, select **View pending actions**.
3. Use the **Pending actions** and **History** tabs. The following table summarizes what you'll see on each tab:

    | Tab | Description |
    | --- | --- |
    | **Pending** | Displays a list of actions that require attention. You can approve or reject actions one at a time, or select multiple actions if they have the same type of action (like Quarantine file).  Make sure to review and approve (or reject) pending actions as soon as possible so that your automated investigations can complete in a timely manner. |
    | **History** | Serves as an audit log for actions that were taken, such as:<br>    - Remediation actions that were taken as a result of automated investigations<br>    - Remediation actions that were taken on suspicious or malicious email messages, files, or URLs<br>    - Remediation actions that were approved by your security operations team<br>    - Commands that were run and remediation actions that were applied during Live Response sessions<br>    - Remediation actions that were taken by your antivirus protection<br><br> Provides a way to undo certain actions (see [Undo completed actions](m365d-autoir-actions#undo-completed-actions)). |
4. You can customize, sort, filter, and export data in the Action center.

    [![Screenshot that shows the sort, filter, and customize capabilities of the Action center.](media/m365d-action-center/m3d-action-center-columnsfilters.png)](media/m365d-action-center/m3d-action-center-columnsfilters.png#lightbox)

    - Select a column heading to sort items in ascending or descending order.
    - Use the time period filter to view data for the past day, week, 30 days, or 6 months.
    - Choose the columns that you want to view.
    - Specify how many items to include on each page of data.
    - Use filters to view just the items you want to see.
    - Select **Export** to export results to a .csv file.

## Actions tracked in the Action center

All actions, whether they're pending approval or were already taken, are tracked in the Action center. Available actions include the following:

- Collect investigation package
- Isolate device (this action can be undone)
- Offboard machine
- Release code execution
- Release from quarantine
- Request sample
- Restrict code execution (this action can be undone)
- Run antivirus scan
- Stop and quarantine
- Contain devices from the network

In addition to remediation actions that are taken automatically as a result of [automated investigations](m365d-autoir), the Action center also tracks actions your security team has taken to address detected threats, and actions that were taken as a result of threat protection features in Microsoft Defender XDR. For more information about automatic and manual remediation actions, see [Remediation actions](m365d-remediation-actions).

## View action source details

The Action center includes an **Action source** column that tells you where each action came from. The following table describes possible **Action source** values:

| Action source value | Description |
| --- | --- |
| **Manual device action** | A manual action taken on a device. Examples include [device isolation](/en-us/defender-endpoint/respond-machine-alerts#isolate-devices-from-the-network) or [file quarantine](/en-us/defender-endpoint/respond-file-alerts#stop-and-quarantine-files). |
| **Manual email action** | A manual action taken on email. An example includes soft-deleting email messages or [remediating an email message](/en-us/defender-office-365/remediate-malicious-email-delivered-office-365). |
| **Automated device action** | An automated action taken on an entity, such as a file or process. Examples of automated actions include sending a file to quarantine, stopping a process, and removing a registry key. (See [Remediation actions in Microsoft Defender for Endpoint](/en-us/defender-endpoint/manage-auto-investigation#remediation-actions).) |
| **Automated email action** | An automated action taken on email content, such as an email message, attachment, or URL. Examples of automated actions include soft-deleting email messages, blocking URLs, and turning off external mail forwarding. (See [Remediation actions in Microsoft Defender for Office 365](/en-us/defender-office-365/air-remediation-actions).) |
| **Advanced hunting action** | Actions taken on devices or email with [advanced hunting](advanced-hunting-overview). |
| **Explorer action** | Actions taken on email content with [Explorer](/en-us/defender-office-365/threat-explorer-real-time-detections-about). |
| **Manual live response action** | Actions taken on a device with [live response](/en-us/defender-endpoint/live-response). Examples include deleting a file, stopping a process, and removing a scheduled task. |
| **Live response action** | Actions taken on a device with [Microsoft Defender for Endpoint APIs](/en-us/defender-endpoint/api/management-apis#microsoft-defender-for-endpoint-apis). Examples of actions include isolating a device, running an antivirus scan, and getting information about a file. |

## Required permissions for Action center tasks

To perform tasks, such as approving or rejecting pending actions in the Action center, you need specific permissions. You have the following options:

- [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the following Microsoft Entra roles gives users the required permissions *and* permissions for other features in Microsoft 365:

    - *Microsoft Defender for Endpoint remediation (devices)*: Membership in the **Security Administrator** role.
    - *Microsoft Defender for Office 365 remediation (Office content and email)*:

        - Membership in the **Security Administrator** role.

        *and*

        - Membership in a role group in [Email & collaboration permissions](/en-us/defender-office-365/mdo-portal-permissions) with the **Search and Purge** role assigned. By default, this role is assigned only to the **Data Investigator** and **Organization Management** role groups in Email & collaboration permissions. You can add users to those role groups, or you can [create a new role group in Email & collaboration permissions](/en-us/defender-office-365/mdo-portal-permissions#create-email--collaboration-role-groups-in-the-microsoft-defender-portal) with the **Search and Purge** role assigned, and add the users to the custom role group.
- [Email & collaboration permissions in the Microsoft Defender portal](/en-us/defender-office-365/mdo-portal-permissions):

    - *Microsoft Defender for Office 365 remediation (Office content and email)*:

        - Membership in the **Security Administrator** role group

        *and*

        - Membership in a role group in [Email & collaboration permissions](/en-us/defender-office-365/mdo-portal-permissions) with the **Search and Purge** role assigned. By default, this role is assigned only to the **Data Investigator** and **Organization Management** role groups in Email & collaboration permissions. You can add users to those role groups, or you can [create a new role group in Email & collaboration permissions](/en-us/defender-office-365/mdo-portal-permissions#create-email--collaboration-role-groups-in-the-microsoft-defender-portal) with the **Search and Purge** role assigned, and add the users to the custom role group.
- [Microsoft Defender XDR Unified role based access control (URBAC)](manage-rbac)

    - *Microsoft Defender for Endpoint remediation*: **Security operations \ Security data \ Response (manage)**.
    - *Microsoft Defender for Office 365 remediation* (Office content and email, if **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](/en-us/defender-office-365/media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell):
        - *Read access for email and Teams message headers*: **Security operations/Raw data (email & collaboration)/Email & collaboration metadata (read)**.
        - *Remediate malicious email*: **Security operations/Security data/Email & collaboration advanced actions (manage)**.

    Tip

    Membership in the **Security Administrator** role group Email & collaboration permissions doesn't grant access to the Action center or Microsoft Defender XDR capabilities. For those, you need to be a member of the **Security Administrator** role in [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal).
- [Defender for Endpoint permissions](/en-us/defender-endpoint/rbac):

    - *Microsoft Defender for Endpoint remediation (devices)*: Membership in the **Active remediation actions** role.