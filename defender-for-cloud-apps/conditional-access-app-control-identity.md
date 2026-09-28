---
layout: Conceptual
title: Identity-managed devices with Conditional Access app control - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/conditional-access-app-control-identity
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Configure Conditional Access app control access and session policies to detect whether devices are identity-managed, with guidance for Microsoft Entra and non-Entra scenarios.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 352f68b7-9c0c-a713-ceb3-20ede5d78bd7
document_version_independent_id: 352f68b7-9c0c-a713-ceb3-20ede5d78bd7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/conditional-access-app-control-identity.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: conditional-access-app-control-identity
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/conditional-access-app-control-identity.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 6f94798f-3a07-e354-9f10-4d1d200cc24f
---

# Identity-managed devices with Conditional Access app control - Microsoft Defender for Cloud Apps | Microsoft Learn

This article explains how to configure Conditional Access app control access and session policies that use device-management signals. If you have Microsoft Entra, you can use Intune-compliant or Microsoft Entra hybrid joined device conditions. If you don't have Microsoft Entra, you can use client certificates to identify managed devices.

## Check for device management with Microsoft Entra

If you have Microsoft Entra, have your policies check for Microsoft Intune-compliant devices, or Microsoft Entra hybrid joined devices.

Microsoft Entra Conditional Access enables Intune-compliant and Microsoft Entra hybrid joined device information to be passed directly to Defender for Cloud Apps. In Defender for Cloud Apps, create an access or session policy that considers the device state. For more information, see the [What is a device identity?](/en-us/entra/identity/devices/overview)

Note

Some browsers may require additional configuration such as installing an extension. For more information, see [Conditional Access browser support](/en-us/azure/active-directory/conditional-access/concept-conditional-access-conditions).

## Check for device management without Microsoft Entra

If you don't have Microsoft Entra, check for the presence of client certificates in a trusted chain. Use either existing client certificates already deployed in your organization or roll out new client certificates to managed devices.

Make sure that the client certificate is installed in the user store and not the computer store. You then use the presence of those certificates to set access and session policies.

Once the root or intermediate CA certificate is uploaded and a relevant policy is configured, when an applicable session traverses Defender for Cloud Apps and Conditional Access app control, Defender for Cloud Apps requests the browser to present the SSL/TLS client certificates. The browser serves the SSL/TLS client certificates that are installed with a private key. A certificate and its private key are typically packaged by using the PKCS #12 file format, such as .p12 or .pfx.

When a client certificate check is performed, Defender for Cloud Apps checks for the following conditions:

- The selected client certificate is valid and is under the correct root or intermediate CA.
- The certificate isn't revoked (if CRL is enabled).

Note

Most major browsers support performing a client certificate check. However, mobile and desktop apps often leverage built-in browsers that may not support this check and therefore affect authentication for these apps.

### Configure a policy to apply device management via client certificates

To request authentication from relevant devices using client certificates, you need an X.509 root or intermediate certificate authority (CA) SSL/TLS certificate, formatted as a *.PEM* file. Certificates must contain the public key of the CA, which is then used to sign the client certificates presented during a session.

Upload your root or intermediate CA certificates to Defender for Cloud Apps in the **Settings &gt; Cloud Apps &gt; Conditional Access App Control &gt; Device identification** page.

After the root or intermediate CA certificates are uploaded, you can create access and session policies based on **Device tag** and **Valid client certificate**.

**To test client certificate-based device identification**, use our sample root CA and client certificate, as follows:

1. Download the [sample root CA certificate (.pem)](https://github.com/microsoft/Microsoft-Cloud-App-Security/blob/master/Doc%20Assets/Proxy/Samples/SampleRootCA.crt.pem) and [sample client certificate (.pfx)](https://github.com/microsoft/Microsoft-Cloud-App-Security/blob/master/Doc%20Assets/Proxy/Samples/SampleClientCert.pfx).
2. Upload the root CA to Defender for Cloud Apps.
3. Install the client certificate onto the relevant devices. The password is `Microsoft`.