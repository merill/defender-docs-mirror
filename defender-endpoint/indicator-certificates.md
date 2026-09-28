---
layout: Conceptual
title: Create indicators based on certificates - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/indicator-certificates
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: Create indicators based on certificates that define the detection, prevention, and exclusion of entities.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- mde-asr
ms.topic: how-to
ms.subservice: asr
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 4e7649e6-c27d-0094-4ee3-8c72a861da10
document_version_independent_id: 4e7649e6-c27d-0094-4ee3-8c72a861da10
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/indicator-certificates.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: indicator-certificates
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/indicator-certificates.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: ecaba023-9a65-573b-810c-c820a00dfdf2
---

# Create indicators based on certificates - Microsoft Defender for Endpoint | Microsoft Learn

This article shows you how to create certificate-based indicators in Microsoft Defender for Endpoint to allow or block signed applications. Some common use cases include:

- Scenarios when you need to deploy blocking technologies, such as [attack surface reduction rules](attack-surface-reduction-rules-overview) but need to allow behaviors from signed applications by adding the certificate in the allowlist.
- Blocking the use of a specific signed application across your organization. By creating an indicator to block the certificate of the application, Microsoft Defender Antivirus prevents file executions (block and remediate), and automated investigation and remediation behaves the same.

## Before you begin

It's important to understand the following requirements before creating indicators for certificates:

- This feature is available if your organization uses Microsoft Defender Antivirus (in active mode) and cloud-based protection is enabled. For more information, see [Manage cloud-based protection](deploy-manage-report-microsoft-defender-antivirus).
- The anti-malware client version must be `4.18.1901.x` or later.
- Supported on machines on Windows 10, version 1703 or later, Windows Server 2012 R2 and later, or Azure Stack HCI OS, version 23H2 and later.

    Note

    Windows Server 2016 and Windows Server 2012 R2 must be onboarded using the instructions in [Onboard Windows Server 2012 R2 and Windows Server 2016 to Microsoft Defender for Endpoint](onboard-server) for certificate-based indicators to work.
- The virus and threat protection definitions must be up to date.
- This feature supports entering .CER or .PEM file extensions.

Important

- A valid leaf certificate is a signing certificate that has a valid certification path and must be chained to the Root Certificate Authority (CA) trusted by Microsoft. Alternatively, a custom (self-signed) certificate can be used as long as it's trusted by the client (Root CA certificate is installed under the Local Machine 'Trusted Root Certification Authorities').
- The children or parent of the allow/block certificate IOCs aren't included in the allow/block IoC functionality, only leaf certificates are supported.
- Microsoft signed certificates can't be blocked.

Note

In situations where a certificate-based indicator is configured to **Block**, but a file hash indicator for one of its signed files is configured to **Allow**, this configuration is **not supported by design**. Certificate-based indicators have higher precedence in the Microsoft Defender for Endpoint evaluation pipeline and will always override file hash allow indicators. A configuration that simultaneously:

- blocks a certificate, and
- attempts to allow one of its signed files via file hash

is **not supported**. Certificate-based indicators take precedence, and therefore the file will continue to be blocked.

## Create an indicator for certificates from the settings page

Use the following steps to create a certificate indicator from the Settings page.

Important

Creating or removing a certificate indicator of compromise (IoC) can take up to 3 hours.

1. In the navigation pane, select **Settings** &gt; **Endpoints** &gt; **Indicators** (under **Rules**).
2. Select **Add indicator**.
3. Specify the following details:

    - **Indicator**: Specify the entity details and define the expiration of the indicator.
    - **Action**: Specify the action to be taken and provide a description.
    - **Scope**: Define the scope of the machine group.
4. Review the details on the **Summary** tab, and then select **Save**.