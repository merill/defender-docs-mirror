---
layout: Conceptual
title: Behavior Monitoring in Microsoft Defender Antivirus on macOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/behavior-monitor-macos
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Behavior Monitoring in Microsoft Defender Antivirus on macOS
author: chrisda
ms.author: chrisda
ms.service: defender-endpoint
ms.topic: overview
ms.date: 2026-09-17T00:00:00.0000000Z
ms.subservice: ngp
ms.collection:
- m365-security
- tier2
- mde-asr
ms.custom:
- partner-contribution
- msecd-doc-authoring-1015
ms.reviewer: yongrhee
ai-usage: ai-assisted
locale: en-us
document_id: 9e35397f-cbc4-aefc-8a89-5d843e9c28bf
document_version_independent_id: 9e35397f-cbc4-aefc-8a89-5d843e9c28bf
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/behavior-monitor-macos.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: behavior-monitor-macos
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/behavior-monitor-macos.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 416d3885-371b-bb74-2a6a-82b51e521349
---

# Behavior Monitoring in Microsoft Defender Antivirus on macOS - Microsoft Defender for Endpoint | Microsoft Learn

Behavior monitoring monitors process behavior to detect and analyze potential threats based on the behavior of the applications, daemons, and files within the system. As behavior monitoring observes how the software behaves in real-time, it can adapt quickly to new and evolving threats and block them.

Check whether behavior monitoring is enabled on a device by running the following command in Terminal:

```bash
mdatp health --details features
```

If the command reports that `behavior_monitoring` is disabled, enable the feature by using one of the methods in this article.

## Prerequisites

