---
layout: Conceptual
title: Troubleshoot Microsoft Defender for Endpoint service issues - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-mdatp
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Find solutions and workarounds to known issues such as server errors when trying to access the service.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: troubleshooting
ms.date: 2025-02-24T00:00:00.0000000Z
locale: en-us
document_id: 0899f55a-63bc-5a45-ffd5-1cb4de9a125c
document_version_independent_id: 0899f55a-63bc-5a45-ffd5-1cb4de9a125c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-mdatp.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-mdatp
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-mdatp.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: cb0e21f9-1b05-f76b-875f-fc853d0e50a2
---

# Troubleshoot Microsoft Defender for Endpoint service issues - Microsoft Defender for Endpoint | Microsoft Learn

This section addresses issues that might arise as you use the Microsoft Defender for Endpoint service.

## Server error - Access is denied due to invalid credentials

If you encounter a server error when trying to access the service, you need to change your browser cookie settings. Configure your browser to allow cookies.

## Elements or data missing on the portal

If some elements or data is missing in the Defender portal, it's possible that proxy settings are blocking it.

Make sure that `*.security.microsoft.com` is included in the proxy allow list.

Note

You must use the HTTPS protocol when adding the following endpoints.

## Microsoft Defender for Endpoint service shows event or error logs in the Event Viewer

See [Review events and errors using Event Viewer](event-error-codes) for a list of event IDs that are reported by the Microsoft Defender for Endpoint service. The article also contains troubleshooting steps for event errors.

## Microsoft Defender for Endpoint service fails to start after a reboot and shows error 577

If onboarding devices successfully completes, but Microsoft Defender for Endpoint doesn't start after a reboot and shows error 577, check that Windows Defender isn't disabled by a policy.

For more information, see [Ensure that Microsoft Defender Antivirus isn't disabled by policy](troubleshoot-onboarding#ensure-that-microsoft-defender-antivirus-is-not-disabled-by-a-policy).

## Known issues with regional formats

### Date and time formats

There are some known issues with the time and date formats.

The following date formats are supported:

- MM/dd/yyyy
- dd/MM/yyyy

The following date and time formats are currently not supported:

- Date format yyyy/MM/dd
- Date format dd/MM/yy
- Date format with yy. Only shows yyyy.
- Time format HH:mm:ss isn't supported (the 12 hour AM/PM format isn't supported). Only the 24-hour format is supported.

### Use of comma to indicate thousand

Support of use of comma as a separator in numbers aren't supported. Regions where a number is separated with a comma to indicate a thousand, will only see the use of a dot as a separator. For example, 15,5 K is displayed as 15.5 K.

## Microsoft Defender for Endpoint tenant was automatically created in Europe

When you use Microsoft Defender for Cloud to monitor servers, a Microsoft Defender for Endpoint tenant is automatically created. The Microsoft Defender for Endpoint data is stored in Europe by default.