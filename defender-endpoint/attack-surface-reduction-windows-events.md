---
layout: Conceptual
title: Attack surface reduction events in Windows Event Viewer - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/attack-surface-reduction-windows-events
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Create custom views in Windows Event Viewer to review events from attack surface reduction rules, controlled folder access, exploit protection, and network protection.
author: chrisda
ms.author: chrisda
ms.service: defender-endpoint
ms.subservice: asr
ms.topic: how-to
ms.collection:
- m365-security
- tier2
- mde-asr
ms.custom: msecd-doc-authoring-1016
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 017e6a13-707f-dd8c-ca19-8f4c903636f6
document_version_independent_id: 017e6a13-707f-dd8c-ca19-8f4c903636f6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/attack-surface-reduction-windows-events.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: attack-surface-reduction-windows-events
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/attack-surface-reduction-windows-events.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 2219b5a4-3267-0c4b-7292-08c3e3d70c0e
---

# Attack surface reduction events in Windows Event Viewer - Microsoft Defender for Endpoint | Microsoft Learn

Reviewing events in Event Viewer is useful when you evaluate attack surface reduction features. For example, you can enable audit mode for features or settings, and then review what would happen if they were fully enabled. You can also view the effects of attack surface reduction features when they're fully enabled.

This article describes how to use [Windows Event Viewer](/en-us/training/modules/manage-monitor-event-logs/) to view events from attack surface reduction (ASR) capabilities, including:

- [Attack surface reduction rules](attack-surface-reduction-rules-overview)
- [Controlled folder access (CFA)](controlled-folder-access-overview)
- [Exploit protection](exploit-protection)
- [Network protection](network-protection)

To view attack surface reduction events, you have the following options as explained in the rest of this article:

- Browse attack surface reduction events in Windows Event Viewer: How to navigate to attack surface reduction events in Event Viewer, and the event IDs for each attack surface reduction capability.
- Use custom views in Windows Event Viewer to view attack surface reduction events: How to create or import custom views to filter Event Viewer for specific ASR capabilities, and ready-to-use XML query templates.

Tip

You can use [Windows Event Forwarding](/en-us/windows/security/operating-system-security/device-management/use-windows-event-forwarding-to-assist-in-intrusion-detection) to centralize attack surface reduction event collection from multiple devices.

The Microsoft Defender portal also provides reporting for attack surface reduction features that's easier to use than Windows Event Viewer:

- [Attack surface reduction (ASR) rules report](attack-surface-reduction-rules-report)
- [Controlled folder access report](controlled-folder-access-overview)
- [Exploit protection report](exploit-protection)
- [Network protection report](network-protection)

## Browse attack surface reduction events in Windows Event Viewer

All attack surface reduction events are located in **Applications and Services Logs**. To view attack surface reduction events, do the following steps:

1. Select **Start**, type **Event Viewer**, and then press **Enter** to open Event Viewer.
2. In Event Viewer, expand **Applications and Services Logs** &gt; **Microsoft** &gt; **Windows**.
3. Continue to expand the path for ASR rule events, controlled folder access events, exploit protection events, or network protection events.
4. Find and filter the events you want to see by using the event ID tables in the ASR rule events, controlled folder access events, exploit protection events, and network protection events sections, or by creating custom views in Event Viewer.

### ASR rule events

ASR rule events are located in the **Windows Defender** &gt; **Operational** log:

| Event ID | Description |
| --- | --- |
| 1121 | Event when rule fires in block mode |
| 1122 | Event when rule fires in audit mode |
| 1129 | Event when user overrides block in warn mode |
| 5007 | Event when settings are changed |

### View controlled folder access events

Controlled folder access events are located in **Windows Defender** &gt; **Operational**.

| Event ID | Description |
| --- | --- |
| 5007 | Event when settings are changed |
| 1124 | Audited controlled folder access event |
| 1123 | Blocked controlled folder access event |
| 1127 | Blocked controlled folder access sector write block event |
| 1128 | Audited controlled folder access sector write block event |

### View exploit protection events

The following exploit protection events are located in the **Security-Mitigations** &gt; **Kernel Mode** and **Security-Mitigations** &gt; **User Mode** logs:

| Event ID | Description |
| --- | --- |
| 1 | ACG audit |
| 2 | ACG enforce |
| 3 | Don't allow child processes audit |
| 4 | Don't allow child processes block |
| 5 | Block low integrity images audit |
| 6 | Block low integrity images block |
| 7 | Block remote images audit |
| 8 | Block remote images block |
| 9 | Disable win32k system calls audit |
| 10 | Disable win32k system calls block |
| 11 | Code integrity guard audit |
| 12 | Code integrity guard block |
| 13 | EAF audit |
| 14 | EAF enforce |
| 15 | EAF+ audit |
| 16 | EAF+ enforce |
| 17 | IAF audit |
| 18 | IAF enforce |
| 19 | ROP StackPivot audit |
| 20 | ROP StackPivot enforce |
| 21 | ROP CallerCheck audit |
| 22 | ROP CallerCheck enforce |
| 23 | ROP SimExec audit |
| 24 | ROP SimExec enforce |

