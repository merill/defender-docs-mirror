---
layout: Conceptual
title: Enable Defender for Endpoint Integration in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-defender-for-endpoint
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
description: Learn how to enable Microsoft Defender for Endpoint integration in Microsoft Defender for Cloud to protect your multicloud and on-premises machines.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 16ecdef5-f17a-b465-e826-b18a5cc31db1
document_version_independent_id: dc5a73be-9684-26eb-998d-20c426d61f23
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/enable-defender-for-endpoint.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/enable-defender-for-endpoint
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/enable-defender-for-endpoint.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 117525b1-d4b8-d027-4e11-5b9ee1e9545a
---

# Enable Defender for Endpoint Integration in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud [integrates natively with Microsoft Defender for Endpoint](integration-defender-for-endpoint) to provide Defender for Endpoint and Defender Vulnerability Management capabilities in Defender for Cloud.

- When you enable the Defender for Servers plan in Defender for Cloud, Defender for Endpoint integration is enabled by default.
- The integration automatically deploys the Defender for Endpoint agent on machines.

This article explains how to manually enable Defender for Endpoint integration if it was previously turned off or if you have a legacy subscription that requires manual opt-in.

## Prerequisites

Before you enable Defender for Endpoint integration, review these requirements.

| Requirement | Details |
| --- | --- |
| **Windows support** | Verify that Windows machines are [supported by Defender for Endpoint](/en-us/defender-endpoint/configure-server-endpoints#windows-server-2012-r2-and-windows-server-2016). |
| **Linux support** | For Linux servers, you must have Python installed. Python 3 is recommended for all distros, but is required for RHEL 8.x and Ubuntu 20.04 or higher. Automatic deployment of the Defender for Endpoint sensor on Linux machines might not work as expected if machines run services that use [fanotify](/en-us/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint-linux#system-requirements). Manually install the Defender for Endpoint sensor on these machines. |
| **Azure VMs** | Check that virtual machines (VMs) can connect to the Defender for Endpoint service. If machines don't have direct access, proxy settings or firewall rules need to allow access to Defender for Endpoint URLs. Review [Windows proxy and internet configuration](/en-us/defender-endpoint/configure-proxy-internet) and [Linux static proxy configuration](/en-us/defender-endpoint/linux-static-proxy-configuration). |
| **On-premises VMs** | We recommend that you [onboard on-premises machines as Azure Arc-enabled VMs](/en-us/azure/azure-arc/servers/learn/quick-enable-hybrid-vm). If you [onboard on-premises VMs directly](onboard-machines-with-defender-for-endpoint), Defender for Servers Plan 1 features are available, but most Defender for Servers Plan 2 functionality doesn't work. |
| **Azure tenant** | If you moved your subscription between Azure tenants, some manual preparatory steps are also required. [Contact Microsoft support](https://portal.azure.com/#view/Microsoft_Azure_Support/HelpAndSupportBlade/%7E/overview) for details. |
| **Windows Server 2016, Windows Server 2012 R2** | Unlike later versions of Windows Server, which come with the Defender for Endpoint sensor preinstalled, Defender for Cloud installs the sensor on machines running Windows Server 2016/Windows Server 2012 R2 using the unified Defender for Endpoint solution. |

## Enable Defender for Endpoint integration on a subscription

When you enable a Defender for Servers plan, Defender for Endpoint integration is enabled by default. If you turn off integration on a subscription, you can manually turn it on again.

To enable Defender for Endpoint integration on a subscription:

1. Go to **Defender for Cloud** &gt; **Environment settings**.
2. Select the relevant subscription.
3. Go to **Settings and monitoring** &gt; **Endpoint protection**.
4. Set status to **On**.

    [![Screenshot of Status toggle that enables Microsoft Defender for Endpoint.](media/integration-defender-for-endpoint/enable-defender-for-endpoint.png)](media/integration-defender-for-endpoint/enable-defender-for-endpoint.png#lightbox)
5. Select **Continue**.
6. Select **Save**.

The Defender for Endpoint sensor is deployed to all Windows and Linux machines in the selected subscription.

Onboarding might take up to an hour. Defender for Cloud detects any previous Defender for Endpoint installations and reconfigures them to integrate with Defender for Cloud.

Note

For Azure VMs created from generalized operating system images, Microsoft Defender for Endpoint (MDE) isn't automatically provisioned through the Endpoint protection setting. You can manually enable the MDE agent and extension by using Azure CLI, REST API, or Azure Policy.

### Verify installation on Linux machines

To verify Defender for Endpoint sensor installation on a Linux machine:

1. Run the following shell command on each machine: `mdatp health`. If Microsoft Defender for Endpoint is installed, you see its health status:

    `healthy : true`

    `licensed: true`
2. Also, in the Azure portal, you can check that Linux machines have a new Azure extension called `MDE.Linux`.

Note

On new subscriptions, Defender for Endpoint integration is automatically enabled and covers machines running a supported Windows Server or Linux operating system. The Enable Defender for Endpoint unified solution on Windows Server 2016/2012 R2 and Enable on Linux machines sections cover one-time opt-in procedures that might be required for legacy subscriptions.

## Enable Defender for Endpoint unified solution on Windows Server 2016/2012 R2

If you enabled Defender for Servers and turned on Defender for Endpoint integration in a subscription that you created before spring 2022, you might need to manually enable integration of the unified solution for machines running Windows Server 2016 or Windows Server 2012 R2 in the subscription.

1. Go to **Defender for Cloud** &gt; **Environment settings**.
2. Select the relevant subscription.
3. In the Monitoring coverage column of the Defender for Servers plan, select **Settings**.

    The status of the Endpoint protections component is **Partial**, which means that not all parts of the component are enabled.
4. Select **Fix** to see the components that aren't enabled.

    [![Screenshot of Fix button that enables Microsoft Defender for Endpoint support.](media/integration-defender-for-endpoint/fix-defender-for-endpoint.png)](media/integration-defender-for-endpoint/fix-defender-for-endpoint.png#lightbox)
5. Go to **Missing components** &gt; **Unified solution**.
6. Select **Enable**.

    [![Screenshot of enabling the use of the Defender for Endpoint unified solution for Windows Server 2012 R2 and 2016 machines.](media/integration-defender-for-endpoint/enable-defender-for-endpoint-unified-small.png)](media/integration-defender-for-endpoint/enable-defender-for-endpoint-unified.png#lightbox)

    The Defender for Endpoint agent automatically installs on Windows Server 2012 R2 and 2016 machines connected to Microsoft Defender for Cloud.
7. Select **Save**.
8. In **Settings and monitoring**, select **Continue**.

Defender for Cloud onboards existing and new machines to Defender for Endpoint.

If you're configuring Defender for Endpoint on the first subscription in your tenant, onboarding might take up to 12 hours. For new machines and subscriptions that you create after enabling the integration, onboarding takes up to an hour.

Note

Enabling Defender for Endpoint integration on Windows Server 2012 R2 and Windows Server 2016 machines is a one-time action. If you disable the Defender for Servers plan and then re-enable it, integration stays enabled.

## Enable on Linux machines (plan/integration enabled)

If Defender for Servers is already enabled and Defender for Endpoint integration is on in a subscription that existed before summer 2021, you might need to manually enable the integration for Linux machines.

1. Go to **Defender for Cloud** &gt; **Environment settings**.
2. Select the relevant subscription.
3. In the Monitoring coverage column of the Defender for Servers plan, select **Settings**.

    The status of the **Endpoint protections** component is **Partial**, meaning that not all parts of the component are enabled.
4. Select **Fix** to see the components that aren't enabled.

    ![Screenshot of Fix button that enables Microsoft Defender for Endpoint support.](media/integration-defender-for-endpoint/fix-defender-for-endpoint.png)
5. In **Missing components** &gt; **Linux machines**, select **Enable**.

    [![Screenshot of enabling the integration between Defender for Cloud and Microsoft's EDR solution, Microsoft Defender for Endpoint for Linux.](media/integration-defender-for-endpoint/enable-defender-for-endpoint-linux-small.png)](media/integration-defender-for-endpoint/enable-defender-for-endpoint-linux.png#lightbox)
6. Select **Save**.
7. In **Settings and monitoring**, select **Continue**.

    - Defender for Cloud onboards Linux machines to Defender for Endpoint.
    - Defender for Cloud detects any previous Defender for Endpoint installations on Linux machines and reconfigures them to integrate with Defender for Cloud.
    - If you're configuring Defender for Endpoint on the first subscription in your tenant, onboarding might take up to 12 hours. For new machines created after the integration has been enabled, onboarding takes up to an hour.
8. To verify Defender for Endpoint sensor installation on a Linux machine, run the following shell command on each machine.

    `mdatp health`

    If Microsoft Defender for Endpoint is installed, you see its health status:

    `healthy : true`

    `licensed: true`
9. In the Azure portal, you can check that Linux machines have a new Azure extension called `MDE.Linux`.

Note

Enabling Defender for Endpoint integration on Linux machines is a one-time action. If you disable the Defender for Servers plan and re-enable it, integration remains enabled.

## Enable integration with PowerShell in multiple subscriptions

To enable Defender for Servers integration for Linux machines or Windows Server 2012 R2 and 2016 with the Microsoft Defender for Endpoint (MDE) Unified solution on multiple subscriptions, use one of the [PowerShell scripts in the Defender for Cloud GitHub repository](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/MDE%20Integration).

- Use the [Enable MDE unified solution script](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/MDE%20Integration/Enable%20MDE%20Unified%20solution) to enable integration with the Defender for Endpoint modern unified solution on Windows Server 2012 R2 or Windows Server 2016.
- Use the [Enable MDE integration for Linux script](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/MDE%20Integration/Enable%20MDE%20Integration%20for%20Linux) to enable Defender for Endpoint integration on Linux machines.

### Manage automatic updates for Linux

In Windows, Defender for Endpoint version updates are provided through continuous knowledge base updates. In Linux, you need to update the Defender for Endpoint package.

- When you use Defender for Servers with the `MDE.Linux` extension, automatic updates for Microsoft Defender for Endpoint are enabled by default.
- If you want to manage version updates manually, you can disable automatic updates on your machines. To do this, add the following tag for machines onboarded with the `MDE.Linux` extension.

    - Tag name: `ExcludeMdeAutoUpdate`
    - Tag value: `true`

This configuration is supported for Azure VMs and Azure Arc machines, where the `MDE.Linux` extension initiates autoupdate.

## Enable integration at scale

You can enable the Defender for Endpoint integration at scale through the supplied REST API version 2022-05-01. For full details, see the [API documentation](/en-us/rest/api/defenderforcloud-composite/settings/update?view=rest-defenderforcloud-composite-latest&amp;tabs=HTTP&amp;preserve-view=true).

The following example shows the request body for the PUT request that enables Defender for Endpoint integration. This `Microsoft.Security/settings` resource configuration sets the `WDATP` setting to enabled, which activates the Defender for Endpoint integration programmatically for the specified subscription.

URI: `https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.Security/settings/WDATP?api-version=2022-05-01`

```json
{
    "name": "WDATP",
    "type": "Microsoft.Security/settings",
    "kind": "DataExportSettings",
    "properties": {
        "enabled": true
    }
}
```

Note

Both the Defender for Endpoint Unified Solution and Defender for Endpoint for Linux are automatically included on new subscriptions when you enable the Defender for Endpoint integration by using `microsoft.security/settings/WDATP`.

The settings `WDATP_UNIFIED_SOLUTION` and `WDATP_EXCLUDE_LINUX_PUBLIC_PREVIEW` are relevant for legacy subscriptions. These settings apply to subscriptions that already have the Defender for Endpoint integration enabled when these features were introduced in August 2021 and Spring 2022.

## Track Defender for Endpoint deployment status

You can use the [Defender for Endpoint deployment status workbook](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Workbooks/Defender%20for%20Servers%20Deployment%20Status) to track the Defender for Endpoint deployment status on your Azure VMs and Azure Arc-enabled VMs. The interactive workbook provides an overview of machines in your environment showing their Defender for Endpoint extension deployment status.

## Access the Microsoft Defender portal

To access the Microsoft Defender portal from Defender for Cloud, complete the following steps:

1. Ensure you have the [right permissions for portal access](/en-us/microsoft-365/security/defender-endpoint/assign-portal-access).
2. Check whether you have a proxy or firewall that blocks anonymous traffic.

    - The Defender for Endpoint sensor connects from the system context, so you must permit anonymous traffic.
    - To ensure unhindered access to the Microsoft Defender portal, [enable access to service URLs in the proxy server](/en-us/microsoft-365/security/defender-endpoint/configure-proxy-internet#enable-access-to-microsoft-defender-for-endpoint-service-urls-in-the-proxy-server).
3. Open the [Microsoft Defender portal](https://security.microsoft.com/). Learn about [Incidents and alerts in the Microsoft Defender portal](/en-us/defender-xdr/incidents-overview).

## Run a detection test

To run a detection test, see [EDR detection test for verifying device's onboarding and reporting services](/en-us/defender-endpoint/edr-detection).

## Remove Defender for Endpoint from a machine

To remove the Defender for Endpoint solution from your machines:

1. To disable the integration, in Defender for Cloud, go to **Environment settings**, then select the subscription with the relevant machines.
2. In the Defender plans page, select **Settings & Monitoring**.
3. In the status of the **Endpoint protection** component, select **Off** to disable the integration with Defender for Endpoint for the subscription.
4. Select **Continue** and **Save** to save your settings.
5. Remove the `MDE.Windows` or `MDE.Linux` extension from the machine.
6. [Offboard the device from the Microsoft Defender for Endpoint service](/en-us/defender-endpoint/offboard-machines).

### Remove Defender for Endpoint integration tags

When you onboard a **Windows** device through Defender for Cloud, Defender for Endpoint creates registry values related to Defender for Cloud. These registry tags remain on the device after offboarding and don’t affect functionality.

To remove these tags completely, follow these steps. On Linux, the system stores this information internally and doesn't show it in the registry.

1. Select **Start**, enter *regedit*, and select **Enter** to open **Registry Editor**.
2. In the left pane, go to:

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Advanced Threat Protection\DeviceTags`
3. Delete these value names if they exist:

    - `AzureResourceId`
    - `SecurityWorkspaceId`
    - `SecurityAgentId`

Important

Editing the registry incorrectly might cause issues on your device.