---
layout: Conceptual
title: Configure Windows Endpoint Monitoring for OT active monitoring - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/configure-windows-endpoint-monitoring
breadcrumb_path: ../breadcrumb/toc.json
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
description: Configure Windows Endpoint Monitoring so Microsoft Defender for IoT can actively probe Windows devices and collect detailed information such as service pack levels.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: bca27314-9ad7-80e5-23a4-fb5da37534c8
document_version_independent_id: 9ba1e6ec-3f99-ebb9-fbfd-4b5ffe1addd8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/configure-windows-endpoint-monitoring.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/configure-windows-endpoint-monitoring
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/configure-windows-endpoint-monitoring.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: fad8062b-8a15-6cfb-b7a0-1c4f7fc0f5fb
---

# Configure Windows Endpoint Monitoring for OT active monitoring - Microsoft Defender for IoT | Microsoft Learn

This article describes how to configure Windows Endpoint Monitoring (WEM) to have Microsoft Defender for IoT selectively and actively probe Windows systems.

WEM can provide more focused and accurate information about your Windows devices, such as service pack levels. Before you begin, make sure you meet the prerequisites, including a configured OT sensor and active monitoring setup.

## Supported protocols

Currently the only protocol supported for Windows Endpoint Monitoring with Defender for IoT is WMI, Microsoft's standard scripting language for managing Windows systems.

## Prerequisites

Before performing the procedures in this article, you must have:

- An OT network sensor with software [installed](ot-deploy/install-software-ot-sensor), [configured, and activated](ot-deploy/activate-deploy-sensor).
- Access to your OT network sensor as an **Admin** user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).
- Completed the prerequisites outlined in [Configure active monitoring for OT networks](configure-active-monitoring), and confirmed that active monitoring is right for your network.
- Before you can configure a WEM scan from your OT sensor console, you'll also need to configure a firewall rule, and WMI domain scanning on your Windows machine.

## Configure the required firewall rule

Configure a firewall rule that opens outgoing traffic from the sensor to the scanned subnet by using UDP port 135 and all TCP ports above 1024.

## Configure WMI domain scanning

Before you can configure a WEM scan from your sensor, you need to configure WMI domain scanning on the Windows machine you'll be scanning.

This procedure describes how to configure WMI scanning using a Group Policy Object (GPO), updating your firewall settings, defining permissions for your WMI namespace, and defining a local group.

### Prerequisites for WMI domain scanning

Before configuring WMI domain scanning, make sure the following requirements are met:

- Make sure that the Windows Management Instrumentation service (**winmgmt**) is in the automatic start mode.
- Create a user named **wmiuser**. Make sure this user is a member of the Domain users on your Windows machine.

### Configure a Group Policy Object (GPO)

Perform the following steps to create and configure the GPO used for WMI access:

1. On your Windows machine, [create a new GPO](/en-us/windows/security/threat-protection/windows-firewall/create-a-group-policy-object) named **WMIAccess**.
2. Right-click your new **WMIAccess** GPO and select **Edit**.
3. In the **Group Policy Management Editor** window, select **Computer Configuration &gt; Windows Settings &gt; Security Settings &gt; Local Policies &gt; Security Options**.
4. Navigate to and double-click the **DCOM: Machine Access Restrictions in Security Descriptor Definition Language (SDDL) syntax** policy to open the properties window to the **Template Security Policy Setting** tab.

    Use the following steps to configure access for this policy:

    1. Select **Edit Security** and then in the **Access Permission** dialog, select **Add**.
    2. In the **Enter the object names to select** box, enter **wmiuser**. Select **Check Names** to verify the setting, and then select **OK**.

        The **wmiuser (wmiuser@DOMAIN.local)** is now listed in the **Access Permission** dialog.
    3. In the **Access Permission** dialog:

        1. In the **Group or user names** list, select **wmiuser**.
        2. In the **Permissions for ANONYMOUS LOGON** box, select **Allow** for both **Local Access** and **Remote Access**.

        Select **OK** to close the **Access Permissions** dialog.
5. Back in the **Group Policy Management Editor** window, make sure that you have **Computer Configuration &gt; Windows Settings &gt; Security Settings &gt; Local Policies &gt; Security Options** selected.
6. Navigate to and double-click the **DCOM: Machine Launch Restrictions in Security Descriptor Definition Language (SDDL) syntax** policy to open the properties window to the **Template Security Policy Setting** tab.

    Use the following steps to configure access for this policy:

    1. Select **Edit Security** and then in the **Access Permission** dialog, select **Add**.
    2. In the **Enter the object names to select** box, enter **wmiuser**. Select **Check Names** to verify the setting, and then select **OK**.

        The **wmiuser (wmiuser@DOMAIN.local)** is now listed in the **Access Permission** dialog.
    3. In the **Access Permission** dialog:

        1. In the **Group or user names** list, select **wmiuser**.
        2. In the **Permissions for Administrators** box, select **Allow** for the **Local Launch**, **Remote Launch**, **Local Activation**, and **Remote Activation** options.

        Select **OK** to close the **Access Permissions** dialog.

