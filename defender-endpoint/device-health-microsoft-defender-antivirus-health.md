---
layout: Conceptual
title: Device health Microsoft Defender Antivirus health report - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/device-health-microsoft-defender-antivirus-health
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use the Microsoft Defender Antivirus report to track antivirus status and Microsoft Defender Antivirus engine, intelligence, and platform versions.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.date: 2025-04-08T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
- mde-ngp
ms.topic: article
ms.subservice: ngp
ms.reviewer: mkaminska, yongrhee
ms.custom:
- sfi-ga-nochange
- sfi-image-nochange
locale: en-us
document_id: b1fca5b5-1e0d-4c21-e2b7-41910bb48d60
document_version_independent_id: b1fca5b5-1e0d-4c21-e2b7-41910bb48d60
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/device-health-microsoft-defender-antivirus-health.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: device-health-microsoft-defender-antivirus-health
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/device-health-microsoft-defender-antivirus-health.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 8ae0ce8a-5e4f-846b-64aa-67f3b5bef47e
---

# Device health Microsoft Defender Antivirus health report - Microsoft Defender for Endpoint | Microsoft Learn

- [Microsoft Defender for Business](/en-us/defender-business/mdb-overview)

The Device Health report provides information about the devices in your organization. The report includes trending information showing the antivirus status and Microsoft Defender Antivirus engine, intelligence, and platform versions.

Important

For devices to appear **correctly** in Microsoft Defender Antivirus device health reports, they must meet the following prerequisites:

- Device is onboarded to Microsoft Defender for Endpoint
- OS: Windows 10, Windows 11, Windows Server 2012 R2 or later (not onboarded via Microsoft Management Agent), macOS, Linux
- Sense (MsSense.exe) version: **10.8210.** \*+.

**OS build dependency (Windows 10 2016 LTSB / 1607):** On older Windows editions, the Microsoft Defender for Endpoint sensor (MsSense.exe) version is **tied to the OS build and can't be upgraded independently**.

- **Windows 10 2016 LTSB (1607)** uses **MsSense.exe 10.1407.\*** and cannot reach **10.8210+** without upgrading Windows to a newer build.
- On these devices, Defender Antivirus health fields (for example **engine** or **platform** version) may appear as **"Unknown"** in the report. This is **expected behavior** when the Sense prerequisite isn't met.
- To get complete Defender Antivirus health reporting, upgrade the device to a newer supported Windows build that includes a Sense version meeting the requirement.

For Windows Server 2012 R2 and Windows Server 2016 to appear in device health reports, these devices must be onboarded using the modern unified solution package. For more information, see [New functionality in the modern unified solution for Windows Server 2012 R2 and 2016](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2).

## View device health cards

In the Microsoft Defender portal, in the navigation pane, select **Reports**, and then open **Device health and compliance**. The **Microsoft Defender Antivirus health** tab has eight cards that report on the following aspects of Microsoft Defender Antivirus:

- Device health, Microsoft Defender Antivirus health report
    - View device health cards
    - Report access permissions
    - Microsoft Defender Antivirus health tab
        - Card functionality
            - New Microsoft Defender Antivirus filter definitions
            - Export report
                - Top level export
        - Microsoft Defender Antivirus version and update cards functionality
            - Full report
        - Card descriptions
            - Antivirus mode card
            - Recent antivirus scan results card
            - Antivirus engine version card
            - Antivirus security intelligence version card
                - Antivirus platform version card
            - Up-to-date cards
                - Up-to-date definitions
                - Antivirus engine updates card
            - Antivirus platform updates card
                - Security intelligence updates card
    - See also

## Report access permissions

To access the Device health and antivirus compliance report in the Microsoft Defender portal, the following permissions are required:

| Permission name | Permission type |
| --- | --- |
| View Data | Threat and vulnerability management (TVM) |

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

