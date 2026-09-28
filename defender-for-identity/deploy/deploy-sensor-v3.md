---
layout: Conceptual
title: Deploy the Microsoft Defender for Identity sensor v3.x - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/deploy/deploy-sensor-v3
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn the requirements and configuration steps to deploy the Defender for Identity sensor v3.x on eligible identity-role servers.
ms.date: 2026-09-09T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1016
ms.reviewer: rlitinsky
ai-usage: ai-assisted
locale: en-us
document_id: 60ad0205-4282-3e44-50b4-e24f83a8bfab
document_version_independent_id: 60ad0205-4282-3e44-50b4-e24f83a8bfab
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/deploy/deploy-sensor-v3.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy/deploy-sensor-v3
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/deploy/deploy-sensor-v3.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 1d6f7caa-98cc-b973-667d-5b1673c51a02
---

# Deploy the Microsoft Defender for Identity sensor v3.x - Microsoft Defender for Identity | Microsoft Learn

Deploy the Defender for Identity sensor v3.x on eligible domain controllers and AD FS, AD CS, or Microsoft Entra Connect servers that aren't domain controllers. Complete the prerequisite checks before activation, then configure auditing and identity settings.

## Before you activate

Complete these checks before activating the sensor.

### Sensor version limitations

Before you activate the Defender for Identity sensor v3.x, note that v3.x:

- Doesn't support VPN integration.
- Doesn't support [syslog notifications](../notifications#configure-syslog-notifications).
- Has limitations working with Azure ExpressRoute. For more information, see [Azure ExpressRoute for Microsoft 365](/en-us/microsoft-365/enterprise/azure-expressroute).

### Server requirements

Make sure that the server on which you're activating the sensor:

- Is onboarded to Defender for Endpoint. The Microsoft Defender Antivirus component can be in either active or passive mode. For eligible domain controllers, you can instead use [sensor v3.x onboarding without Defender for Endpoint deployment](activate-sensor#onboard-the-domain-controller-preview).
- Doesn't have a Defender for Identity sensor v2.x already deployed.
- Runs Windows Server 2019 or later.
- Has the Windows Server July 2026 or later cumulative update installed.

#### Supported server types

The v3.x sensor supports domain controllers. It also supports servers that aren't domain controllers and run the following identity roles:

- Active Directory Federation Services (AD FS)
- Active Directory Certificate Services (AD CS)
- Microsoft Entra Connect

Note

Activating the Defender for Identity sensor v3.x on AD FS, AD CS, and Microsoft Entra Connect servers that aren't domain controllers is in preview. Manual activation and automatic Windows event auditing are supported. Automatic activation and migration aren't currently supported for these servers.

Important

If you deploy the Defender for Identity sensor v3.x only on AD FS, AD CS, or Microsoft Entra Connect servers, you must also install at least one v3.x sensor on a domain controller.

### Licensing requirements

Deploying Defender for Identity requires one of the following Microsoft 365 licenses:

- Enterprise Mobility + Security E5 (EMS E5/A5)
- Microsoft 365 E5 (Microsoft E5/A5/G5)
- Microsoft 365 E5/A5/G5/F5\* Security
- Microsoft 365 F5 Security + Compliance\*

Both F5 licenses require Microsoft 365 F1/F3 or Office 365 F3 and Enterprise Mobility + Security E3. Purchase licenses in the Microsoft 365 portal or through Cloud Solution Partner (CSP) licensing. For more information, see [Licensing and privacy FAQs](/en-us/defender-for-identity/technical-faq#licensing-and-privacy).

### Roles and permissions

- To create your Defender for Identity workspace, you need a Microsoft Entra ID tenant.
- You must either be a [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference), or have the following [Unified RBAC](../role-groups#unified-role-based-access-control-rbac) permissions:

    - `System settings (Read and manage)`
    - `Security settings (All permissions)`

### Network requirements

The Defender for Identity sensor uses the same URIs as Microsoft Defender for Endpoint. Review the following documents for Defender for Endpoint, based on your system's connectivity, to find the complete list of required service endpoints.

- [Microsoft Defender for Endpoint streamlined connectivity URLs](/en-us/defender-endpoint/streamlined-device-connectivity-urls-commercial?tabs=Windows)
- [Microsoft Defender for Endpoint standard connectivity URLs](/en-us/defender-endpoint/standard-device-connectivity-urls-commercial)

### Memory requirements

The following table describes memory requirements on the server running the Defender for Identity sensor, depending on the type of virtualization you're using:

| VM running on | Description |
| --- | --- |
| Hyper-V | Ensure that **Enable Dynamic Memory** isn't enabled for the VM. |
| VMware | Ensure that the amount of memory configured and the reserved memory are the same, or select the **Reserve all guest memory (All locked)** option in the VM settings. |
| Other virtualization host | Refer to the vendor-supplied documentation on how to ensure that memory is always fully allocated to the VMs. |

Important

When running as a virtual machine, always allocate all memory to the virtual machine.

The Defender for Identity sensor v3.x limits CPU utilization to 30% and memory usage to 1.5 GB. However, if another service uses substantial system resources, the server might still experience performance strain. If the sensor reaches the CPU limit, it throttles some event processing. If the sensor reaches the memory limit, the sensor service might restart.

Refer to the [Defender for Identity Capacity Planning documentation](/en-us/defender-for-identity/deploy/capacity-planning) to determine whether your servers have enough resources for a Microsoft Defender for Identity sensor.

### Service account requirements

The Defender for Identity sensor interacts with Active Directory in two ways:

- **Reading AD data** (querying objects, tracking changes, resolving entities). In v2.x, this uses a Directory Service Account (DSA). In v3.x, LocalSystem handles this automatically.
- **Performing remediation actions** (disabling accounts, resetting passwords). In v2.x, this uses an action account. In v3.x, LocalSystem handles this automatically.

The v3.x sensor uses the local system identity of the server for both purposes. It doesn't use Directory Service Accounts (DSA) or group Managed Service Accounts (gMSA). LocalSystem is the only supported identity for v3.x.

If you're migrating from sensor v2.x and previously had a gMSA configured for [action accounts](manage-action-accounts), select **Automatically use the sensor's local system account** in the Microsoft Defender portal (**Settings** &gt; **Identities** &gt; **Microsoft Defender for Identity** &gt; **Manage action accounts**). The v3.x sensors don't use gMSA accounts configured for v2.x sensors.

Important

If any of your sensors are v3.x, select **Automatically use the sensor's local system account** for all sensors. The v3.x sensors use the local system account regardless of gMSA configuration.

#### DSA and gMSA health alerts in environments with both v2.x and v3.x sensors

If your workspace still has a Directory Service Account (DSA) or group Managed Service Account (gMSA) configured because v2.x sensors on AD FS, AD CS, or Entra Connect servers still require it, DSA and gMSA credentials continue to be validated on all sensors in the workspace, including v3.x sensors. If DSA or gMSA credential validation fails, the **Directory services user credentials are incorrect** health alert appears. Workspace-level validation of DSA and gMSA credentials on all sensors is by design. Defender for Identity validates DSA and gMSA credentials at the workspace level for all sensors as long as those accounts exist, regardless of whether individual sensors use them for auditing or response actions.

Defender for Identity v3.x sensors ignore the DSA and gMSA for auditing and response actions, but they're still included in workspace-level credential validation. To stop receiving this health alert on v3.x sensors, remove the workspace-level DSA or gMSA after all sensors are fully migrated to v3.x and no v2.x sensors require it.

### Test your prerequisites

Run the [*Test-MdiReadiness.ps1*](https://github.com/microsoft/Microsoft-Defender-for-Identity/tree/main/Test-MdiReadiness) script to test whether your environment has the necessary prerequisites.

The *Test-MdiReadiness.ps1* script is also available from Microsoft Defender XDR, on the **Identities &gt; Tools** page (Preview).

## Activate the sensor

After confirming all prerequisites, [activate the sensor from the Microsoft Defender portal](activate-sensor).

## Configure settings after activation

Complete these configuration steps after the sensor is activated and running.

### Configure Windows event auditing

Defender for Identity relies on Windows event logs for many detections. For v3.x sensors, [enable automatic auditing](configure-windows-event-collection#configure-defender-for-identity-to-collect-windows-events-automatically), which handles all auditing settings without manual configuration.

If automatic auditing isn't available or you opted out, [configure auditing manually](configure-windows-event-collection#configure-windows-event-collection-manually) or [configure Windows event collection using PowerShell](configure-windows-event-collection#configure-windows-event-collection-using-powershell).

### Configure RPC auditing

Starting with the July 2026 Defender for Identity sensor release (sensor version 3.0.8), RPC auditing is automatically enabled on domain controllers when you upgrade the sensor to the latest version. You no longer need to apply a tag manually to enable RPC auditing, and the related health alert clears shortly after the upgrade.

Note

If you're on sensor version 3.0.8 and you already applied the **Unified Sensor RPC Audit** or **Sensor Extended RPC Audit** tag, no additional action is needed. You can leave the tag in place.

### Recommended settings

Use the following recommended settings to help ensure stable sensor performance:

- Set the **Power Option** of the machine running the Defender for Identity sensor to **High Performance**.
- Synchronize the time on servers where you install the sensor to within five minutes of each other.