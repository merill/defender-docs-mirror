---
layout: Conceptual
title: Verify client connectivity to Microsoft Defender for Endpoint service URLs - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/verify-connectivity
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to verify client connectivity to Defender for Endpoint service URLs
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: mkaminska
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: how-to
ms.subservice: onboard
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: bcf32b08-9cf7-2544-c7ba-898d0b3d7eee
document_version_independent_id: bcf32b08-9cf7-2544-c7ba-898d0b3d7eee
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/verify-connectivity.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verify-connectivity
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/verify-connectivity.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 65bd90ad-9545-2759-0d1f-e2cf94dab0be
---

# Verify client connectivity to Microsoft Defender for Endpoint service URLs - Microsoft Defender for Endpoint | Microsoft Learn

Check that clients are able to connect to the Defender for Endpoint service URLs using the Defender for Endpoint Client Analyzer to ensure that endpoints are able to communicate telemetry to the service.

For more information on the Defender for Endpoint Client Analyzer, see [Troubleshoot sensor health using Microsoft Defender for Endpoint Client Analyzer](overview-client-analyzer).

Note

You can run the Defender for Endpoint Client Analyzer on devices prior to onboarding and after onboarding.

- When testing on a device onboarded to Defender for Endpoint, the tool will use the onboarding parameters.
- When testing on a device not yet onboarded to Defender for Endpoint, the tool will use the defaults of US, UK, and EU. For the consolidated service URLs provided by streamlined connectivity (default for new tenants), when testing devices not yet onboarded to Defender for Endpoint, run `mdeclientanalyzer.cmd` with `-o <path to MDE onboarding package >`. The command will use geo parameters from the onboarding script to test connectivity. Otherwise, the default pre-onboarding test runs against the standard URL set. For more details, see Testing connectivity to the streamlined onboarding method.

Verify that the proxy configuration is completed successfully. The WinHTTP can then discover and communicate through the proxy server in your environment, and then the proxy server allows traffic to the Defender for Endpoint service URLs.