To assign permissions, follow these steps:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com) using account with Security administrator or Global administrator role assigned.
2. In the navigation pane, select **Settings** &gt; **Endpoints** &gt; **Roles** (under **Permissions**).
3. Select the role you'd like to edit.
4. Select **Edit**.
5. In **Edit role**, on the **General** tab, in **Role name**, type a name for the role.
6. In **Description** type a brief summary of the role.
7. In **Permissions**, select **View Data**, and under **View Data** select **Threat and vulnerability management** (TVM).

For more information about user role management, see [Create and manage roles for role-based access control](user-roles).

## Microsoft Defender Antivirus health tab

The Microsoft Defender Antivirus health tab contains eight cards that report on several aspects of Microsoft Defender Antivirus in your organization:

Two cards, Antivirus mode card and Recent antivirus scan results card, report about Microsoft Defender Antivirus functions.

The remaining six cards report about the Microsoft Defender Antivirus status for devices in your organization:

| `version`cards: | `update`cards |
| --- | --- |
| Antivirus engine version cardAntivirus security intelligence version cardAntivirus platform version card | Antivirus engine updates cardSecurity intelligence updates cardAntivirus platform updates card |
| The three version cards provide flyout reports that provide additional information, and enable further exploration. | The three up-to-date reporting cards provide links to resources to learn more. |

For the three `updates` cards (also known as up-to-date reporting cards), "**No data available**" (or "Unknown" value) indicates devices that aren't reporting update status. Devices that aren't reporting update status can be due to various reasons, such as:

- Computer is disconnected from the network.
- Computer is powered down or in a hibernation state.
- Microsoft Defender Antivirus is disabled.
- Device is a Mac device.
- Cloud protection isn't enabled.
- Device doesn't meet pre-requisites for Antivirus engine or platform version.