### Configure your firewall

Perform the following steps to create an inbound firewall rule that allows WMI traffic:

1. Navigate back to the **WMIAccess** GPO you created in Configure a Group Policy Object (GPO), and select **Edit**.
2. In the **Group Policy Management Editor** dialog, go to **Computer Configuration &gt; Windows Settings &gt; Security Settings** and expand the **Windows Defender Firewall with Advanced Security** node.
3. Under **Windows Defender Firewall with Advanced Security**, right-click **Inbound Rules** and select **New Rule...**
4. In the **New Inbound Rule Wizard**, select **Predefined** and then select **Windows Management Instrumentation** from the drop-down menu.
5. Select **Next** to continue. In the **Predefined Rules** pane, make sure that all rules in the **Rules** box are selected.
6. Select **Next** to continue, and then select **Allow the connection** &gt; **Finish**.

### Configure permissions for your WMI namespace

The following steps define permissions for your WMI namespace. You can't complete this configuration with a regular GPO.

If you'll be using a non-admin account to run your WEM scans, configuring WMI namespace permissions is critical and must be performed exactly as instructed to allow sign-in attempts using WMI.

1. On your Windows machine, open a **Run** dialog and enter **wmimgmt.msc**.
2. In the **wmimgmt - [Console Root\WMI Control (Local)]** dialog, right-click **WMI Control (Local)** and select **Properties**.
3. In the **WMI Control (Local) Properties** dialog, select the **Security** tab &gt; **Root** &gt; **Security**.
4. In the **Security for ROOT\SECURITY** dialog, make sure that the **wmiuser** account is listed in the **Group or user names** box:

    1. Select **Add**, and in the **Enter the object names to select** box, enter **wmiuser**.
    2. Select **Check Names** &gt; **OK**.
5. In the **Group or user names** box, select the **wmiuser** account. In the **Permissions for Authenticated Users** box, select **Allow** for the following permissions:

    - **Execute Methods**
    - **Enable Account**
    - **Remote Enable**
    - **Read Security**
6. In the **Security for ROOT\SECURITY** dialog, select **Advanced**. Then, in the **Advanced Security Settings for Root** dialog, select the **wmiuser** account &gt; **Edit**.
7. In the **Permissions Entry for Root** dialog, from the **Apply To** drop-down menu, select **This namespace and all subnamespaces**.

    Note

    You must apply permissions recursively to the entire tree.
8. Select **OK** until all dialog boxes you'd opened in this procedure are closed.

### Add your wmiuser account to the local Performance Log Users group

Perform the following steps to add the **wmiuser** account to the local **Performance Log Users** group:

1. Sign in to your Windows machine with a user you know is part of the **Performance Log Users** group.
2. Open a **Run** dialog and enter **compmgmt.msc**.
3. In the **Computer Management** dialog, select **Computer Management (Local) &gt; System Tools &gt; Local Users and Groups &gt; Groups** and double-click **Performance Log Users**.
4. Select **Add** and then, in the **Enter the object names to select**, enter **wmiuser** to add the **wmiuser** to the group. Select **Check Names** and then **OK** until all dialog boxes you'd opened in this procedure are closed.

## Configure a WEM scan on your sensor console

**To configure a WEM scan**:

1. On your OT sensor console, select **System settings** &gt; **Network monitoring** &gt; **Active discovery** &gt; **Windows Endpoint Monitoring (WMI)**.
2. In the **Edit scan ranges configuration** section, enter the ranges you want to scan and add the username and password required to access those resources.

    - We recommend entering values with domain or local administrator privileges for the best scanning results.
    - Select **Import ranges** to import a .csv file with a set of ranges you want to scan. Make sure your .csv file includes the following data: **FROM**, **TO**, **USER**, **PASSWORD**, **DISABLE**, where **DISABLE** is defined as **TRUE**/**FALSE**.
    - To get a .csv list of all ranges currently configured for WEM scans, select **Export ranges**.
3. In the **Scan will run** area, define whether you want to run the scan in intervals, every few hours, or by a specific time. If you select **By specific time**, an additional **Add scan time** option appears, which you can use to configure several scans running at specific times.

    While you can configure your WEM scan to run as often as you like, only one WEM scan can run at a time.
4. Select **Save** and then do one of the following:

    - To run your scan manually now, select **Apply changes** &gt; **Manually scan**.
    - To let your scan run later as configured, select **Apply changes**, and then close the pane as needed.

**To view scan results:**

1. When your scan is finished, go back to the **System settings** &gt; **Network monitoring** &gt; **Active discovery** &gt; **Windows Endpoint Monitoring (WMI)** page on your sensor console.
2. Select **View Scan Results**. A .csv file with the scan results is downloaded to your computer.