1. Download the [Microsoft Defender for Endpoint Client Analyzer tool](https://aka.ms/mdeanalyzer) on the device where the Defender for Endpoint sensor is running.
2. Extract the contents of MDEClientAnalyzer.zip on the device.
3. Open an elevated command line:

    1. Go to **Start** and type **cmd**.
    2. Right-click **Command prompt** and select **Run as administrator**.
4. Enter the following command and press **Enter**:

    ```command
    HardDrivePath\MDEClientAnalyzer.cmd
    ```

    Replace *HardDrivePath* with the path, where the MDEClientAnalyzer tool was downloaded. For example:

    ```command
    C:\Work\tools\MDEClientAnalyzer\MDEClientAnalyzer.cmd
    ```
5. The tool creates and extracts the *MDEClientAnalyzerResult.zip* file in the folder specified by *HardDrivePath*.
6. Open *MDEClientAnalyzerResult.txt* and verify that you've performed the proxy configuration steps to enable server discovery and access to the service URLs.

    The tool checks the connectivity of Defender for Endpoint service URLs. Ensure the Defender for Endpoint client is configured to interact. The tool prints the results in the *MDEClientAnalyzerResult.txt* file for each URL that can potentially be used to communicate with the Defender for Endpoint services. For example:

    ```text
    Testing URL : https://xxx.microsoft.com/xxx
    1 - Default proxy: Succeeded (200)
    2 - Proxy auto discovery (WPAD): Succeeded (200)
    3 - Proxy disabled: Succeeded (200)
    4 - Named proxy: Doesn't exist
    5 - Command line proxy: Doesn't exist
    ```

If any one of the connectivity options returns a (200) status, then the Defender for Endpoint client can communicate with the tested URL properly using this connectivity method.

However, if the connectivity check results indicate a failure, an HTTP error is displayed (see [HTTP Status Codes](/en-us/troubleshoot/developer/webapps/iis/www-administration-management/http-status-code)). You can then use the URLs listed in [Enable access to Defender for Endpoint service URLs in the proxy server](configure-environment#enable-access-to-microsoft-defender-for-endpoint-service-urls-in-the-proxy-server), which provides the required service URLs to allow through your proxy server. The URLs available for use depend on the region selected in the Defender for Endpoint onboarding package or onboarding script used for the device.

Note

- Cloud connectivity checks in the Connectivity Analyzer tool are incompatible with the attack surface reduction (ASR) rule [Block process creations originating from PSExec and WMI commands](attack-surface-reduction-rules-reference#block-process-creations-originating-from-psexec-and-wmi-commands). To run the connectivity tool, you need to do one of the following steps:
    - Temporarily disable the **Block process creations originating from PSExec and WMI commands** rule.
    - Temporarily add a global or per-rule ASR exclusion for the analyzer. For more information, see [File and folder exclusions for ASR rules](attack-surface-reduction-rules-overview#file-and-folder-exclusions-for-asr-rules).
- When the TelemetryProxyServer is set in the registry or via Group Policy, Defender for Endpoint falls back to direct connectivity if Defender for Endpoint fails to access the defined proxy.

## Testing connectivity to the streamlined onboarding method

If you're testing connectivity on a device that hasn't yet been onboarded to Defender for Endpoint using streamlined device connectivity (relevant for both new and migrating devices):

1. Download the streamlined onboarding package for relevant OS.
2. Extract the .cmd from onboarding package.
3. Download the [Microsoft Defender for Endpoint Client Analyzer tool](https://aka.ms/mdeanalyzer) and extract the contents of MDEClientAnalyzer.zip on the device.
4. Run `mdeclientanalyzer.cmd -o <path to onboarding cmd file>` from within the MDEClientAnalyzer folder. The command uses geo parameters from the onboarding script to test connectivity.

If you're testing connectivity on a device onboarded to Defender for Endpoint using the streamlined onboarding package, run the Defender for Endpoint Client Analyzer as normal. The tool uses the configured onboarding parameters to test connectivity.

For more info on how to access the streamlined onboarding package and connectivity script, see [Onboarding devices using streamlined device connectivity](configure-device-connectivity).

## Microsoft Monitoring Agent (MMA) Service URL connections

See the following guidance to eliminate the wildcard (\*) requirement for your specific environment when using the Microsoft Monitoring Agent (MMA) for previous versions of Windows.

1. Onboard a previous operating system with the Microsoft Monitoring Agent (MMA) into Defender for Endpoint. For more information, see [Onboard Windows Server 2016 and Windows Server 2012 R2](onboard-server#onboard-windows-server-2016-and-windows-server-2012-r2).
2. Ensure the machine is successfully reporting into the Microsoft Defender portal.
3. Run the TestCloudConnection.exe tool from `C:\Program Files\Microsoft Monitoring Agent\Agent` to validate the connectivity, and to get the required URLs for your specific workspace.
4. Check the Microsoft Defender for Endpoint URLs list for the complete list of requirements for your region (refer to the [Microsoft Defender for Endpoint service URLs spreadsheet](https://go.microsoft.com/fwlink/?linkid=2247417)).

![This is admin PowerShell.](/en-us/defender/media/defender-endpoint/admin-powershell.png)

The wildcards (\*) used in `*.ods.opinsights.azure.com`, `*.oms.opinsights.azure.com`, and `*.agentsvc.azure-automation.net` URL endpoints can be replaced with your specific Workspace ID. The Workspace ID is specific to your environment and workspace. It can be found in the Onboarding section of your tenant within the Microsoft Defender portal.

The `*.blob.core.windows.net` URL endpoint can be replaced with the URLs shown in the "Firewall Rule: \*.blob.core.windows.net" section of the test results.

Note

In the case of onboarding via Microsoft Defender for Cloud, multiple workspaces can be used. You will need to perform the TestCloudConnection.exe procedure on the onboarded machine from each workspace (to determine, if there are any changes to the \*.blob.core.windows.net URLs between the workspaces).