[![Shows the Microsoft Defender Antivirus Health tab.](media/device-health-defender-antivirus-health-tab.png)](media/device-health-defender-antivirus-health-tab.png#lightbox)

### Card functionality

The functionality is essentially the same for all cards. By clicking on a numbered bar in any of the cards, the **Microsoft Defender Antivirus details** flyout opens enabling you to review information about all the devices configured with the version number of an aspect on that card.

[![Shows the Microsoft Defender Antivirus details flyout.](media/device-health-defender-antivirus-health-antivirus-details.png)](media/device-health-defender-antivirus-health-antivirus-details.png#lightbox)

If the version number that you clicked on is:

- A current version, then **Remediation required** and **Security recommendation** aren't present.
- An outdated version, a notification at the top of the report is present, indicating **Remediation required**, and a **Security recommendation** link is present. Select the security recommendation link to navigate to the threat and vulnerability management console, which can recommend appropriate antivirus updates.

To add or remove specific types of information on the **Microsoft Defender Antivirus details** flyout, select **Customize Columns**. In **Customize Columns**, select or clear items to specify what you want included in the Microsoft Defender Antivirus details report.

[![Shows custom column options for Microsoft Defender Antivirus health reporting.](media/device-health-defender-antivirus-engine-version-details-custom-columns.png)](media/device-health-defender-antivirus-engine-version-details-custom-columns.png#lightbox)

#### New Microsoft Defender Antivirus filter definitions

The following table contains a list of terms that are new to Microsoft Defender Antivirus reporting.

| Column name | Description |
| --- | --- |
| Security intelligence publish time | Indicates Microsoft's release date of the security intelligence update version on the device. Devices with a security intelligence publish time greater than seven days are considered out of date in the reports. |
| Last seen | Indicates date when device last had connection. |
| Data refresh timestamp | Indicates when client events were last received for reporting on: AV mode, AV engine version, AV platform version, AV security intelligence version, and scan information. |
| Signature refresh time | Indicates when client events were last received for reporting on engine, platform, and signature up to date status. |

Within the flyout: clicking on the name of the device will redirect you to the "Device page" for that device, where you can access detailed reports.

#### Export report

There are two levels of reports that you can export:

##### Top level export

There are two different export csv functionalities through the portal:

- **Top level export**. You can use the top-level **Export** button to gather an all-up Microsoft Defender Antivirus health report (500-K limit).

    [![Screenshot that shows the top-level export report button.](media/device-health-defender-antivirus-health-tab-export.png)](media/device-health-defender-antivirus-health-tab-export.png#lightbox)
- **Flyout level export**. You can use the **Export** button within the flyouts to export a report to an Excel spreadsheet (100-K limit).

Exported reports capture information based on your entry point into the details report and which filters or customized columns you have set.

For information on exporting using API, see the following articles:

- [Export device antivirus health report](api/device-health-export-antivirus-health-report-api)
- [Export device antivirus health details API methods and properties](api/device-health-api-methods-properties)

Important

Currently, only the [Antivirus Health JSON Response](api/device-health-api-methods-properties#13-export-device-antivirus-health-details-api-properties-json-response) is generally available. [Antivirus Health API via files](api/device-health-api-methods-properties#14-export-device-antivirus-health-details-api-properties-via-files) is only available in public preview.

[Advanced Hunting custom query](api/run-advanced-query-api) is currently only available in public preview, even if the queries are visible.

### Microsoft Defender Antivirus version and update cards functionality

Following are descriptions for the six cards that report about the `version` and `update` information for Microsoft Defender Antivirus engine, security intelligence, and platform components:

#### Full report

In any of the three `version` cards, select **View full report** to display the nine most recent Microsoft Defender Antivirus `version` reports for each of the three device types: Windows, Mac, and Linux; if fewer than nine exist, they're all shown. An **Other** category captures recent antivirus engine versions ranking tenth and below, if detected.

[![Shows the distribution of the top nine operating systems of each type](media/device-health-defender-antivirus-health-view-full-report.png)](media/device-health-defender-antivirus-health-view-full-report.png#lightbox)

A primary benefit of the three `version` cards is that they provide quick indicators as to whether the most current versions of the antivirus engines, platforms, and security intelligence are being utilized. Coupled with the detailed information that is linked to the card, the versions cards become a powerful tool to check if versions are up to date and to gather information about individual computers, or groups of computers. Ideally, when you run these reports, they'll indicate that the most current antivirus versions are installed, as opposed to older versions. Use these reports to determine whether your organization is taking full advantage of the most current versions.

[![Shows Microsoft Defender Antivirus version details](media/device-health-defender-antivirus-health-antivirus-details-up-to-date.png)](media/device-health-defender-antivirus-health-antivirus-details-up-to-date.png#lightbox)

To help ensure your anti-malware solution detects the latest threats, get updates automatically as part of Windows Update.

For more details on the current versions and how to update the different Microsoft Defender Antivirus components, visit [Microsoft Defender Antivirus platform support](microsoft-defender-antivirus-updates).

### Card descriptions

Following are brief summaries of the collected information reported in each of the `Antivirus version` cards:

#### Antivirus mode card

Reports on how many devices in your organization – on the date indicated on the card – are in any of the following Microsoft Defender Antivirus modes:

| value | mode |
| --- | --- |
| `0` | `Active` |
| `1` | `Passive` |
| `2` | `Disabled` (uninstalled, disabled, or SideBySidePassive {also known as Low Periodic Scan}) |
| `3` | `Others` (Not running, Unknown) |
| `4` | `EDRBlocked` |

[![Shows filtering Microsoft Defender Antivirus modes](media/device-health-defender-antivirus-health-antivirus-mode.png)](media/device-health-defender-antivirus-health-antivirus-mode.png#lightbox)

Following are descriptions for each mode:

- **Active** mode - In active mode, Microsoft Defender Antivirus is used as the primary antivirus app on the device. Files are scanned, threats are remediated, and detected threats are listed in your organization's security reports and in your Windows Security app.
- **Passive** mode - In passive mode, Microsoft Defender Antivirus isn't used as the primary antivirus app on the device.

    Important

    Microsoft Defender Antivirus can run in passive mode only on endpoints that are onboarded to Microsoft Defender for Endpoint. See [Requirements for Microsoft Defender Antivirus to run in passive mode](microsoft-defender-antivirus-compatibility#requirements-for-microsoft-defender-antivirus-to-run-in-passive-mode).
- **Disabled** mode - synonymous with: uninstalled, disabled, sideBySidePassive, and Low Periodic Scan. When disabled, Microsoft Defender Antivirus isn't used. Files aren't scanned, and threats aren't remediated. In general, Microsoft doesn't recommend disabling or uninstalling Microsoft Defender Antivirus.
- **Others** mode - Not running, Unknown
- **EDR in Block** mode - In endpoint detection and response (EDR) blocked mode. See [Endpoint detection and response in block mode](edr-in-block-mode)

Devices that are in either passive, LPS, or Off present a potential security risk and should be investigated.

For details about LPS, see [Use limited periodic scanning in Microsoft Defender Antivirus](limited-periodic-scanning-microsoft-defender-antivirus).

#### Recent antivirus scan results card

This card has two bars graphs showing all-up results for quick scans and full scans. In both graphs, the first bar indicates the completion rate for scans, and indicate **Completed**, **Canceled**, or **Failed**. The second bar in each section provides the error codes for failed scans. By scanning the **Mode** and **Recent scan results** columns, you can quickly identify devices that aren't in active antivirus scan mode, and devices that have failed or canceled recent antivirus scans. You can return to the report with this information and gather more details and security recommendations. If any error codes are reported in this card, there will be a link to learn more about error codes.

For more details on the current Microsoft Defender Antivirus versions and how to update the different Microsoft Defender Antivirus components, visit [Manage Microsoft Defender Antivirus updates and apply baselines](microsoft-defender-antivirus-updates).

#### Antivirus engine version card

Shows the real-time results of the most current Microsoft Defender Antivirus engine versions installed across Windows Devices, Mac devices, and Linux devices in your organization. Microsoft Defender Antivirus engine is updated monthly. For more information on the current versions and how to update the different Microsoft Defender Antivirus components, see [Microsoft Defender Antivirus platform support](microsoft-defender-antivirus-updates).

#### Antivirus security intelligence version card

Lists the most common Microsoft Defender Antivirus security intelligence versions installed on devices on your network. Microsoft continually updates Microsoft Defender security intelligence to address the latest threats, and to refine detection logic. These refinements to security intelligence enhance the ability for Microsoft Defender Antivirus (and other Microsoft anti-malware solutions) to accurately identify potential threats. This security intelligence works directly with cloud-based protection to deliver AI-enhanced, next-generation protection that is fast and powerful.

##### Antivirus platform version card

Shows the real-time results of the most current Microsoft Defender Antivirus platform versions installed across versions of Windows, Mac, and Linux devices in your organization. Microsoft Defender Antivirus platform is updated monthly. For more information on the current versions and how to update the different Microsoft Defender Antivirus components, see [Microsoft Defender Antivirus platform support](microsoft-defender-antivirus-updates)

#### Up-to-date cards

The up-to-date cards show the up-to-date status for **Antivirus engine**, **Antivirus platform**, and **Security intelligence** update versions. There are three possible states: `Up to date` (`True`), `out of date` (`False`), and `no data available` (`Unknown`).

Important

The logic used to make up-to-date determinations has recently been enhanced and simplified. The new behavior is documented in this section.

Definitions for `Up to date`, `out of date`, and `no data available` are provided for each card below.

Microsoft Defender Antivirus uses the additional criteria of "Signature refresh time" (the last time device communicated with up to date reports) to make up-to-date reports and determinations for engine, platform, and security intelligence updates.

The up-to-date status is automatically marked as "unknown" or "no data available" if the device hasn't communicated with reports for more than seven days (signature refresh time &gt;7).

For more information about the aforementioned terms, refer back to the section: New Microsoft Defender Antivirus filter definitions

Note

Up-to-date reporting generates information for devices that meet the following criteria:

- **Windows:**
    - OS - Windows 10 1809 or later
    - Engine version: 1.1.19300.2+
    - Platform version: 4.8.2202.1+
    - Sense (MsSense.exe): 10.8210.\*+
- **Linux and Mac:**
    - Platform version: 101.23112.\*+
- **Cloud Protection enabled**

##### Up-to-date definitions

Following are up-to-date definitions for engine and platform:

| The engine/platform on the device is considered: | Situation |
| --- | --- |
| **up to date** | If the device communicated with the Defender report event (`Signature refresh time`) within last seven days, and the Engine or Platform build version is greater than or equal to (`>=`) the most recent monthly release version. |
| **out-of-date** | If the device communicated with the Defender report event (`Signature refresh time`) within last seven days, but Engine or Platform build version is less than (`<`) the most recent monthly release version. |
| **unknown (no data available)** | If the device hasn't communicated with the report event (`Signature refresh time`) for more than seven days. |

Following is the definitions for up-to-date security intelligence:

| The security intelligence update is considered: | Situation |
| --- | --- |
| **up to date** | If the security intelligence version on the device was written in the past seven days and the device has communicated with the report event in past seven days. |

For more information, see:

- Antivirus engine updates card
- Security intelligence updates card
- Antivirus platform updates card

##### Antivirus engine updates card

This card identifies devices that have antivirus engine versions that are up to date versus out of date.

**The general definition of `up to date`** - The engine version on the device is the most recent engine release. The engine is typically released monthly, via Windows Update (WU). There's a three-day grace period given from the day when Windows Update (WU) is released.

The following table lays out the possible values for up to date reports for **Antivirus Engine**. Reported Status is based on the last time reporting event was received (signature refresh time). If the device hasn't communicated with reports for more than seven days (signature refresh time &gt;7 days), then the status is automatically marked as `Unknown` / `No Data Available`.

| Event's Last Refresh Time (also known as "Signature Refresh Time" in reports) | Reported Status |
| --- | --- |
| &lt; 7 days (new) | whatever client reports (*Up to date Out of date Unknown)* |
| &gt; 7 days (old) | `Unknown` |

For information about Manage Microsoft Defender Antivirus update versions, see [Monthly platform and engine versions](microsoft-defender-endpoint-releases#microsoft-defender-antivirus-releases).

#### Antivirus platform updates card

This card identifies devices that have Antivirus platform versions that are up to date versus out of date.

**The general definition of `up to date`** is that the platform version on the device is the most recent platform release. Platform is typically released monthly, via Windows Update (WU). There's a three-day grace period from the day when WU is released.

The following table lays out the possible up to date report values for **Antivirus Platform**. Reported values are based on the last time reporting event was received (signature refresh time). If the device hasn't communicated with reports for more than seven days (signature refresh time &gt;7 days) then the status is automatically marked as `Unknown`/ `No Data Available`.

| Event's Last Refresh Time (also known as "Signature Refresh Time" in reports) | Reported Status |
| --- | --- |
| &lt; 7 days (new) | whatever client reports (`Up to date``Out of date``Unknown)` |
| &gt; 7 days (old) | `Unknown` |

For information about Manage Microsoft Defender Antivirus update versions, see [Monthly platform and engine versions](microsoft-defender-endpoint-releases#microsoft-defender-antivirus-releases).

##### Security intelligence updates card

This card identifies devices that have security intelligence versions that are up to date versus out of date.

**The general definition of `up to date`** is that the security intelligence version on the device was written in the past 7 days.

The following table lays out the possible up to date report values for **Security Intelligence** updates. Reported values are based on the last time reporting event was received, and the security intelligence publish time. If the device hasn't communicated with reports for more than seven days (signature refresh time &gt;7 days), then the status is automatically marked as `Unknown/ No Data Available`. Otherwise, the determination is made based on whether the security intelligence publish time is within seven days.

| Event's Last Refresh Time(Also known as "Signature Refresh Time" in reports) | Security Intelligence Publish Time | *Reported Status* |
| --- | --- | --- |
| &gt;7 days (old) | &gt;7 days (old) | `Unknown` |
| &lt;7 days (new) | &gt;7 days (old) | `Out of date` |
| &gt;7 days (old) | &lt;7 days (new) | `Unknown` |
| &lt;7 days (new) | &lt;7 days (new) | `Up to date` |