The following exploit protection event is located in the **WER-Diagnostics** &gt; **Operational** log:

| Event ID | Description |
| --- | --- |
| 5 | CFG Block |

The following exploit protection event is located in the **Win32k** &gt; **Operational** log:

| Event ID | Description |
| --- | --- |
| 260 | Untrusted Font |

### View network protection events

Network protection events are located in **Windows Defender** &gt; **Operational**.

| Event ID | Description |
| --- | --- |
| 5007 | Event when settings are changed |
| 1125 | Event when network protection fires in audit mode |
| 1126 | Event when network protection fires in block mode |

## Use custom views in Windows Event Viewer to view attack surface reduction events

You can create custom views in Windows Event Viewer to see only the events for specific attack surface reduction capabilities. The easiest way is to import a custom view as an XML file. You can also copy the XML directly into Event Viewer.

For ready-to-use XML templates, see the Custom XML templates for attack surface reduction events section.

### Import an existing XML custom view

To import an existing XML custom view into Event Viewer, complete the following steps:

1. Create an empty .txt file and copy the XML for the custom view you want to use into the .txt file. Do this step for each of the custom views you want to use. Rename the files as follows (ensure you change the type from .txt to .xml):

    - Controlled folder access events custom view: *cfa-events.xml*
    - Exploit protection events custom view: *ep-events.xml*
    - Attack surface reduction events custom view: *asr-events.xml*
    - Network protection events custom view: *np-events.xml*
2. Select **Start**, type **Event Viewer**, and then press **Enter** to open Event Viewer.
3. Select **Action** &gt; **Import Custom View...**

![Animation showing how to select and import a saved XML file as a custom view in Event Viewer.](media/events-import.gif)
4. Navigate to the XML file for the custom view you want and select it.
5. Select **Open**.

The custom view filters to show only the events related to the selected attack surface reduction capability.

### Copy XML directly into Event Viewer

To paste XML directly into a custom view, complete the following steps:

1. Select **Start**, type **Event Viewer**, and then press **Enter** to open Event Viewer.
2. In the **Actions** pane, select **Create Custom View...**
3. Go to the XML tab. Note that if you select **Edit query manually**, you can't edit the query later by using the **Filter** tab. Select **Edit query manually**, and then select **Yes** to confirm.
4. Paste the XML code for attack surface reduction rules, controlled folder access, exploit protection, or network protection from the custom XML templates into the XML section.
5. Select **OK**. Specify a name for your filter. The custom view filters to show only the events related to the selected attack surface reduction capability.

### Custom XML templates for attack surface reduction events

Use the following XML templates to create custom views in Event Viewer for each attack surface reduction capability. You can import these templates as XML files or paste them directly into Event Viewer.

#### XML for attack surface reduction rule events

The following XML query filters the Windows Defender Operational log for ASR rule events (event IDs 1121, 1122, 1129, and 5007):

```xml
<QueryList>
  <Query Id="0" Path="Microsoft-Windows-Windows Defender/Operational">
   <Select Path="Microsoft-Windows-Windows Defender/Operational">*[System[(EventID=1121 or EventID=1122 or EventID=1129 or EventID=5007)]]</Select>
   <Select Path="Microsoft-Windows-Windows Defender/WHC">*[System[(EventID=1121 or EventID=1122 or EventID=1129 or EventID=5007)]]</Select>
  </Query>
</QueryList>
```

#### XML for controlled folder access events

The following XML query filters the Windows Defender Operational log for controlled folder access events (event IDs 1123, 1124, 1127, 1128, and 5007):

```xml
<QueryList>
  <Query Id="0" Path="Microsoft-Windows-Windows Defender/Operational">
   <Select Path="Microsoft-Windows-Windows Defender/Operational">*[System[(EventID=1123 or EventID=1124 or EventID=1127 or EventID=1128 or EventID=5007)]]</Select>
   <Select Path="Microsoft-Windows-Windows Defender/WHC">*[System[(EventID=1123 or EventID=1124 or EventID=1127 or EventID=1128 or EventID=5007)]]</Select>
  </Query>
</QueryList>
```

#### XML for exploit protection events

The following XML query creates a custom view for exploit protection events across the Security-Mitigations, WER-Diagnostics, and Win32k providers (event IDs 1–24, 5, and 260):

