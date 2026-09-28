---
layout: Conceptual
title: Configure a monitoring interface using a Hyper-V vSwitch - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/traffic-mirroring/configure-mirror-hyper-v
breadcrumb_path: ../../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
description: This article describes traffic mirroring with a Hyper-V vSwitch for OT monitoring with Microsoft Defender for IoT.
ms.date: 2024-03-14T00:00:00.0000000Z
ms.topic: install-set-up-deploy
locale: en-us
document_id: c3928e52-8e55-fca2-2ffc-3f12d58d3ae5
document_version_independent_id: ada9ad6a-3883-afae-22a0-e97670f0b4d1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/traffic-mirroring/configure-mirror-hyper-v.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/traffic-mirroring/configure-mirror-hyper-v
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/traffic-mirroring/configure-mirror-hyper-v.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 7e5a7474-9271-9fbe-96be-7dd734a870b8
---

# Configure a monitoring interface using a Hyper-V vSwitch - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](../ot-deploy/ot-deploy-path) for OT monitoring with Microsoft Defender for IoT.

[![Diagram of a progress bar with Network level deployment highlighted.](../media/deployment-paths/progress-network-level-deployment.png)](../media/deployment-paths/progress-network-level-deployment.png#lightbox)

This article describes how to use *Promiscuous mode* in a Hyper-V Vswitch environment as a workaround for configuring traffic mirroring, similar to a [SPAN port](configure-mirror-span). A SPAN port on your switch mirrors local traffic from interfaces on the switch to a different interface on the same switch.

For more information, see [Traffic mirroring with virtual switches](../best-practices/traffic-mirroring-methods#traffic-mirroring-with-virtual-switches).

## Prerequisites

Before you start:

- Make sure that you understand your plan for network monitoring with Defender for IoT, and the SPAN ports you want to configure.

    For more information, see [Traffic mirroring methods for OT monitoring](../best-practices/traffic-mirroring-methods).
- Ensure that there's no instance of a virtual appliance running.
- Make sure that you've enabled *Ensure SPAN* on your virtual switch's data port, and not the management port.
- Ensure that the data port SPAN configuration isn't configured with an IP address.

## Create new Hyper-V virtual switch to relay the mirrored traffic into the VM

### Create a new virtual switch with PowerShell

```PowerShell
New-VMSwitch -Name vSwitch_Span -NetAdapterName Ethernet -AllowManagementOS:$true
```

Where:

| Parameter | Description |
| --- | --- |
| **vSwitch\_Span** | Newly added SPAN virtual switch name |
| **Ethernet** | Physical adapter name |

Learn how to [Create and configure a virtual switch with Hyper-V](/en-us/windows-server/virtualization/hyper-v/get-started/create-a-virtual-switch-for-hyper-v-virtual-machines?tabs=powershell#create-a-virtual-switch)

### Create a new virtual switch with Hyper-V Manager

1. Open the Virtual Switch Manager.
2. In the **Virtual switches** list, select **New virtual network switch** &gt; **External** as the dedicated spanned network adapter type.

    ![Screenshot of selecting new virtual network and external before creating the virtual switch.](../media/tutorial-install-components/new-virtual-network.png)
3. Select **Create Virtual Switch**.
4. In the **Connection type** area, select **External network** and ensure that the **Allow management operating system to share this network adapter** option is selected. For example:

    ![Screenshot of the External network option.](../media/tutorial-install-components/external-network.png)
5. Select **OK**.

## Attach a SPAN Virtual Interface to the virtual switch

Use Windows PowerShell or Hyper-V Manager to attach a SPAN virtual interface to the virtual switch you created earlier.

If you use PowerShell, define the name of the newly added adapter hardware as `Monitor`. If you use Hyper-V Manager, the name of the newly added adapter hardware is set to `Network Adapter`.

### Attach a SPAN virtual interface to the virtual switch with PowerShell

1. Select the newly added SPAN virtual switch you created earlier, and run the following command to add a new network adapter:

    ```powershell
    ADD-VMNetworkAdapter -VMName VK-C1000V-LongRunning-650 -Name Monitor -SwitchName vSwitch_Span
    ```
2. Enable port mirroring for the selected interface as the span destination with the following command:

    ```powershell
    Get-VMNetworkAdapter -VMName VK-C1000V-LongRunning-650 | ? Name -eq Monitor | Set-VMNetworkAdapter -PortMirroring Destination
    ```

    Where:

    | Parameter | Description |
    | --- | --- |
    | **VK-C1000V-LongRunning-650** | CPPM VA name |
    | **vSwitch\_Span** | Newly added SPAN virtual switch name |
    | **Monitor** | Newly added adapter name |
3. When you're done, select **OK**.

### Attach a SPAN virtual interface to the virtual switch with Hyper-V Manager

1. Under the Hyper-V Manager's **Hardware** list, select **Network Adapter**.
2. In the **Virtual switch** field, select **vSwitch\_Span**.

    ![Screenshot of selecting the following options on the virtual switch screen.](../media/tutorial-install-components/vswitch-span.png)
3. In the **Hardware** list, under the **Network Adapter** drop-down list, select **Advanced Features**. Under the **Port Mirroring** section, select **Destination** as the mirroring mode for the new virtual interface.

    ![Screenshot of the selections needed to configure mirroring mode.](../media/tutorial-install-components/destination.png)
4. Select **OK**.

## Turn on Microsoft NDIS capture extensions with PowerShell

Turn on support for [Microsoft NDIS Capture Extensions](/en-us/windows-hardware/drivers/network/capturing-extensions) for the virtual switch you created earlier.

**To enable Microsoft NDIS capture extensions for your new virtual switch**:

```PowerShell
Enable-VMSwitchExtension -VMSwitchName vSwitch_Span -Name "Microsoft NDIS Capture"
```

## Turn on Microsoft NDIS capture extensions with Hyper-V Manager

Turn on support for [Microsoft NDIS Capture Extensions](/en-us/windows-hardware/drivers/network/capturing-extensions) for the virtual switch you created earlier.

**To enable Microsoft NDIS capture extensions for your new virtual switch**:

1. Open the Virtual Switch Manager on the Hyper-V host.
2. In the Virtual Switches list, expand the virtual switch name `vSwitch_Span` and select **Extensions**.
3. In the Switch Extensions field, select **Microsoft NDIS Capture**.

    ![Screenshot of enabling the Microsoft NDIS by selecting it from the switch extensions menu.](../media/tutorial-install-components/microsoft-ndis.png)
4. Select **OK**.

## Configure the switch's mirroring mode

Configure the mirroring mode on the virtual switch you created earlier so that the external port is defined as the mirroring source. This includes configuring the Hyper-V virtual switch (vSwitch\_Span) to forward any traffic that comes to the external source port to a virtual network adapter configured as the destination.

To set the virtual switch's external port as the source mirror mode, run:

```PowerShell
$ExtPortFeature=Get-VMSystemSwitchExtensionPortFeature -FeatureName "Ethernet Switch Port Security Settings"
$ExtPortFeature.SettingData.MonitorMode=2
Add-VMSwitchExtensionPortFeature -ExternalPort -SwitchName vSwitch_Span -VMSwitchExtensionFeature $ExtPortFeature
```

Where:

| Parameter | Description |
| --- | --- |
| **vSwitch\_Span** | Name of the virtual switch you created earlier |
| **MonitorMode=2** | Source |
| **MonitorMode=1** | Destination |
| **MonitorMode=0** | None |

To verify the monitoring mode status, run:

```PowerShell
Get-VMSwitchExtensionPortFeature -FeatureName "Ethernet Switch Port Security Settings" -SwitchName vSwitch_Span -ExternalPort | select -ExpandProperty SettingData
```

| Parameter | Description |
| --- | --- |
| **vSwitch\_Span** | Newly added SPAN virtual switch name |

## Configure VLAN settings for the Monitor adapter (if needed)

If the mirrored traffic is VLAN tagged, configure the Monitor adapter of the VM to accept traffic from the mirrored VLAN(s).

Use this PowerShell command to enable the Monitor adapter of the VM to accept the monitored traffic from different VLANs:

```PowerShell
Set-VMNetworkAdapterVlan -VMName VK-C1000V-LongRunning-650 -VMNetworkAdapterName Monitor -Trunk -AllowedVlanIdList 1010-1020 -NativeVlanId 10
```

Where:

| Parameter | Description |
| --- | --- |
| **VK-C1000V-LongRunning-650** | CPPM VA name |
| **1010-1020** | VLAN range from which IoT traffic is mirrored |
| **10** | Native VLAN ID of the environment |

Learn more about the [Set-VMNetworkAdapterVlan](/en-us/powershell/module/hyper-v/set-vmnetworkadaptervlan) PowerShell cmdlet.

## Validate traffic mirroring

After configuring traffic mirroring, make an attempt to receive a sample of recorded traffic (PCAP file) from the switch SPAN or mirror port.

A sample PCAP file will help you:

- Validate the switch configuration
- Confirm that the traffic going through your switch is relevant for monitoring
- Identify the bandwidth and an estimated number of devices detected by the switch

1. Use a network protocol analyzer application, such as [Wireshark](https://www.wireshark.org/), to record a sample PCAP file for a few minutes. For example, connect a laptop to a port where you've configured traffic monitoring.
2. Check that *Unicast packets* are present in the recording traffic. Unicast traffic is traffic sent from address to another.

    If most of the traffic is ARP messages, your traffic mirroring configuration isn't correct.
3. Verify that your OT protocols are present in the analyzed traffic.

    For example:

    ![Screenshot of Wireshark validation.](../media/how-to-set-up-your-network/wireshark-validation.png)