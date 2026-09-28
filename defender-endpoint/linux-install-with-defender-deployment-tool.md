---
layout: Conceptual
title: Deploy Microsoft Defender endpoint security to Linux devices using the Defender deployment tool (preview) - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/linux-install-with-defender-deployment-tool
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the Defender deployment tool to install and onboard Microsoft Defender for Endpoint on Linux devices and verify deployment.
ms.reviewer: meghapriya
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-linux
ms.topic: install-set-up-deploy
ms.subservice: linux
ms.date: 2026-09-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 5301563f-90a8-bf1e-23bc-ba89d0b6b717
document_version_independent_id: 5301563f-90a8-bf1e-23bc-ba89d0b6b717
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/linux-install-with-defender-deployment-tool.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: linux-install-with-defender-deployment-tool
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/linux-install-with-defender-deployment-tool.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: d34c13e7-df03-0a2d-86b0-8e909dd40545
---

# Deploy Microsoft Defender endpoint security to Linux devices using the Defender deployment tool (preview) - Microsoft Defender for Endpoint | Microsoft Learn

The Defender deployment tool provides an efficient, user-friendly onboarding process for Microsoft Defender for Endpoint on Linux devices. It allows users to install and onboard Microsoft Defender for Endpoint using a single package that can be downloaded from the Microsoft Defender portal. This eliminates the need to install Defender using installer script/cli commands and then, separately, to onboard the device using the onboarding package from the portal.

The defender-deployment tool supports both manual and bulk onboarding through third-party tools such as Chef, Ansible, Puppet, and SaltStack. The tool supports several parameters you can use to customize large scale deployments, making it possible to have tailored installations across diverse environments.

## Prerequisites and system requirements

Before you get started, see [Prerequisites for Microsoft Defender for Endpoint on Linux](mde-linux-prerequisites) for a description of prerequisites and system requirements. Additionally, the following requirements also need to be met:

- Outbound HTTPS access on port 443 to `msdefender.download.prss.microsoft.com`. This deployment tool download endpoint is required in addition to the core Defender for Endpoint service endpoints used by [streamlined connectivity](streamlined-device-connectivity-urls-commercial). Before you begin deployment, run the connectivity test, which checks whether the required URLs are accessible.
- The endpoint must have either **wget** or **curl** installed.

The deployment tool enforces the following set of prerequisites checks, which if not met will abort the deployment process:

- Device memory: Greater than 1 GB
- Available disk space on the device: Greater than 2GB
- Glibc library version on the device: Newer than 2.17
- Defender build version: Must be supported and not expired. To check the product expiration date, run the command `-mdatp health`.

Tip

Before running the deployment tool to onboard Defender onto your Linux server, it's recommended to run the tool with the `--pre-req` option to help identify and fix any potential issues that might impact the deployment.

## Deployment: Step-by-step guide

