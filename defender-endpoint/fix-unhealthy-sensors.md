---
layout: Conceptual
title: Fix unhealthy sensors in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/fix-unhealthy-sensors
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Fix device sensors that are reporting as misconfigured or inactive so that the service receives data from the device.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- ngp
ms.topic: article
ms.date: 2025-03-25T00:00:00.0000000Z
ms.subservice: onboard
locale: en-us
document_id: 42d41a22-67e8-0504-54ef-530729eb8bc7
document_version_independent_id: 42d41a22-67e8-0504-54ef-530729eb8bc7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/fix-unhealthy-sensors.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fix-unhealthy-sensors
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/fix-unhealthy-sensors.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 14315dfd-828e-31f3-65bb-77b3bebcbeba
---

# Fix unhealthy sensors in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Devices can be categorized as misconfigured or inactive are flagged for different reasons. This article provides information about why a device might be categorized as inactive or misconfigured.

## Inactive devices

An inactive device isn't necessarily flagged because of an issue. The following actions taken on a device can cause a device to be categorized as inactive:

- Device isn't in use
- Device was reinstalled or renamed
- Device was off-boarded
- Device isn't sending signals

### Device isn't in use

Any device that isn't in use for more than seven days retains 'Inactive' status in the portal.

### Device was reinstalled or renamed

A new device entity is generated in the Defender portal for reinstalled or renamed devices. The previous device entity remains, with an 'Inactive' status in the portal. If you reinstalled a device and deployed the Defender for Endpoint package, search for the new device name to verify that the device is reporting normally.

### Device was off-boarded

If the device was off-boarded, it still appears in devices list. After seven days, the device health state should change to inactive.

### Device isn't sending signals

If the device isn't sending any signals to any Microsoft Defender for Endpoint channels for more than seven days for any reason, a device can be considered inactive. Misconfigured devices can also be considered inactive.

## Misconfigured devices

Misconfigured devices can further be classified to:

- Impaired communications
- No sensor data

### Impaired communications

This status indicates that there's limited communication between the device and the service.

The following suggested actions can help fix issues related to a misconfigured device with impaired communications:

- [Ensure the device has Internet connection](troubleshoot-onboarding#troubleshoot-onboarding-issues-on-the-device). The Microsoft Defender for Endpoint sensor requires Microsoft Windows HTTP (WinHTTP) to report sensor data and communicate with the Microsoft Defender for Endpoint service.
- [Verify client connectivity to Microsoft Defender for Endpoint service URLs](verify-connectivity). Verify the proxy configuration completed successfully, that WinHTTP can discover and communicate through the proxy server in your environment, and that the proxy server allows traffic to the Microsoft Defender for Endpoint service URLs.

If you took corrective actions and the device status is still misconfigured, [open a support ticket](https://go.microsoft.com/fwlink/?LinkID=761093&amp;clcid=0x409).

### No sensor data

A misconfigured device with status 'No sensor data' has communication with the service but can only report partial sensor data.

Follow theses actions to correct known issues related to a misconfigured device with status 'No sensor data':

- [Ensure the device has Internet connection](troubleshoot-onboarding#troubleshoot-onboarding-issues-on-the-device). The Microsoft Defender for Endpoint sensor requires Microsoft Windows HTTP (WinHTTP) to report sensor data and communicate with the Microsoft Defender for Endpoint service.
- [Verify client connectivity to Microsoft Defender for Endpoint service URLs](verify-connectivity). Verify the proxy configuration completed successfully, that WinHTTP can discover and communicate through the proxy server in your environment, and that the proxy server allows traffic to the Microsoft Defender for Endpoint service URLs.
- [Ensure the diagnostic data service is enabled](troubleshoot-onboarding#ensure-the-diagnostics-service-is-enabled). If the devices aren't reporting correctly, you should verify that the Windows diagnostic data service is set to automatically start. Also verify that the Windows diagnostic data service is running on the endpoint.
- [Ensure that Microsoft Defender Antivirus isn't disabled by policy](troubleshoot-onboarding#ensure-that-microsoft-defender-antivirus-is-not-disabled-by-a-policy). If your devices are running a third-party anti-malware client, Defender for Endpoint agent requires that the Microsoft Defender Antivirus Early Launch anti-malware (ELAM) driver is enabled.
- For macOS devices that sleep for more than approximately 48 hours (a weekend), Microsoft Defender for Endpoint on macOS still sends Command and Control (CnC) channel data, but doesn't send any Cyber channel data. After the devices are turned on and used on the first business day, the devices will show up as active.

If you took corrective actions and the device status is still misconfigured, [open a support ticket](https://go.microsoft.com/fwlink/?LinkID=761093&amp;clcid=0x409).