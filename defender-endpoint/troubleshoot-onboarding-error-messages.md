---
layout: Conceptual
title: Troubleshoot onboarding issues and error messages - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding-error-messages
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot onboarding issues and error message while completing setup of Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: troubleshooting
ms.subservice: onboard
ms.date: 2024-07-18T00:00:00.0000000Z
locale: en-us
document_id: 3fc4aed2-3d57-a3cf-6aef-22f30fc55ffa
document_version_independent_id: 3fc4aed2-3d57-a3cf-6aef-22f30fc55ffa
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-onboarding-error-messages.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-onboarding-error-messages
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-onboarding-error-messages.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2e4e7374-eb59-b0fe-eda0-39cb00d77e44
---

# Troubleshoot onboarding issues and error messages - Microsoft Defender for Endpoint | Microsoft Learn

This page provides detailed steps to troubleshoot issues that might occur when setting up your Microsoft Defender for Endpoint service.

If you receive an error message, the Defender portal provides a detailed explanation on what the issue is and relevant links are supplied.

## No subscriptions found

If, while you're accessing the Defender portal, you get an error message that says, "No subscriptions found," it means that the Microsoft Entra ID used to sign into the Microsoft Defender portal doesn't have a license for Defender for Endpoint.

Potential reasons:

- The Windows E5 and Office E5 licenses are separate licenses.
- The license was purchased but not provisioned to this Microsoft Entra instance.
    - It could be a license provisioning issue.
    - It could be you inadvertently provisioned the license to a different Microsoft Entra ID than the one used for authentication into the service.

For both cases, you should contact Microsoft support at [General Microsoft Defender for Endpoint Support](https://engagecenter.microsoft.com/) or [Volume Licensing support](/en-us/microsoft-365/commerce/licenses/contact-vl-support).

[![The No subscriptions found page](media/atp-no-subscriptions-found.png)](media/atp-no-subscriptions-found.png#lightbox)

## Your subscription has expired

If while accessing the Defender portal you get a **Your subscription has expired** message, your online service subscription has expired. Microsoft Defender for Endpoint subscription, like any other online service subscription, has an expiration date.

You can choose to renew or extend the license at any point in time. When accessing the portal after the expiration date, a message appears that says, "Your subscription has expired." The message includes an option to download the device offboarding package, just in case you choose to not renew your subscription.

Note

For security reasons, the package used to Offboard devices will expire seven days after the date it was downloaded. Expired offboarding packages sent to a device are rejected. When downloading an offboarding package, you're notified of the package's expiry date and it is also included in the package name.

[![The subscription expired notification message](media/atp-subscription-expired.png)](media/atp-subscription-expired.png#lightbox)

## You are not authorized to access the portal

If you receive a message that says, "You are not authorized to access the portal," it's most likely because you haven't been granted access to the Microsoft Defender portal. Defender for Endpoint is a security monitoring, incident investigation and response product, and as such, access to it's restricted and controlled by your organization's security team. For more information, see, [**Assign user access to the portal**](/en-us/windows/threat-protection/windows-defender-atp/assign-portal-access-windows-defender-advanced-threat-protection).

[![The access disallowed notification message](media/atp-not-authorized-to-access-portal.png)](media/atp-not-authorized-to-access-portal.png#lightbox)

## Data currently isn't available on some sections of the portal

If the portal dashboard and other sections show an error message, such as "Data currently isn't available," you might need to allow subdomains.

[![The data unavailability notification message](media/atp-data-not-available.png)](media/atp-data-not-available.png#lightbox)

You need to allow the `security.windows.com` and all subdomains under it on your web browser. For example, `*.security.windows.com`.

## Portal communication issues

If you encounter issues with accessing the portal, missing data, or restricted access to portions of the portal, you need to verify that the following URLs are accessible through the browser for authorized users:

- `*.blob.core.windows.net`
- `crl.microsoft.com`
- `https://*.microsoftonline-p.com`
- `https://*.security.microsoft.com`
- `https://automatediracs-eus-prd.security.microsoft.com`
- `https://login.microsoftonline.com`
- `https://login.windows.net`
- `https://onboardingpackagescusprd.blob.core.windows.net`
- `https://secure.aadcdn.microsoftonline-p.com`
- `https://security.microsoft.com`
- `https://static2.sharepointonline.com`