1. Download the Defender deployment tool from the Defender portal using the following steps.

    1. Go to **Settings** &gt; **Endpoints** &gt; **Device management** &gt; **Onboarding**.
    2. In the Step 1 drop-down menu, select **Linux** as the operating system.
    3. Under **Download and apply onboarding packages or files**, select the **Download package** button under **Defender deployment tool**.

    Note

    Since this package installs and onboards the agent, it's a tenant specific package and must not be used across tenants.

    [![Screenshot showing the download package button.](media/linux-install-with-defender-deployment-tool/deployment-tool-download-package.png)](media/linux-install-with-defender-deployment-tool/deployment-tool-download-package.png#lightbox)
2. From a command prompt, extract the contents of the archive:

    ```bash
    unzip GatewayLinuxDefenderDeploymentTool.zip
    ```

    ```console
    Archive: GatewayLinuxDefenderDeploymentTool.zip
    inflating: defender_deployment_tool.sh
    ```
3. Grant executable permissions to the script.

    ```bash
    chmod +x defender_deployment_tool.sh
    ```
4. Run the script using the following command to install and onboard Microsoft Defender for Endpoint on your endpoint.

    ```bash
    sudo bash defender_deployment_tool.sh
    ```

    This command installs the latest agent version from the production channel and onboards the device to Defender portal. It might take 5-20 minutes for the device to show up in the [Device Inventory](https://security.microsoft.com/machines?category=all-devices).

    Note

    If you have set up a system-wide proxy to redirect Defender for Endpoint traffic, make sure you configure the proxy using the Defender deployment tool as well. Refer to the command-line help (--help) for available proxy options.
5. You can further customize deployment by passing parameters to the tool based on your requirements. Use the option `--help` to see all the available options:

    ```bash
     ./defender_deployment_tool.sh --help
    ```

    [![Screenshot showing the help command output.](media/linux-install-with-defender-deployment-tool/deployment-tool-help.png)](media/linux-install-with-defender-deployment-tool/deployment-tool-help.png#lightbox)

    The following table provides examples of commands for useful scenarios.

    | **Scenario** | **Command** |
    | --- | --- |
    | Check for unmet prerequisites | `sudo ./defender_deployment_tool.sh --pre-req` |
    | Run the connectivity test | `sudo ./defender_deployment_tool.sh --connectivity-test` |
    | Deploy to a custom location | `sudo ./defender_deployment_tool.sh --install-path /usr/microsoft/` |
    | Deploy from a locally configured package repository | `sudo ./defender_deployment_tool.sh --use-local-repo`This option can't be combined with `--channel` or `--clean`. |
    | Deploy from a specific channel | `sudo ./defender_deployment_tool.sh --channel insiders-slow` |
    | Deploy using a proxy | `sudo ./defender_deployment_tool.sh --http-proxy <http://username:password@proxy_host:proxy_port>` |
    | Deploy a specific agent version | `sudo ./defender_deployment_tool.sh --mdatp 101.25042.0003 --channel prod` |
    | Upgrade to a specific agent version | `sudo ./defender_deployment_tool.sh --upgrade --mdatp 101.24082.0004` |
    | Downgrade to a specific agent version | `sudo ./defender_deployment_tool.sh --downgrade --mdatp 101.24082.0004` |
    | Uninstall Defender | `sudo ./defender_deployment_tool.sh --remove` For more information, see [Offboard or uninstall Microsoft Defender for Endpoint on Linux](linux-off-board-endpoints) |
    | Only onboard if Defender is already installed | `sudo ./defender_deployment_tool.sh --only-onboard` |
    | Offboard Defender | `sudo ./defender_deployment_tool.sh --offboard MicrosoftDefenderATPOffboardingLinuxServer.py`*(Note: Before using the --offboard option, you must first download the latest offboarding script from the Defender portal at System &gt; Settings &gt; Endpoints &gt; Offboarding). For other methods of offboarding, see [Offboard or uninstall Microsoft Defender for Endpoint on Linux](linux-off-board-endpoints).* |

## Monitor deployment progress in the Microsoft Defender portal

As the Defender deployment tool runs, it sends a progress event to the Defender portal at the start and end of each deployment step. These events let you track deployment status for all your devices without signing in to each one, and pinpoint the step where a failed deployment stopped.

Check the onboarding status for a device in **Device inventory**. To check fleet-wide onboarding status, use an advanced hunting query. To see the stepwise progress, see the device timeline. Go to **Device inventory**, select the device, and then select **Timeline**.

To filter deployment events on the timeline, enter `DefenderDeployment` in the timeline search box. Each event reads `Defender deployment tool: <step> succeeded` or `Defender deployment tool: <step> failed`, and includes any extra details the tool reports for that step. The following screenshot shows a successful install run.

[![Screenshot of the device timeline filtered to show successful Defender deployment tool events.](media/linux-install-with-defender-deployment-tool/deployment-tool-successful-install-timeline.png)](media/linux-install-with-defender-deployment-tool/deployment-tool-successful-install-timeline.png#lightbox)

### Deployment timeline

A successful install-and-onboard run produces the following sequence of events:

| Order | Step (`ActionName`) | Description |
| --- | --- | --- |
| 1 | Start | The deployment tool starts. The event includes the tool version and the operation: install, upgrade, downgrade, remove, or offboard. |
| 2 | Download | The tool downloads the installer script from Microsoft. This step is skipped if you supply a pre-staged script with the `--script` option. |
| 3 | Prerequisite check | The tool validates the system requirements, such as memory, disk space, glibc, and kernel features. |
| 4 | Installation | The tool installs the Microsoft Defender for Endpoint package. The event includes the installed agent version. |
| 5 | Sensor initialization | The agent finishes onboarding, and the sensor is licensed and active. |
| 6 | Sequence completion | The full deployment sequence finishes. This step is always the last event for a run. |

A remove, upgrade, or offboard run includes only the steps that apply to it. If a step fails, the tool sends a failure event for that step, along with an exit code and an error description that explains what went wrong.

### Query deployment status with advanced hunting

To inspect the events for a specific device, run the following query in [advanced hunting](/en-us/defender-xdr/advanced-hunting-overview). Replace `<DeviceId>` with the target device ID. To find the device ID, go to **Device inventory**, or run `mdatp health --field edr_device_id` on the device.

```kusto
DeviceEvents
| where Timestamp > ago(1d)
| where ActionType == "DefenderDeploymentToolEvent"
| where DeviceId == "<DeviceId>"
| extend Details = parse_json(AdditionalFields)
| project
    Timestamp,
    DeviceName,
    Step = tostring(Details.ActionName),
    Succeeded = tobool(Details.IsSuccess),
    ExitCode = toint(Details.ExitCode),
    Data = tostring(Details.Data),
    ErrorDescription = tostring(Details.ErrorDescription)
| sort by Timestamp asc
```

To get a deployment status summary for all your devices, run the following query. It returns the most recent step that each device reported in the last 30 days, and classifies each device as **Onboarded**, **Onboarding Failed**, or still onboarding:

```kusto
DeviceEvents
| where Timestamp > ago(30d)
| where ActionType == "DefenderDeploymentToolEvent"
| extend Details = parse_json(AdditionalFields)
| extend Step = tostring(Details.ActionName), Succeeded = tobool(Details.IsSuccess)
| summarize arg_max(Timestamp, DeviceName, Step, Succeeded) by DeviceId
| extend Status = case(
    Step == "Sequence completion" and Succeeded, "Onboarded",
    Step == "Sequence completion" and not(Succeeded), "Onboarding Failed",
    not(Succeeded), strcat("Failed at: ", Step),
    "Onboarding")
| project DeviceId, DeviceName, LastEvent = Timestamp, LastStep = Step, Status
```

## Verify AV/EDR functioning

1. In the [Microsoft Defender portal](https://security.microsoft.com/), open the device inventory. It might take 5-20 minutes for the device to show up in the portal.
2. Run an antivirus detection test to verify that the device is properly onboarded and reporting to the service. Perform the following steps on the newly onboarded device:

    1. Ensure that real-time protection is enabled (denoted by a result of true from running the following command):

        ```bash
        mdatp health --field real_time_protection_enabled
        ```

        If it isn't enabled, execute the following command:

        ```bash
        mdatp config real-time-protection --value enabled
        ```
    2. Open a Terminal window and execute the following command to run a detection test:

        ```bash
        curl -o /tmp/eicar.com.txt https://secure.eicar.org/eicar.com.txt
        ```
    3. You can run more detection tests on zip files using either of the following commands:

        ```bash
        curl -o /tmp/eicar_com.zip https://secure.eicar.org/eicar_com.zip
        curl -o /tmp/eicarcom2.zip https://secure.eicar.org/eicarcom2.zip
        ```
    4. The files should be quarantined by Defender for Endpoint on Linux. Use the following command to list all the detected threats:

        ```bash
        mdatp threat list
        ```
3. Run an EDR detection test and simulate a detection to verify that the device is properly onboarded and reporting to the service. Perform the following steps on the newly onboarded device:

    1. Download and extract the [script file](https://aka.ms/MDE-Linux-EDR-DIY) to an onboarded Linux server.
    2. Grant executable permissions to the script:

        ```bash
        chmod +x mde_linux_edr_diy.sh
        ```
    3. Run the following command:

        ```bash
        ./mde_linux_edr_diy.sh
        ```
    4. After a few minutes, a detection should be raised in Microsoft Defender XDR.
    5. Check the alert details, machine timeline, and perform your typical investigation steps.

## Troubleshoot deployment issues

1. Check deployment error logs:

    - `/tmp/defender_deployment_tool.log` records the deployment tool's activity.
    - `/tmp/defender_deployment_tool_telemetry.log` records the progress events that the tool sends to the Microsoft Defender portal.
2. If you're experiencing any connectivity issues, run this command to perform a connectivity test:

    ```bash
    sudo ./defender_deployment_tool.sh --connectivity-test
    ```

    It might take some time to run as it performs checks for every URL needed by Defender and finds issues, if any.
3. Run the advanced hunting query for the device and look for the most recent event where `Succeeded` is `false`. The `Step` field identifies the failed step, and the `ErrorDescription` and `ExitCode` fields explain why:

    - If the deployment fails at the **Download** step, the installer script couldn't be downloaded. Verify that the device has `curl` or `wget` installed and that it allows outbound HTTPS connectivity to Microsoft download endpoints.
    - If the deployment fails at the **Prerequisite check** step, the device doesn't meet the minimum system requirements. The `ErrorDescription` field lists the failed checks, separated by `|`. Non-blocking failures have a `(non_blocking)` prefix and don't stop the deployment.
    - If the deployment fails at the **Installation** step, the package manager couldn't install the agent. Common causes include a misconfigured package repository, a missing dependency, or a requested `mdatp` version that isn't available in the selected channel.
    - If the deployment fails at the **Sensor initialization** step, the agent installed but didn't finish onboarding within the expected time. Run `mdatp health` on the device, and check the `licensed`, `healthy`, and `org_id` fields.
    - If deployment events don't appear in the portal for a device, check `/tmp/defender_deployment_tool_telemetry.log` on that device to confirm whether the tool sent them.
4. If that doesn't help you resolve the issue, try checking the following steps:

    - [Log installation issues](linux-resources#log-installation-issues).
    - [Installation issues](linux-support-install).
    - [Defender for Endpoint agent health issues](health-status).
    - [Troubleshoot performance issues](linux-support-perf).
    - [Troubleshoot cloud connectivity issues](linux-support-connectivity).

## How to switch between channels after you have deployed from a channel

Defender for Endpoint on Linux can be deployed from one of the following channels:

- insiders-fast
- insiders-slow
- prod (production)

Each of these channels corresponds to a Linux software repository. The channel determines the type and frequency of updates that are offered to your device. Devices in insiders-fast are the first to receive updates and new features, followed later by insiders-slow and lastly by prod.

By default, the deployment tool configures your device to use the prod channel. You can use the configuration options described in this document to deploy from a different channel.

To preview new features and provide early feedback, it's recommended that you configure some devices in your enterprise to use either insiders-fast or insiders-slow. If you've already deployed Defender for Endpoint on Linux from a channel and want to switch to a different channel (from prod to insiders-fast, for example), you must first remove the current channel, then delete the current channel repo, and then finally install Defender from the new channel, as illustrated in the following example, where the channel is changed from insiders-fast to prod:

1. Remove the insiders-fast channel version of Defender for Endpoint on Linux..

    ```bash
    sudo ./defender_deployment_tool.sh --remove --channel insiders-fast
    ```
2. Delete the Defender for Endpoint on the Linux insiders-fast repo.

    ```bash
    sudo ./defender_deployment_tool.sh --clean --channel insiders-fast
    ```
3. Install Microsoft Defender for Endpoint on Linux using the production channel.

    ```bash
    sudo ./defender_deployment_tool.sh --channel prod
    ```