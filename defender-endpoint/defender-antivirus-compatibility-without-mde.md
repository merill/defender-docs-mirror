---
layout: Conceptual
title: Microsoft Defender Antivirus and non-Microsoft antivirus/antimalware solutions Antivirus protection without Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/defender-antivirus-compatibility-without-mde
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Microsoft Defender Antivirus and non-Microsoft antivirus/antimalware solutions Antivirus protection without Defender for Endpoint
author: chrisda
ms.author: chrisda
ms.reviewer: yongrhee
ms.service: defender-endpoint
ms.topic: article
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: ngp
ms.localizationpriority: medium
ms.custom:
- partner-contribution
locale: en-us
document_id: 889c6641-c24c-85e1-1cc8-abb0d48b2eea
document_version_independent_id: 889c6641-c24c-85e1-1cc8-abb0d48b2eea
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/defender-antivirus-compatibility-without-mde.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-antivirus-compatibility-without-mde
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/defender-antivirus-compatibility-without-mde.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 1bc75ba7-0612-f58f-6729-6ecf79bf5a41
---

# Microsoft Defender Antivirus and non-Microsoft antivirus/antimalware solutions Antivirus protection without Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

This section describes what happens when you use Microsoft Defender Antivirus alongside non-Microsoft antivirus/antimalware products on endpoints that aren't onboarded to Defender for Endpoint Plan 2.

Microsoft Defender Antivirus doesn't run in passive mode on devices that aren't onboarded to Defender for Endpoint Plan 2.

The following table summarizes what to expect:

| Windows version | Primary antivirus/antimalware solution | Microsoft Defender Antivirus state |
| --- | --- | --- |
| Windows 11 and Windows 10 | Microsoft Defender Antivirus | Active mode |
| Windows 11 and Windows 10 | A non-Microsoft antivirus solution | Disabled mode (happens automatically). |
| Windows server 2016 and later.  Windows Server version 1803 or newer.  Azure Stack HCI OS, version 23H2 and later. | Microsoft Defender Antivirus | Active mode |
| Windows server 2016 and later.  Windows Server version 1803 or newer.  Azure Stack HCI OS, version 23H2 and later. | A non-Microsoft antivirus solution | Disabled (set manually; see the note that follows this table) |

Note

Defender for Endpoint support for Windows Server 2025 is rolling out, beginning in February 2025 and over the next several weeks. On Windows Server, if you're running a non-Microsoft antivirus product, you can uninstall Microsoft Defender Antivirus by using the following PowerShell cmdlet (as an administrator): `Uninstall-WindowsFeature Windows-Defender`. Restart your server to finish removing Microsoft Defender Antivirus. On Windows Server 2016, you might see *Windows Defender Antivirus* instead of *Microsoft Defender Antivirus*. If you uninstall your non-Microsoft antivirus product, make sure that Microsoft Defender Antivirus is re-enabled. See **[Re-enable Microsoft Defender Antivirus on Windows Server if it was disabled](enable-update-mdav-to-latest-ws)**.

Check the services and filter drivers for Microsoft Defender Antivirus by using the following command:

```powershell

gsv WinDefend, WdBoot, WdFilter, WdNisSvc, WdNisDrv | ft -auto DisplayName, Name, StartType, Status

```

| Display Name | Name | StartType | Status when Microsoft Defender Antivirus is enabled | Status when Microsoft Defender Antivirus is disabled | Comments |
| --- | --- | --- | --- | --- | --- |
| Microsoft Defender Antivirus Boot Driver | `WdBoot` | Boot | Stopped (`0x0 Boot_start`) | Stopped (`0x3 Demand_start`) | It's normal to be stopped after boot. |
| Microsoft Defender Antivirus Mini-Filter Driver | `WdFilter` | Manual | Running (`0x0 Boot_start`) | Stopped (`0x3 Demand_start`) | If a non-Microsoft antivirus solution is installed, expect the status to be stopped. |
| Microsoft Defender Antivirus Network Inspection System Driver | `WdNisDrv` | Manual | Running (`0x3 Demand_start`) | Stopped (`0x3 Demand_start`) | If a non-Microsoft antivirus solution is installed, expect the status to be stopped. |
| Microsoft Defender Antivirus Network Inspection Service | `WdNisSvc` | Manual | Running (`0x3 Demand_start`) | Stopped (`0x3 Demand_start`) | If a non-Microsoft antivirus solution is installed, expect the status to be stopped. |
| Microsoft Defender Antivirus Service | `WinDefend` | Automatic | Running (`0x2 Auto_start`) | Stopped (`0x3 Demand_start`) | If a non-Microsoft antivirus solution is installed, expect the status to be stopped. |

### Frequently Asked Questions (FAQ)

**Q:** Can I update Microsoft Defender Antivirus components such as "Security intelligence update" or "Engine update" or "Platform update" when Microsoft Defender Antivirus is disabled?

**A:** No. When Microsoft Defender Antivirus is disabled, since the services and drivers aren't running, you won't be able to update the components such as "Security intelligence update" or "Engine update" or "Platform update".

Tip

If you are migrating to Microsoft Defender for Endpoint Plan 2, when onboarded, Microsoft Defender Antivirus goes into passive mode automatically on Windows clients, and can be set to passive mode using a registry key on Windows Server. You can update the different components of Microsoft Defender Antivirus.

**Q:** Can I manually change the start type of the services and drivers for Microsoft Defender Antivirus?

**A:** We don't support the manual modification of the start type of the services and drivers for Microsoft Defender Antivirus in Windows images. On Windows clients, the supported method is by your non-Microsoft antivirus registering in Windows Security Center (WSC) api. Or, on Windows Server, you can uninstall the Microsoft Defender Antivirus feature by using roles and features MMC or by running the following PowerShell command (as an administrator):

Windows Server 2019 and newer

```powershell

Uninstall-WindowsFeature Windows-Defender

```

Windows Server 2016

```powershell

Uninstall-WindowsFeature Windows-Defender
Uninstall-WindowsFeature Windows-Defender-Gui
```

**Q:** Can I use Microsoft Defender Antivirus in passive mode without onboarding to Microsoft Defender for Endpoint?

**A:** No. Passive mode is a functionality in Microsoft Defender for Endpoint Plan 1, Microsoft Defender for Endpoint Plan 2 and Microsoft Defender for Business.

**Q:** Can I use [EDR in block mode](edr-in-block-mode) without onboarding to Microsoft Defender for Endpoint?

**A:** No. EDR in block mode is a functionality in Microsoft Defender for Endpoint Plan 2.

**Q:** Can I use indicators, such as file hashes, IP addresses, URLs, or certificates with Microsoft Defender Antivirus (in active mode) with my Microsoft 365 E3/A3 license?

**A:** Yes. See [Tech Community Blog: Microsoft Defender for Endpoint Plan 1 Now Included in Microsoft 365 E3/A3 Licenses](https://techcommunity.microsoft.com/blog/microsoftdefenderatpblog/microsoft-defender-for-endpoint-plan-1-now-included-in-m365-e3a3-licenses/3060639) and [Overview of Microsoft Defender for Endpoint Plan 1](defender-endpoint-plan-1).