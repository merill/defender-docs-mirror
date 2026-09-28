---
layout: Conceptual
title: Troubleshoot device discovery and authenticated network scans in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-device-discovery-network-scans
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to troubleshoot device discovery and authenticated network scans in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1016
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 41a6e792-7b4d-e4ec-757f-829a5aa8b667
document_version_independent_id: 41a6e792-7b4d-e4ec-757f-829a5aa8b667
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-device-discovery-network-scans.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-device-discovery-network-scans
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-device-discovery-network-scans.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: ccc9d9b2-60ce-622f-4964-9345a398207e
---

# Troubleshoot device discovery and authenticated network scans in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

[Device discovery](device-discovery) allows you to improve your visibility into unmanaged devices, assess their security posture, and take appropriate actions to secure them.

[Authenticated network scans](device-discovery#authenticated-network-scans) allow you to scan specific network devices, especially in scenarios where you want to scan a specific subnet.

This article includes troubleshooting information for device discovery and authenticated network scans.

## Security tool raises alert on UnicastScanner.ps1 / PSScript\_{GUID}.ps1 or port scanning activity initiated by the security tool

The active probing scripts are signed by Microsoft and are safe. You can add the following path to your exclusion list:

`C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Downloads\*.ps1`

## Scanner installation failed

Verify that the required URLs are added to the allowed domains in your firewall settings. Also, make sure proxy settings are configured as described in [Configure device proxy and Internet connectivity settings](configure-proxy-internet).

## The Microsoft.com/devicelogin web page didn't show up

Verify that the required URLs are added to the allowed domains in your firewall. Also, make sure proxy settings are configured as described in [Configure device proxy and Internet connectivity settings](configure-proxy-internet).

## Network devices aren't shown in the device inventory after several hours

The scan results should be updated a few hours after the initial scan that took place after completing the network device authenticated scan configuration.

If devices are still not shown, verify that the service `MdatpNetworkScanService` is running on your devices being scanned, on which you installed the scanner, and perform a "Run scan" in the relevant network device authenticated scan configuration.

If you still don't get results after 5 minutes, restart the `MdatpNetworkScanService` service.

## Devices last seen time is longer than 24 hours

Validate that the scanner is running properly. Then go to the scan definition (the saved settings for the scan) and select "Run test." Check what error messages are returning from the relevant IP addresses.

## My scanner is configured but scans aren't running

As the authenticated scanner currently uses an encryption algorithm that isn't compliant with [Federal Information Processing Standards (FIPS)](/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/system-cryptography-use-fips-compliant-algorithms-for-encryption-hashing-and-signing), the scanner can't operate when an organization enforces the use of FIPS compliant algorithms.

To allow algorithms that aren't compliant with FIPS, set the following value in the registry for the devices where the scanner runs:

Computer`\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\FipsAlgorithmPolicy` with a DWORD value named `Enabled` and value of `0x0`.

FIPS compliant algorithms are only used in relation to departments and agencies of the United States federal government.

## Registration error: insufficient permissions to add a new agent

Registration finished with an error: "It looks like you don't have sufficient permissions for adding a new agent. The required permission is 'Manage security settings in Defender'." Press any key to exit.

To resolve this issue, take one of the following actions:

- Ask your system administrator to assign you the required permissions.
- Ask another relevant member to help you with the sign-in process by providing them with the sign-in code and link.

## Registration process fails using provided link in the command line in registration process

Try a different browser or copy the sign-in link and code to a different device.

## Text too small or can't copy text from command line

Change command-line settings on your device to allow copying and change text size.

## Unmanaged device health state is always "Active".

Temporarily, unmanaged device health state is "Active" during the standard retention period of the device inventory, regardless of the devices' actual state.