```xml
<QueryList>
  <Query Id="0" Path="Microsoft-Windows-Security-Mitigations/KernelMode">
   <Select Path="Microsoft-Windows-Security-Mitigations/KernelMode">*[System[Provider[@Name='Microsoft-Windows-Security-Mitigations' or @Name='Microsoft-Windows-WER-Diag' or @Name='Microsoft-Windows-Win32k' or @Name='Win32k'] and ( (EventID &gt;= 1 and EventID &lt;= 24)  or EventID=5 or EventID=260)]]</Select>
   <Select Path="Microsoft-Windows-Win32k/Concurrency">*[System[Provider[@Name='Microsoft-Windows-Security-Mitigations' or @Name='Microsoft-Windows-WER-Diag' or @Name='Microsoft-Windows-Win32k' or @Name='Win32k'] and ( (EventID &gt;= 1 and EventID &lt;= 24)  or EventID=5 or EventID=260)]]</Select>
   <Select Path="Microsoft-Windows-Win32k/Contention">*[System[Provider[@Name='Microsoft-Windows-Security-Mitigations' or @Name='Microsoft-Windows-WER-Diag' or @Name='Microsoft-Windows-Win32k' or @Name='Win32k'] and ( (EventID &gt;= 1 and EventID &lt;= 24)  or EventID=5 or EventID=260)]]</Select>
   <Select Path="Microsoft-Windows-Win32k/Messages">*[System[Provider[@Name='Microsoft-Windows-Security-Mitigations' or @Name='Microsoft-Windows-WER-Diag' or @Name='Microsoft-Windows-Win32k' or @Name='Win32k'] and ( (EventID &gt;= 1 and EventID &lt;= 24)  or EventID=5 or EventID=260)]]</Select>
   <Select Path="Microsoft-Windows-Win32k/Operational">*[System[Provider[@Name='Microsoft-Windows-Security-Mitigations' or @Name='Microsoft-Windows-WER-Diag' or @Name='Microsoft-Windows-Win32k' or @Name='Win32k'] and ( (EventID &gt;= 1 and EventID &lt;= 24)  or EventID=5 or EventID=260)]]</Select>
   <Select Path="Microsoft-Windows-Win32k/Power">*[System[Provider[@Name='Microsoft-Windows-Security-Mitigations' or @Name='Microsoft-Windows-WER-Diag' or @Name='Microsoft-Windows-Win32k' or @Name='Win32k'] and ( (EventID &gt;= 1 and EventID &lt;= 24)  or EventID=5 or EventID=260)]]</Select>
   <Select Path="Microsoft-Windows-Win32k/Render">*[System[Provider[@Name='Microsoft-Windows-Security-Mitigations' or @Name='Microsoft-Windows-WER-Diag' or @Name='Microsoft-Windows-Win32k' or @Name='Win32k'] and ( (EventID &gt;= 1 and EventID &lt;= 24)  or EventID=5 or EventID=260)]]</Select>
   <Select Path="Microsoft-Windows-Win32k/Tracing">*[System[Provider[@Name='Microsoft-Windows-Security-Mitigations' or @Name='Microsoft-Windows-WER-Diag' or @Name='Microsoft-Windows-Win32k' or @Name='Win32k'] and ( (EventID &gt;= 1 and EventID &lt;= 24)  or EventID=5 or EventID=260)]]</Select>
   <Select Path="Microsoft-Windows-Win32k/UIPI">*[System[Provider[@Name='Microsoft-Windows-Security-Mitigations' or @Name='Microsoft-Windows-WER-Diag' or @Name='Microsoft-Windows-Win32k' or @Name='Win32k'] and ( (EventID &gt;= 1 and EventID &lt;= 24)  or EventID=5 or EventID=260)]]</Select>
   <Select Path="System">*[System[Provider[@Name='Microsoft-Windows-Security-Mitigations' or @Name='Microsoft-Windows-WER-Diag' or @Name='Microsoft-Windows-Win32k' or @Name='Win32k'] and ( (EventID &gt;= 1 and EventID &lt;= 24)  or EventID=5 or EventID=260)]]</Select>
   <Select Path="Microsoft-Windows-Security-Mitigations/UserMode">*[System[Provider[@Name='Microsoft-Windows-Security-Mitigations' or @Name='Microsoft-Windows-WER-Diag' or @Name='Microsoft-Windows-Win32k' or @Name='Win32k'] and ( (EventID &gt;= 1 and EventID &lt;= 24)  or EventID=5 or EventID=260)]]</Select>
  </Query>
</QueryList>
```

#### XML for network protection events

The following XML query filters the Windows Defender Operational log for network protection events (event IDs 1125, 1126, and 5007):

```xml
<QueryList>
 <Query Id="0" Path="Microsoft-Windows-Windows Defender/Operational">
  <Select Path="Microsoft-Windows-Windows Defender/Operational">*[System[(EventID=1125 or EventID=1126 or EventID=5007)]]</Select>
  <Select Path="Microsoft-Windows-Windows Defender/WHC">*[System[(EventID=1125 or EventID=1126 or EventID=5007)]]</Select>
 </Query>
</QueryList>
```