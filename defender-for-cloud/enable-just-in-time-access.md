---
layout: Conceptual
title: Enable Just-in-Time Access - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-just-in-time-access
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how just-in-time VM access (JIT) in Microsoft Defender for Cloud helps you control access to your Azure virtual machines.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1013
- ge-structured-content-pilot
ai-usage: ai-assisted
locale: en-us
document_id: 950f8d43-1e42-ff2a-1f47-bb0f563dcacf
document_version_independent_id: 30486397-72d5-fb08-da8f-5776e12f36c2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/enable-just-in-time-access.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/enable-just-in-time-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/enable-just-in-time-access.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
platformId: f4576550-5b9d-2ac5-0820-b1c106b4aaad
---

# Enable Just-in-Time Access - Microsoft Defender for Cloud | Microsoft Learn

[Defender for Servers](defender-for-servers-overview) in Microsoft Defender for Cloud provides a just-in-time (JIT) machine access feature.

You can use Microsoft Defender for Cloud's just-in-time access to protect your Azure virtual machines (VMs) from unauthorized network access. Firewalls often include allow rules that leave VMs exposed. JIT lets you allow access only when it's needed, on the required ports, and for the required time.

In this article, you learn how to set up and use just-in-time access, including how to:

- Enable just-in-time on VMs from the Azure portal or programmatically
- Request access to a VM that has just-in-time access enabled from the Azure portal or programmatically
- Audit just-in-time access activity to make sure your VMs are secured appropriately

## Prerequisites

- Enable [Microsoft Defender for Servers Plan 2](defender-for-servers-overview) on the subscription.
- Supported VMs: VMs deployed through Azure Resource Manager, VMs protected by Azure Firewall on the same virtual network (VNet) as the VM, and AWS EC2 instances (Preview).
- Unsupported VMs: VMs deployed with [classic deployment models](/en-us/azure/azure-resource-manager/management/deployment-models), VMs protected by Azure Firewalls controlled by [Azure Firewall Manager](/en-us/azure/firewall-manager/overview).
- To set up just-in-time access on your AWS VMs, [connect your AWS account](quickstart-onboard-aws) to Defender for Cloud.
- To create a JIT policy, the policy name, together with the targeted VM name, can't exceed 56 characters.
- You need **Reader** and **SecurityReader** permissions to view JIT status and parameters. A custom role can also provide this access.
- For a custom role, assign the permissions summarized in the following table. To create a least-privileged role for users that only need to request JIT access to a VM, use the [Set-JitLeastPrivilegedRole script](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/JIT%20Scripts/JIT%20Custom%20Role).

| User action | Permissions to set |
| --- | --- |
| Configure or edit a JIT policy for a VM | *Assign these actions to the role:*<br>- On the scope of a subscription (or resource group when using API or PowerShell only) that's associated with the VM:`Microsoft.Security/locations/jitNetworkAccessPolicies/write`<br>- On the scope of a subscription (or resource group when using API or PowerShell only) of VM:`Microsoft.Compute/virtualMachines/write` |
| Request JIT access to a VM | *Assign these actions to the user:*<br>- `Microsoft.Security/locations/jitNetworkAccessPolicies/initiate/action`<br>- `Microsoft.Security/locations/jitNetworkAccessPolicies/*/read`<br>- `Microsoft.Compute/virtualMachines/read`<br>- `Microsoft.Network/networkInterfaces/*/read`<br>- `Microsoft.Network/publicIPAddresses/read` |
| Read JIT policies | *Assign these actions to the user:*<br>- `Microsoft.Security/locations/jitNetworkAccessPolicies/read`<br>- `Microsoft.Security/locations/jitNetworkAccessPolicies/initiate/action`<br>- `Microsoft.Security/policies/read`<br>- `Microsoft.Security/pricings/read`<br>- `Microsoft.Compute/virtualMachines/read`<br>- `Microsoft.Network/*/read` |

Note

Only the `Microsoft.Security` permissions are relevant for AWS. To create a least-privileged role for users that only need to request JIT access to a VM, use the [Set-JitLeastPrivilegedRole script](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/JIT%20Scripts/JIT%20Custom%20Role).

## Work with JIT VM access using Microsoft Defender for Cloud

You can use Defender for Cloud or programmatically enable JIT VM access with your own custom options. You can also enable JIT with default, hard-coded parameters from Azure virtual machines.

**Just-in-time VM access** shows your VMs grouped into:

- **Configured**: VMs configured to support just-in-time VM access. This view shows:

    - the number of approved JIT requests in the last seven days
    - the last access date and time
    - the connection details configured
    - the last user
- **Not configured**: VMs without JIT enabled, but that can support JIT. Enable JIT for these VMs.
- **Unsupported**: VMs that don't support JIT because:

    - Missing network security group (NSG) or Azure Firewall. JIT requires an NSG to be configured or a Firewall configuration or both.
    - Classic VM. JIT supports VMs that are deployed through Resource Manager.
    - Other. The JIT solution is disabled in the security policy of the subscription or the resource group.