- The device must be [onboarded to Microsoft Defender for Endpoint](microsoft-defender-endpoint-mac).
- For the best experience, Microsoft Defender should be up-to-date with the latest version.
- The Defender for Endpoint `app_version` (also known as **Platform update**) must be `101.25032.0006` (April 2025) or later.
- [Real-time protection](mac-preferences#enforcement-level-for-antivirus-engine) (RTP) must be enabled.
- [Cloud-delivered protection](mac-preferences) must be enabled.

## Intune deployment

> 
> Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

1. Copy the following property list XML to create an Apple configuration profile, and save the profile as `BehaviorMonitoring_for_MDE_on_macOS.mobileconfig`.

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    <plist version="1.0">
        <dict>
            <key>PayloadUUID</key>
            <string>C4E6A782-0C8D-44AB-A025-EB893987A295</string>
            <key>PayloadType</key>
            <string>Configuration</string>
            <key>PayloadOrganization</key>
            <string>Microsoft</string>
            <key>PayloadIdentifier</key>
            <string>C4E6A782-0C8D-44AB-A025-EB893987A295</string>
            <key>PayloadDisplayName</key>
            <string>Microsoft Defender for Endpoint settings</string>
            <key>PayloadDescription</key>
            <string>Microsoft Defender for Endpoint configuration settings</string>
            <key>PayloadVersion</key>
            <integer>1</integer>
            <key>PayloadEnabled</key>
            <true/>
            <key>PayloadRemovalDisallowed</key>
            <true/>
            <key>PayloadScope</key>
            <string>System</string>
            <key>PayloadContent</key>
            <array>
                <dict>
                    <key>PayloadUUID</key>
                    <string>99DBC2BC-3B3A-46A2-A413-C8F9BB9A7295</string>
                    <key>PayloadType</key>
                    <string>com.microsoft.wdav</string>
                    <key>PayloadOrganization</key>
                    <string>Microsoft</string>
                    <key>PayloadIdentifier</key>
                    <string>99DBC2BC-3B3A-46A2-A413-C8F9BB9A7295</string>
                    <key>PayloadDisplayName</key>
                    <string>Microsoft Defender for Endpoint configuration settings</string>
                    <key>PayloadDescription</key>
                    <string/>
                    <key>PayloadVersion</key>
                    <integer>1</integer>
                    <key>PayloadEnabled</key>
                    <true/>
                    <key>antivirusEngine</key>
                    <dict>
                    <key>behaviorMonitoring</key>
                    <string>enabled</string>
                    </dict>
                    <key>features</key>
                    <dict>
                    <key>behaviorMonitoring</key>
                    <string>enabled</string>
                    </dict>
                </dict>
            </array>
        </dict>
    </plist>
    ```
2. Create a custom macOS configuration profile in Intune. For detailed instructions, see [Add custom settings to Apple devices in Microsoft Intune](/en-us/intune/device-configuration/templates/configure-custom-settings-apple) (link opens in a new tab).

    When you create the policy on the **Policies** tab of the **Devices | Configuration** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/configuration](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesMenu/%7E/configuration), by selecting ![](media/defender-portal-icon-create.png)**Create** &gt; ![](media/defender-portal-icon-create.png)**New policy**, use these specific settings:

    - **Platform**: Select **macOS**.
    - **Profile type**: Select **Templates**.
    - **Template name**: Select **Custom**.

    In the **Custom** wizard, use these settings on the **Configuration settings** tab:

    - **Custom configuration profile name**: Enter a descriptive name, such as `Microsoft Defender behavior monitoring`.
    - **Deployment channel**: Select **Device channel**.
    - **Configuration profile file**: Browse to and select the `BehaviorMonitoring_for_MDE_on_macOS.mobileconfig` file.

## Jamf Pro deployment

> 
> Jamf Pro is a separate third-party product that isn't part of Defender for Endpoint and isn't included with Defender for Endpoint subscriptions. To use Jamf Pro, your organization needs a separate Jamf Pro subscription. For product and subscription information, see [Jamf Pro](https://www.jamf.com/products/jamf-pro/). If your organization doesn't use Jamf Pro, use another configuration method in this article, if available.

1. Copy the following XML to create a *.plist* file, and save it as `BehaviorMonitoring_for_MDE_on_macOS.plist`:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    <plist version="1.0">
        <dict>
            <key>antivirusEngine</key>
                <dict>
                    <key>behaviorMonitoring</key>
                    <string>enabled</string>
                </dict>
            <key>features</key>
                <dict>
                    <key>behaviorMonitoring</key>
                    <string>enabled</string>
                </dict>
        </dict>
    </plist>
    ```
2. Follow the Jamf instructions to [deploy a custom computer configuration profile](https://learn.jamf.com/r/technical-articles/Deploying_Custom_Computer_Configuration_Profiles_Using_the_Application_and_Custom_Settings_Payload). Use these Defender-specific values:

    - **Preference Domain**: Enter `com.microsoft.wdav`.
    - **Property list**: Upload the `BehaviorMonitoring_for_MDE_on_macOS.plist` file.

For more information, see: [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences).

## Manual deployment

Use the following syntax in Terminal to enable or disable behavior monitoring:

```bash
sudo mdatp config behavior-monitoring --value <enabled|disabled>
```

For example, run the following command to enable behavior monitoring:

```bash
sudo mdatp config behavior-monitoring --value enabled
```

For more information, see: [Resources for Microsoft Defender for Endpoint on macOS](mac-resources).

## Verifying behavior monitoring is enabled

To verify behavior monitoring is enabled, run the following command in Terminal:

```bash
mdatp health --field behavior_monitoring
```

When behavior monitoring is enabled, the command returns `enabled`.

## To test behavior monitoring (prevention/block) detection

See [Behavior Monitoring demonstration](demonstration-behavior-monitoring).

## Verifying behavior monitoring detections

The existing Microsoft Defender for Endpoint on macOS command line interface can be used to review behavior monitoring details and artifacts.

```bash
sudo mdatp threat list
```

## Frequently asked questions (FAQ)

### What if I see an increase in CPU utilization or memory utilization?

Disable behavior monitoring and see if the issue goes away. If the issue doesn't go away, it isn't related to behavior monitoring.

If the issue goes away, re-enable behavior monitoring and use behavior monitoring statistics to identify and exclude processes generating excessive events:

```bash
sudo mdatp config behavior-monitoring-statistics --value enabled
```

Repro the issue and then execute:

```bash
sudo mdatp diagnostic behavior-monitoring-statistics --sort
```

This command lists processes running on the machine which are reporting behavior monitoring events to the engine process. The more events, the more CPU/memory impact that process has.

Exclude identified processes using the following syntax:

```bash
sudo mdatp exclusion process add --path <path to process with lots of events>
```

Important

Verify the reliability of the processes being excluded. Excluding these processes prevent all events from being sent to behavior monitoring and from undergoing content scanning. However, endpoint detection an response (EDR) continues to receive events from these processes.

Disabling behavior monitoring is unlikely to reduce CPU usage by the `wdavdaemon` or `wdavdaemon_enterprise` processes, but might affect the `wdavdaemon_unprivileged` process. If `wdavdaemon` or `wdavdaemon_enterprise` are also experiencing high CPU usage, behavior monitoring might not be the sole cause, and contacting Microsoft support is recommended.

Once done, disable behavior monitoring statistics:

```bash
sudo mdatp config behavior-monitoring-statistics --value disabled
```

If the issue persists, especially after a reboot, download the [XMDE Client Analyzer](https://aka.ms/XMDEClientAnalyzer), and then contact Microsoft support.

## Network real-time inspection for macOS

Important

Some information relates to a prerelease product that might be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

The network real-time inspection (NRI) for macOS feature enhances real-time protection (RTP) by using [behavior monitoring](behavior-monitor-macos) in concert with file, process, and other events to detect suspicious activity. Behavior monitoring triggers both telemetry and sample submissions on suspicious files for Microsoft to analyze from the cloud protection backend, and is delivered to the client device, resulting in a removal of the threat.

### Is there an impact on performance?

NRI should have a low impact on network performance. Instead of holding the connection and blocking, NRI makes a copy of the packet as it crosses the network, and NRI performs an asynchronous inspection.

Note

When network real-time inspection (NRI) for macOS is enabled, you might see a slight increase in memory utilization.

### Requirements for NRI for macOS

- The device must be [onboarded to Microsoft Defender for Endpoint](microsoft-defender-endpoint-mac).
- Preview features must be turned on in the [Microsoft Defender portal](https://security.microsoft.com).
- The device must be in the Beta channel (formerly `InsiderFast`).
- The Defender for Endpoint `app_version` (also known as **Platform update**) must be `101.24092.0004` (October 2024) or later.
- [Real-time protection](mac-preferences#enforcement-level-for-antivirus-engine) must be enabled.
- Behavior monitoring must be enabled.
- [Cloud-delivered protection](mac-preferences) must be enabled.
- The device must be explicitly enrolled into the preview.

### Deployment instructions for NRI for macOS

1. E-mail us at `NRIonMacOS@microsoft.com` with information about your Microsoft Defender for Endpoint OrgID where you would like to have network real-time inspection (NRI) for macOS enabled.

    Important

    In order to evaluate NRI for macOS, send email to `NRIonMacOS@microsoft.com`. Include your Defender for Endpoint Org ID. We're enabling this feature on a per-request basis for each tenant.
2. Enable behavior monitoring if it's not already enabled:

    ```Bash
    sudo mdatp config behavior-monitoring --value enabled
    ```
3. Enable network protection in block mode:

    ```Bash
    sudo mdatp config network-protection enforcement-level --value block
    ```
4. Enable network real-time inspection (NRI):

    ```Bash
    sudo mdatp network-protection remote-settings-override set --value "{\"enableNriMpengineMetadata\" : true}"
    ```

    Note

    While this feature is in preview, and because the setting is set by using command line, network real-time inspection (NRI) doesn't persist following reboots. You must re-enable it.