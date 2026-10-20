---
layout: Conceptual
title: Onboard servers to Microsoft Defender - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/onboard-server
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Choose automatic or manual endpoint deployment and verify server onboarding.
ms.service: defender-endpoint
ms.author: kschwabacher
author: paulinbar
ms.localizationpriority: medium
ms.reviewer: pahuijbr
ms.collection:
- m365-security
- tier2
ms.topic: install-set-up-deploy
ms.subservice: onboard
ms.date: 2026-09-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: de90e20d-7fd0-579e-d0a5-a3203b19310e
document_version_independent_id: de90e20d-7fd0-579e-d0a5-a3203b19310e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/onboard-server.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: onboard-server
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/onboard-server.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 25b1fe44-e7b6-36eb-7a98-ac56ea0bca82
---

# Onboard servers to Microsoft Defender - Microsoft Defender for Endpoint | Microsoft Learn

Use this guide to prepare and onboard new servers. Defender for Endpoint can help protect your organization's servers with capabilities that include posture management, threat protection, endpoint detection and response, and integration with Defender for Servers.

For servers already running Defender for Endpoint, see [Existing deployments](azure-server-integration#servers-already-running-defender-for-endpoint). Those servers don't require onboarding, reinstallation, or migration to maintain their existing Defender for Endpoint protection.

Tip

For a customized experience based on your environment, you can access the [Security Analyzer automated setup guide](https://go.microsoft.com/fwlink/p/?linkid=2268615) in the Microsoft 365 admin center.

## Choose a deployment method

| Server | Method |
| --- | --- |
| Supported Azure VM or Azure Arc-enabled server in an enabled subscription | Automatic onboarding |
| Server you manage through an endpoint deployment tool | Manual deployment |
| Server already reporting to Defender for Endpoint | [No deployment changes required](azure-server-integration#servers-already-running-defender-for-endpoint) |

## Prerequisites

- Meet the [minimum requirements for Defender for Endpoint](minimum-requirements) and [connectivity requirements](configure-device-connectivity).
- Before automatic or manual deployment, review [antivirus coexistence](mde-side-by-side) and [Windows Server passive-mode requirements](microsoft-defender-antivirus-compatibility#windows-server-and-passive-mode) if another antivirus application is installed.
- Confirm the permissions required by your deployment method.
- Identify existing agents and deployment policies to avoid competing assignments.

### Prepare the rollout

- Record the target servers, operating systems, responsible owners, and required protection features.
- Agree on a change window and the method for [offboarding](offboard-machines) or reinstalling endpoint software if needed.
- For methods that support a pilot, start with representative servers. Expand after completing the onboarding checks and [access checks](azure-server-integration#verify-rbac-and-server-access).

Before choosing Direct onboarding, review its [tenant-wide scope](/en-us/azure/defender-for-cloud/onboard-machines-with-defender-for-endpoint#who-is-affected). You can't limit Direct onboarding to a pilot group.

## Server plans

To onboard servers to Defender for Endpoint, [server licenses](/en-us/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-365-security-compliance-licensing-guidance#microsoft-defender-for-endpoint) are required. You can choose from these options:

- [Microsoft Defender for Servers Plan 1 or Plan 2](/en-us/azure/defender-for-cloud/defender-for-servers-overview) (as part of the Defender for Cloud) offering
- Microsoft Defender for Endpoint for servers
- [Microsoft Defender for Business servers](/en-us/defender-business/get-defender-business#how-to-get-microsoft-defender-for-business-servers) (for small and medium-sized businesses only)

Tip

For most organizations, Microsoft recommends onboarding servers through **Microsoft Defender for Servers Plan 2** as part of [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/defender-for-servers-overview). Plan 2 includes Defender for Endpoint server protection and capabilities specific to server workloads:

- Agentless machine scanning for vulnerabilities, malware, and secrets
- File integrity monitoring
- Just-in-time virtual machine access
- Regulatory compliance assessment
- Premium Microsoft Defender Vulnerability Management capabilities
- Operating system configuration assessment based on the Microsoft Cloud Security Benchmark
- A 500-MB daily data ingestion benefit for each protected machine

Defender for Cloud automatically onboards the Defender for Endpoint extension to supported Azure virtual machines and Azure Arc-enabled machines, so you don't need per-machine onboarding scripts. For a feature comparison, see [Defender for Servers plan features](/en-us/azure/defender-for-cloud/defender-for-servers-overview#plan-protection-features).

If your organization doesn't use Defender for Cloud, the standalone Microsoft Defender for Endpoint for servers and Microsoft Defender for Business servers licenses are alternatives.

## Integration with Microsoft Defender for Servers

Defender for Endpoint integrates seamlessly with [Defender for Servers](/en-us/azure/defender-for-cloud/defender-for-servers-overview) (in Defender for Cloud). If your subscription includes Defender for Servers Plan 1 or Plan 2, you can:

- Onboard servers automatically
- Have servers that are monitored by Defender for Cloud appear in the Microsoft Defender portal, in the device inventory
- Conduct detailed investigations as a Defender for Cloud customer

Here are a few things to keep in mind:

- When you use Defender for Cloud to monitor servers, a Defender for Endpoint tenant is created automatically. Data collected by Defender for Endpoint is stored in the geographical location of the tenant, identified during provisioning.
- If you use Defender for Endpoint before using Defender for Cloud, your data is stored in the location you specified when you created your tenant, even if you integrate with Defender for Cloud at a later time.
- Once configured, you can't change the location of where your data is stored. To move your data to another location, [contact support](contact-support) to reset your tenant.
- Server endpoint monitoring utilizing this integration isn't currently available for Office 365 GCC customers.
- Linux servers onboarded through Defender for Cloud have their initial configuration set to run Microsoft Defender Antivirus in [passive mode](microsoft-defender-antivirus-compatibility#microsoft-defender-antivirus-and-non-microsoft-antivirusantimalware-solutions). For information on how to deploy Defender for Endpoint on Linux server, start with the [Prerequisites for Microsoft Defender for Endpoint on Linux](mde-linux-prerequisites).

For more information, see [Protect your endpoints with Defender for Endpoint integration with Defender for Cloud](/en-us/azure/defender-for-cloud/integration-defender-for-endpoint).

## Onboard automatically

1. [Enable Defender for Servers](/en-us/azure/defender-for-cloud/tutorial-enable-servers-plan) on the subscription containing the Azure VM or Azure Arc resource.
2. Review [Defender for Endpoint integration settings and prerequisites](/en-us/azure/defender-for-cloud/enable-defender-for-endpoint).
3. Allow deployment to complete, and then perform the onboarding checks.

## Important information for non-Microsoft antivirus/anti-malware solutions

If you intend to use a non-Microsoft anti-malware solution, you need to run Microsoft Defender Antivirus in passive mode. Make sure to set passive mode during the installation and onboarding process. For more information, see [Windows Server and passive mode](microsoft-defender-antivirus-compatibility#windows-server-and-passive-mode).

Important

If you're installing Defender for Endpoint on servers running McAfee Endpoint Security or VirusScan Enterprise, the McAfee platform version might need to be updated to ensure that Microsoft Defender Antivirus isn't removed or disabled. For more information on specific version numbers required, see the [McAfee Knowledge Center article](https://kcm.trellix.com/corporate/index?page=content&amp;id=KB88214).

## Deploy Defender for Endpoint manually

Choose the deployment method that matches your server and management approach. Follow the linked procedure in the following table to complete deployment, including downloading any required installation or onboarding packages.

| Operating system | Deployment method |
| --- | --- |
| Windows Server 2012 R2 and later, Windows Server version 1803, and Azure Stack HCI OS version 23H2 and later | [Local script](configure-endpoints-script) (uses an onboarding package)[Microsoft Configuration Manager](/en-us/intune/configmgr/protect/deploy-use/defender-advanced-threat-protection)[Group Policy](configure-endpoints-gp)[VDI scripts](configure-endpoints-vdi)Modern, unified solution for Windows Server 2016 and 2012 R2 |
| Linux | [Installer script-based deployment](linux-installer-script)[Ansible-based deployment](linux-install-with-ansible)[Chef-based deployment](linux-deploy-defender-for-endpoint-with-chef)[Puppet-based deployment](linux-install-with-puppet)[Saltstack-based deployment](linux-install-with-saltack)[Manual deployment](linux-install-manually) (uses a local script)[Deployment guidance for Defender for Endpoint on Linux for SAP](mde-linux-deployment-on-sap) |

### Onboard Windows Server, version 1803, Windows Server 2019 and later, and Azure Stack HCI OS

1. Review the [minimum requirements for Defender for Endpoint](minimum-requirements).
2. Use Choose a deployment method to select the appropriate onboarding method for your server.
3. If you're deploying Defender for Endpoint manually, follow Deploy Defender for Endpoint manually for the selected method.
4. Complete the onboarding checks after deployment.

### Onboard Windows Server 2016 and Windows Server 2012 R2

1. Review the [minimum requirements for Defender for Endpoint](minimum-requirements) and the prerequisites for Windows Server 2016 and Windows Server 2012 R2.
2. Use Choose a deployment method to select the appropriate onboarding method for your server.
3. If you're deploying Defender for Endpoint manually, follow Deploy Defender for Endpoint manually for the selected method.
4. Complete the onboarding checks after deployment.

Note

The installation package for Windows Server 2016 and Windows Server 2012 R2 is updated monthly. If your deployment method requires the installation package, download the latest package before deployment. To update after installation, you don't have to run the installer package again. If you do, the installer asks you to offboard first because offboarding is required for uninstallation. See Update packages for Defender for Endpoint on Windows Server 2012 R2 and 2016.

If you're migrating from the previous Microsoft Monitoring Agent (MMA)-based solution, see [Migrate servers from Microsoft Monitoring Agent to the modern unified solution](server-migration).

#### Prerequisites for Windows Server 2016 and 2012 R2

- It's recommended to install the latest available Servicing Stack Update (SSU) and Latest Cumulative Update (LCU) on the server.
- The SSU from September 14, 2021 or later must be installed.
- The LCU from September 20, 2018 or later must be installed.
- Enable the Microsoft Defender Antivirus feature and ensure it's up to date. For more information on enabling Defender Antivirus on Windows Server, see [Re-enable Defender Antivirus on Windows Server if it was disabled](enable-update-mdav-to-latest-ws#re-enable-microsoft-defender-antivirus-on-windows-server-if-it-was-disabled) and [Re-enable Defender Antivirus on Windows Server if it was uninstalled](enable-update-mdav-to-latest-ws#re-enable-microsoft-defender-antivirus-on-windows-server-if-it-was-uninstalled).
- Download and install the latest platform version using Windows Update. Alternatively, download the update package manually from the [Microsoft Update Catalog](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4052623) or from [MMPC](https://go.microsoft.com/fwlink/?linkid=870379&amp;arch=x64).
- On Windows Server 2016, Microsoft Defender Antivirus must be installed as a feature and fully updated before installation.

#### Update packages for Windows Server 2016 or Windows Server 2012 R2

To receive regular product improvements and fixes for the Defender for Endpoint component, ensure Windows Update [KB5005292](https://go.microsoft.com/fwlink/?linkid=2168277) gets applied or approved. In addition, to keep protection components updated, see [Manage Microsoft Defender Antivirus updates and apply baselines](microsoft-defender-endpoint-releases#microsoft-defender-antivirus-releases).

If you're using Windows Server Update Services (WSUS) and/or [Microsoft Configuration Manager](/en-us/intune/configmgr/core/understand/introduction), this new "Microsoft Defender for Endpoint update for EDR Sensor" is available under the category "Microsoft Defender for Endpoint."

### Functionality in the modern unified solution for Windows Server 2016 and Windows Server 2012 R2

The previous implementation (before April 2022) of onboarding Windows Server 2016 and Windows Server 2012 R2 required the use of Microsoft Monitoring Agent (MMA). The modern, unified solution package makes it easier to onboard servers by removing dependencies and installation steps. It also provides a much expanded feature set. For more information, see the following resources:

- [Server migration scenarios from the previous, MMA-based Microsoft Defender for Endpoint solution](server-migration)
- [Tech Community Blog: Defending Windows Server 2012 R2 and 2016](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/defending-windows-server-2012-r2-and-2016/ba-p/2783292)

Depending on the server that you're onboarding, the unified solution installs Defender for Endpoint and/or the EDR sensor on the server. The following table indicates what component is installed and what is built in by default.

| Server version | Microsoft Defender Antivirus | EDR sensor |
| --- | --- | --- |
| Windows Server 2012 R2 | ![Yes](media/svg/check-yes.svg) | ![Yes](media/svg/check-yes.svg) |
| Windows Server 2016 | Built-in | ![Yes](media/svg/check-yes.svg) |
| Windows Server 2019 and later | Built-in | Built-in |

#### Known issues and limitations in the modern unified solution

The following points apply to Windows Server 2016 and Windows Server 2012 R2:

- Always download the latest installer package from the Microsoft Defender portal (https://security.microsoft.com) before performing a new installation and ensure prerequisites are met. After installation, ensure to regularly update using component updates described in the section Update packages for Defender for Endpoint on Windows Server 2012 R2 and 2016.
- An operating system update can introduce an installation issue on machines with slower disks due to a time out with service installation. Installation fails with the message `Couldn't find c:\program files\windows defender\mpasdesc.dll, - 310 WinDefend`. Use the latest installation package, and the latest [install.ps1](https://github.com/microsoft/mdefordownlevelserver) script to help clear the failed installation if necessary.
- The user interface on Windows Server 2016 and Windows Server 2012 R2 only allows for basic operations. To perform operations on a device locally, refer to [Manage Defender for Endpoint with PowerShell, WMI, and MPCmdRun.exe](preferences-setup). As a result, features that specifically rely on user interaction, such as where the user is prompted to make a decision or perform a specific task, might not work as expected. It's recommended to disable or not enable the user interface nor require user interaction on any managed server as it may impact protection capability.
- Not all attack surface reduction rules are applicable to all operating systems. See [Attack surface reduction rules](attack-surface-reduction-rules-reference).
- Operating system upgrades are supported on Windows 10 and 11, and Windows Server 2019 or later. These versions include the necessary Defender for Endpoint components. For Windows Server 2016 and earlier, you must offboard from Defender for Endpoint and uninstall Defender for Endpoint before upgrading the OS.
- To automatically deploy and onboard the new solution using Microsoft Configuration Manager, you need to be on [version 2207 or later](/en-us/intune/configmgr/core/plan-design/changes/whats-new-in-version-2207#improved-microsoft-defender-for-endpoint-mde-onboarding-for-windows-server-2012-r2-and-windows-server-2016). You can still configure and deploy using version 2107 with the hotfix rollup, but this requires extra deployment steps. See [Microsoft Configuration Manager migration scenarios](server-migration#microsoft-endpoint-configuration-manager-migration-scenarios) for more information.

## Onboard Linux servers

To onboard servers running Linux, follow these steps:

1. Make sure to review the [Prerequisites for Microsoft Defender for Endpoint on Linux](mde-linux-prerequisites).
2. Choose a deployment method. Depending on your particular environment, you can choose from several options:

    - [Installer script based deployment](linux-installer-script)
    - [Ansible based deployment](linux-install-with-ansible)
    - [Chef based deployment](linux-deploy-defender-for-endpoint-with-chef)
    - [Puppet based deployment](linux-install-with-puppet)
    - [Saltstack based deployment](linux-install-with-saltack)
    - [Manual deployment](linux-install-manually) (uses a local script)
    - [Direct onboarding with Defender for Cloud](/en-us/azure/defender-for-cloud/onboard-machines-with-defender-for-endpoint)
    - [Connect your non-Azure machines to Microsoft Defender for Cloud with Defender for Endpoint](/en-us/azure/defender-for-cloud/quickstart-onboard-machines)
    - [Deployment guidance for Defender for Endpoint on Linux for SAP](mde-linux-deployment-on-sap)
3. Configure your capabilities. See [Configure security settings in Microsoft Defender for Endpoint on Linux](linux-preferences).

## Associate non-Azure servers by using Direct onboarding

If manually onboarded on-premises servers need Defender for Servers coverage, follow [Direct onboarding](/en-us/azure/defender-for-cloud/onboard-machines-with-defender-for-endpoint). Review [who is affected](/en-us/azure/defender-for-cloud/onboard-machines-with-defender-for-endpoint#who-is-affected) before enabling it.

Direct onboarding isn't required merely to keep an existing Defender for Endpoint deployment operating.

## Verify onboarding

1. Check local agent health using the instructions for the selected method.
2. Find the server in the Microsoft Defender device inventory. Check its identity, sensor health, and recent activity.
3. Run an approved [detection test](run-detection-test) and confirm that the alert arrives.
4. If Defender for Servers is required, verify its plan and subscription association in Defender for Cloud.

    Note

    Running Microsoft Defender Antivirus isn't required but it's recommended. If another antivirus vendor product is the primary endpoint protection solution, you can run Defender Antivirus in Passive mode. You can only confirm that passive mode is on after verifying that Defender for Endpoint sensor (SENSE) is running.
5. On Windows Server devices that should have Microsoft Defender Antivirus installed in active mode, run the following command:

    ```cmd
    sc.exe query Windefend
    ```

    If the result is, "The specified service doesn't exist as an installed service," then you need to install Microsoft Defender Antivirus.
6. Run the following command to verify that Defender for Endpoint is running:

    ```cmd
    sc.exe query sense
    ```

    The result should show it's running. If you encounter issues with onboarding, see [Troubleshoot onboarding](troubleshoot-onboarding).

## Offboard Windows servers

For automatic Azure offboarding, manual endpoint offboarding, and separate software-removal checks, see [Offboard servers from Microsoft Defender](offboard-machines#offboard-servers).

You can manually offboard Windows servers by using the same methods that are available for Windows client devices:

- [Offboard devices using Configuration Manager](configure-endpoints-sccm#offboard-devices-using-configuration-manager)
- [Offboard devices using Mobile Device Management tools](configure-endpoints-mdm#offboard-devices-using-mobile-device-management-tools)
- [Offboard devices using Group Policy](configure-endpoints-gp#offboard-devices-using-group-policy)
- [Offboard devices using a local script](configure-endpoints-script#offboard-devices-using-a-local-script)

After offboarding, you can proceed to uninstall the unified solution package on Windows Server 2016 and Windows Server 2012 R2. For previous versions of Windows Server, you have two options to offboard Windows servers from the service:

- Uninstall the MMA agent
- Remove the Defender for Endpoint workspace configuration

Note

These offboarding instructions for other Windows Server versions also apply if you're running the previous Defender for Endpoint for Windows Server 2016 and Windows Server 2012 R2 that requires the MMA. Instructions to migrate to the new unified solution are at [Server migration scenarios in Defender for Endpoint](server-migration).