### Enable JIT on your VMs from Microsoft Defender for Cloud

From Defender for Cloud, you can enable and configure the JIT VM access.

To enable JIT on your VMs from Defender for Cloud:

1. Open **Workload protections** and, in the advanced protections, select **Just-in-time VM access**.

    [![Screenshot showing how to configure Just-in-time VM access in Microsoft Defender for Cloud.](media/just-in-time-access-usage/configure-just-in-time-access.gif)](media/just-in-time-access-usage/configure-just-in-time-access.gif#lightbox)
2. In the **Not configured** virtual machines tab, mark the VMs to protect with JIT and select **Enable JIT on VMs**.

    The JIT VM access page opens listing the ports that Defender for Cloud recommends protecting:

    - 22 - SSH
    - 3389 - RDP
    - 5985 - WinRM
    - 5986 - WinRM

    To customize the JIT access:

    1. Select **Add**.
    2. Select one of the ports in the list to edit it or enter other ports. For each port, you can set the:

        - **Protocol**
        - **Allowed source IPs**
        - **Maximum request time**
    3. Select **OK**.
3. To save the port configuration, select **Save**.

### Edit the JIT configuration on a JIT-enabled VM using Defender for Cloud

You can modify a VM's just-in-time configuration by adding and configuring a new port to protect for that VM, or by changing any other setting related to an already protected port.

To edit the existing JIT rules for a VM:

1. Open **Workload protections** and, in the advanced protections, select **Just-in-time VM access**.
2. In the **Configured** virtual machines tab, right-click on a VM and select **Edit**.
3. In the **JIT VM access configuration**, edit the list of ports or select **Add** for a new custom port.
4. When you finish editing the ports, select **Save**.

### Request access to a JIT-enabled VM from Microsoft Defender for Cloud

When a VM has JIT enabled, you need to request access to connect to it. You can request access in any supported way, regardless of how you enabled JIT.

To request access to a JIT-enabled VM from Defender for Cloud:

1. From the **Just-in-time VM access** page, select the **Configured** tab.
2. Select the VMs you want to access.

    - The icon in the **Connection Details** column indicates whether JIT is enabled on the network security group or firewall. If it's enabled on both, only the firewall icon appears.
    - The **Connection Details** column shows the user and ports that can access the VM.
3. Select **Request access**. The **Request access** window opens.
4. Under **Request access**, select the ports that you want to open for each VM, the source IP addresses that you want the port opened on, and the time window to open the ports.
5. Select **Open ports**.

    Note

    If a user who is requesting access is behind a proxy, enter the IP address range of the proxy.

## Other ways to work with JIT VM access

You can also manage just-in-time VM access through Azure virtual machines, PowerShell, or the REST API.

### Azure virtual machines

The following tasks show how to enable and request JIT access from the Azure virtual machines experience in the Azure portal.

#### Enable JIT on your VMs from Azure virtual machines

You can enable JIT on a VM from the Azure virtual machines pages of the Azure portal.

To enable JIT on a VM from Azure virtual machines:

Tip

If a VM already has JIT enabled, the VM configuration page shows that JIT is enabled. Use the **Just-in-time VM access** link on that page to open Defender for Cloud and review or change settings.

1. From the [Azure portal](https://portal.azure.com), search for and select **Virtual machines**.
2. Select the virtual machine you want to protect with JIT.
3. In the menu, select **Configuration**.
4. Under **Just-in-time access**, select **Enable just-in-time**.

    By default, just-in-time access for the VM uses these settings:

    - Windows machines:
        - RDP port: 3389
        - Maximum allowed access: 3 hours
        - Allowed source IP addresses: Any
    - Linux machines:
        - SSH port: 22
        - Maximum allowed access: 3 hours
        - Allowed source IP addresses: Any
5. To edit any of these values or add more ports to your JIT configuration, use Microsoft Defender for Cloud's just-in-time page:

    1. From Defender for Cloud's menu, select **Just-in-time VM access**.
    2. From the **Configured** tab, right-click on the VM to which you want to add a port, and select **Edit**.

        ![Screenshot of editing just-in-time VM access settings, showing allowed ports and access duration options.](media/just-in-time-access-usage/jit-policy-edit-security-center.png)
    3. Under **JIT VM access configuration**, you can either edit the existing settings of an already protected port or add a new custom port.
    4. When you finish editing the ports, select **Save**.

#### Request access to a JIT-enabled VM from the Azure virtual machine's connect page

When a VM has JIT enabled, you need to request access to connect to it. You can request access in any supported way, regardless of how you enabled JIT.

![Screenshot of a just-in-time VM access request showing selected ports and access duration.](media/just-in-time-access-usage/jit-request-vm.png)

To request access from Azure virtual machines:

1. In the Azure portal, open the virtual machines pages.
2. Select the VM to which you want to connect, and open the **Connect** page.

    Azure checks to see if JIT is enabled on that VM.

    - If JIT isn't enabled for the VM, you're prompted to enable it.
    - If JIT is enabled, select **Request access** to pass an access request with the requesting IP, time range, and ports that you configured for that VM.

Note

After a request is approved for a VM protected by Azure Firewall, Defender for Cloud provides the user with the connection details, including the port mapping from the DNAT table, to use to connect to the VM.

### PowerShell

You can also enable and request JIT access by using PowerShell cmdlets.

#### Enable JIT on your VMs using PowerShell

To enable just-in-time VM access from PowerShell, use the official Microsoft Defender for Cloud PowerShell cmdlet `Set-AzJitNetworkAccessPolicy`.

To configure JIT on a VM with PowerShell:

This example enables just-in-time VM access on a specific VM with the following rules:

- Close ports 22 and 3389
- Set a maximum time window of 3 hours for each so they can be opened per approved request
- Allow the user who is requesting access to control the source IP addresses
- Allow the user who is requesting access to establish a successful session upon an approved just-in-time access request

The following PowerShell commands create this JIT configuration:

1. Assign a variable that holds the just-in-time VM access rules for a VM:

    ```azurepowershell
    $JitPolicy = (@{
        id="/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUP/providers/Microsoft.Compute/virtualMachines/VMNAME";
        ports=(@{
            number=22;
            protocol="*";
            allowedSourceAddressPrefix=@("*");
            maxRequestAccessDuration="PT3H"},
            @{
            number=3389;
            protocol="*";
            allowedSourceAddressPrefix=@("*");
            maxRequestAccessDuration="PT3H"})})
    ```
2. Insert the VM just-in-time VM access rules into an array:

    ```azurepowershell
    $JitPolicyArr=@($JitPolicy)
    ```
3. Configure the just-in-time VM access rules on the selected VM:

    ```azurepowershell
    Set-AzJitNetworkAccessPolicy -Kind "Basic" -Location "LOCATION" -Name "default" -ResourceGroupName "RESOURCEGROUP" -VirtualMachine $JitPolicyArr
    ```

    Use the `-Name` parameter to specify the JIT policy name for each VM. For example, to establish the JIT configuration for two different VMs, VM1 and VM2, use: `Set-AzJitNetworkAccessPolicy -Name VM1` and `Set-AzJitNetworkAccessPolicy -Name VM2`.

#### Request access to a JIT-enabled VM using PowerShell

In the following example, you can see a just-in-time VM access request to a specific VM for port 22, for a specific IP address, and for a specific amount of time:

To request access to a JIT-enabled VM using PowerShell, run the following commands:

1. Configure the VM request access properties:

    ```azurepowershell
    $JitPolicyVm1 = (@{
        id="/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUP/providers/Microsoft.Compute/virtualMachines/VMNAME";
        ports=(@{
            number=22;
            endTimeUtc="2020-07-15T17:00:00.3658798Z";
            allowedSourceAddressPrefix=@("IPV4ADDRESS")})})
    ```
2. Insert the VM access request parameters in an array:

    ```azurepowershell
    $JitPolicyArr=@($JitPolicyVm1)
    ```
3. Send the request access (use the resource ID from step 1)

    ```azurepowershell
    Start-AzJitNetworkAccessPolicy -ResourceId "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUP/providers/Microsoft.Security/locations/LOCATION/jitNetworkAccessPolicies/default" -VirtualMachine $JitPolicyArr
    ```

Learn more in the [PowerShell cmdlet documentation](/en-us/powershell/scripting/developer/cmdlet/cmdlet-overview).

### REST API

You can manage JIT VM access programmatically by using the Microsoft Defender for Cloud REST API.

#### Enable JIT on your VMs using the REST API

The just-in-time VM access feature can be used with the Microsoft Defender for Cloud API. Use this API to get information about configured VMs, add new ones, request access to a VM, and more.

For more information, see [JIT network access policies](/en-us/rest/api/defenderforcloud-composite/jit-network-access-policies?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true).

#### Request access to a JIT-enabled VM using the REST API

The just-in-time VM access feature can be used with the Microsoft Defender for Cloud API. Use this API to get information about configured VMs, add new ones, request access to a VM, and more.

For more information, see [JIT network access policies](/en-us/rest/api/defenderforcloud-composite/jit-network-access-policies?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true).

## Audit JIT access activity in Defender for Cloud

Use log search to review VM activity. To view the logs:

1. From **Just-in-time VM access**, select the **Configured** tab.
2. For the VM that you want to audit, open the ellipsis menu at the end of the row.
3. Select **Activity Log** from the menu.

    ![Screenshot of selecting the just-in-time VM access activity log in Defender for Cloud.](media/just-in-time-access-usage/jit-select-activity-log.png)

    The activity log provides a filtered view of previous operations for that VM along with time, date, and subscription.
4. To download the log information, select **Download as CSV**.