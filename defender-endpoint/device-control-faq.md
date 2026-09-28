---
layout: Conceptual
title: Microsoft Defender for Endpoint Device Control frequently asked questions - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/device-control-faq
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Answers frequently asked questions about device control in Defender for Endpoint
ms.service: defender-endpoint
ms.subservice: asr
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-asr
ms.custom:
- admindeeplinkDEFENDER
- sfi-image-nochange
ms.topic: faq
ms.date: 2026-01-05T00:00:00.0000000Z
ms.reviewer: tewchen, joshbregman
locale: en-us
document_id: 9f8e8f61-6cfe-68dc-f286-40f444bea76b
document_version_independent_id: 9f8e8f61-6cfe-68dc-f286-40f444bea76b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/device-control-faq.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: device-control-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/device-control-faq.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 67e0b911-de3d-fbde-51c7-78064918e03a
---

# Microsoft Defender for Endpoint Device Control frequently asked questions - Microsoft Defender for Endpoint | Microsoft Learn

This article provides answers to frequently asked questions about device control removable storage capabilities in Microsoft Defender for Endpoint.

## How do I generate GUID for Group ID/PolicyRule ID/Entry ID?

You can generate the GUID through online open source or by using PowerShell. For more information, see [How to generate GUID through PowerShell](/en-us/powershell/module/microsoft.powershell.utility/new-guid).

![Screenshot of GUID in PowerShell.](https://user-images.githubusercontent.com/81826151/159046476-26ea0a21-8087-4f01-b8ae-5aa73b392d8f.png)

## What are the removable storage media and policy limitations?

The backend call is done through OMA-URI (GET to read or PATCH to update) either from Intune or through Microsoft Graph API. The limitation is the same as any OMA-URI custom configuration profile at Microsoft, which is officially 350,000 characters for XML files. For example, if you need two blocks of entries per user SID to "Allow" / "Audit allowed" specific users, and then two blocks of entries at the end to "Deny" all, you'll be able to manage 2,276 users.

## Why doesn't the policy work?

The most common reason is there's no required anti-malware client version.

Another reason could be that the XML file isn't correctly formatted. For example, not using the correct markdown formatting for the "&" character in the XML file or the text editor might add a byte order mark (BOM) 0xEF 0xBB 0xBF at the beginning of the files causing the XML parsing not to work. One simple solution is to download the [sample file](https://github.com/microsoft/mdatp-devicecontrol/tree/main/Removable%20Storage%20Access%20Control%20Samples) (select **Raw** and then **Save as**), and then update.

If you're deploying and managing the policy by using Group Policy, make sure to combine all policy rules into one XML file within a parent node called `PolicyRules`. Also, combine all groups into one XML file within a parent node called `PolicyGroups`. If you're managing devices with Intune, keep separate XML files for each group and policy when deploying as `Custom OMA-URI`.

The device (machine) should have a valid certificate. Run the following PowerShell command on the machine to check:

```powershell
Get-AuthenticodeSignature C:\Windows\System32\wbem\WmiPrvSE.exe
```

![Screenshot showing results of Get-AuthenticodeSignature cmdlet.](https://user-images.githubusercontent.com/81826151/202582101-5470dd54-ef32-4448-80c9-ba23a721dc70.png)

If the policy still isn't working, generate the `C:\ProgramData\Microsoft\Windows Defender\Support\MpSupportFiles.cab` file, and then contact support. For instructions, see [Collect Microsoft Defender Antivirus diagnostic data](collect-diagnostic-data).

## Why is there no configuration UX for some policy groups?

There's no configuration UX for **Define device control policy groups** and **Define device control policy rules** in Group Policy. However, you can configure the policies by using the related `.adml` and `.admx` files. For details, see [Configure device control with Group Policy](device-control-configure#configure-device-control-with-group-policy).

## How do I confirm that the latest policy has been deployed to the target machine?

You can run the PowerShell cmdlet `Get-MpComputerStatus` as an administrator. The following value will show whether the latest policy has been applied to the target machine.

![Screenshot showing device control status in PowerShell.](media/148609885-bea388a9-c07d-47ef-b848-999d794d24b8.png)

## How can I know which machine is using out of date anti-malware client version in the organization?

You can use following query to get anti-malware client version on the Microsoft 365 security portal:

```kusto
//check the anti-malware client version
DeviceFileEvents
|where FileName == "MsMpEng.exe"
|where FolderPath contains @"C:\ProgramData\Microsoft\Windows Defender\Platform\"
|extend PlatformVersion=tostring(split(FolderPath, "\\", 5))
//|project DeviceName, PlatformVersion // check which machine is using legacy platformVersion
|summarize dcount(DeviceName) by PlatformVersion // check how many machines are using which platformVersion
|order by PlatformVersion desc
```

## How do I find the media property in the Device Manager?

1. After you insert the media, open Device Manager (for example, run the command `devmgmt.msc`).
2. Locate the media in Device Manager (for example, under Disk drives), right-click on the media, and then select **Properties**

    [![Screenshot of right-clicking on the media in Device Manager and then selecting Properties.](media/device-manager-select-media.png)](media/device-manager-select-media.png#lightbox)
3. In the properties of the media, select the **Details** tab, and then select the **Device instance path** property.

    [![Screenshot of the Device instance path property of the Details tab of the media properties in Device Manager.](media/device-manager-media-properties.png)](media/device-manager-media-properties.png#lightbox)

Another way to find the media property is to deploy an Audit policy to the organization, and then see the events in advanced hunting or the device control report.

## How do I find Sid for Microsoft Entra group?

The Sid is uses the **Object ID** value for Microsoft Entra groups. You can find the **Object Id** value from the group properties in the Microsoft Entra portal.

[![Screenshot of the Object ID value in the group properties in the Microsoft Entra admin center.](media/microsoft-entra-group-sid.png)](media/microsoft-entra-group-sid.png#lightbox)

## Why is my printer blocked in my organization?

The **Default Enforcement** setting is for all device control components, which means if you set it to `Deny`, it will block all printers as well. You can either create custom policy to explicitly allow printers or you can replace the Default Enforcement policy with a custom policy.

## Why is creating a folder not blocked by File system level access?

Creating an empty folder will not be blocked even if **File system level access** Write access Deny is configured. Any non-empty file will be blocked.

## Why is my USB still blocked with an allow-ready policy?

Some specific USB devices require more than Read access, the following list shows some examples:

1. Read access to some Kingston encrypted USBs requires Execute access for its CDROM.
2. Read access to some WD My Passport USBs requires Disk level Write access. To deny Write access, you use the **File system level access**.

The best way to understand this is to check the event on the Advanced hunting which will clearly show what accessMask is required.

## Can I use both Group Policy and Intune deploy policies?

You can use Group Policy and Intune to manage device control, but for one machine, use *either* Group Policy *or* Intune. If a machine is covered by both, device control will only apply the Group Policy setting.

## Is device control available in Microsoft Defender for Business?

Yes, for Windows and Mac.

To set up device control on Windows, use [attack surface reduction](/en-us/defender-business/mdb-asr). You need [Microsoft Intune](/en-us/intune/intune-service/fundamentals/what-is-intune). The standalone version of Defender for Business doesn't include Intune, but it can be added on. [Microsoft 365 Business Premium](/en-us/microsoft-365/business-premium) includes Intune. See [Microsoft Defender for Endpoint Device Control Removable Storage Access Control](device-control-overview).

To set up device control on Mac, use Intune or Jamf. See [Device Control for macOS](mac-device-control-overview).