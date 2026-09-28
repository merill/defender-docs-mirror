---
layout: Conceptual
title: Cloud protection and sample submission at Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/cloud-protection-microsoft-antivirus-sample-submission
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about cloud-delivered protection and Microsoft Defender Antivirus
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.reviewer: mkaminska, yongrhee
ms.subservice: ngp
ms.topic: concept-article
ms.date: 2025-10-20T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
- mde-ngp
locale: en-us
document_id: 6ba41ed7-0ded-4236-72ec-aa8038b2f322
document_version_independent_id: 6ba41ed7-0ded-4236-72ec-aa8038b2f322
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/cloud-protection-microsoft-antivirus-sample-submission.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: cloud-protection-microsoft-antivirus-sample-submission
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/cloud-protection-microsoft-antivirus-sample-submission.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 61a00676-fba0-a72e-258a-9298aa79b3de
---

# Cloud protection and sample submission at Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender Antivirus uses many intelligent mechanisms for detecting malware. One of the most powerful capabilities is the ability to apply the power of the cloud to detect malware and perform rapid analysis. Cloud protection and automatic sample submission work together with Microsoft Defender Antivirus to help protect against new and emerging threats.

If a suspicious or malicious file is detected, a sample is sent to the cloud service for analysis while Microsoft Defender Antivirus blocks the file. As soon as a determination is made, which happens quickly, the file is either released or blocked by Microsoft Defender Antivirus.

This article provides an overview of cloud protection and automatic sample submission at Microsoft Defender Antivirus. To learn more about cloud protection, see [Cloud protection and Microsoft Defender Antivirus](cloud-protection-microsoft-defender-antivirus).

## Prerequisites

### Supported operating systems

- Windows
- macOS
- Linux
- Windows Server

## How cloud protection and sample submission work together

To understand how cloud protection works together with sample submission, it can be helpful to understand how Defender for Endpoint protects against threats. The Microsoft Intelligent Security Graph monitors threat data from a vast network of sensors. Microsoft layers cloud-based machine-learning models that can assess files based on signals from the client and the vast network of sensors and data in the Intelligent Security Graph. This approach gives Defender for Endpoint the ability to block many never-before-seen threats.

The following image depicts the flow of cloud protection and sample submission with Microsoft Defender Antivirus:

[![Cloud-delivered protection flow](media/cloud-protection-flow.png)](media/cloud-protection-flow.png#lightbox)

Microsoft Defender Antivirus and cloud protection automatically block most new, never-before-seen threats at first sight by using the following methods:

1. Lightweight client-based machine-learning models, blocking new and unknown malware.
2. Local behavioral analysis, stopping file-based and file-less attacks.
3. High-precision antivirus, detecting common malware through generic and heuristic techniques.
4. Advanced cloud-based protection is provided for cases when Microsoft Defender Antivirus running on the endpoint needs more intelligence to verify the intent of a suspicious file.

    1. In the event Microsoft Defender Antivirus can't make a clear determination, file metadata is sent to the cloud protection service. Often within milliseconds, the cloud protection service can determine based on the metadata as to whether the file is malicious or not a threat.

        - The cloud query of file metadata can be a result of behavior, mark of the web, or other characteristics where a clear verdict isn't determined.
        - A small metadata payload is sent, with the goal of reaching a verdict of malware or not a threat. The metadata doesn't include personal data, such as personally identifiable information (PII). Information such as filenames, are hashed.
        - Can be synchronous or asynchronous. For synchronous, the file doesn't open until the cloud renders a verdict. For asynchronous, the file opens while cloud protection performs its analysis.
        - Metadata can include PE attributes, static file attributes, dynamic and contextual attributes, and more (see Examples of metadata sent to the cloud protection service).
    2. After examining the metadata, if Microsoft Defender Antivirus cloud protection can't reach a conclusive verdict, it can request a sample of the file for further inspection. This request honors the setting configuration for sample submission, as described in the following table:

        | Setting | Description |
        | --- | --- |
        | **Send safe samples automatically** | - Safe samples are samples considered to not commonly contain PII data. Examples include `.bat`, `.scr`, `.dll`, and `.exe`. - If file is likely to contain PII, the user gets a request to allow file sample submission.- This option is the default configuration on Windows, macOS, and Linux. |
        | **Always Prompt** | - If configured, the user is always prompted for consent before file submission- This setting isn't available in macOS and Linux cloud protection |
        | **Send all samples automatically** | - If configured, all samples are sent automatically- If you would like sample submission to include macros embedded in Word docs, you must choose **Send all samples automatically**- "Send all samples automatically" is the equivalent to the "Enable" setting in macOS policy |
        | **Do not send** | - Prevents "block at first sight" based on file sample analysis- "Don't send" is the equivalent to the "Disabled" setting in macOS policy and "None" setting in Linux policy.- Metadata is sent for detections even when sample submission is disabled |
    3. After files are submitted to cloud protection, the submitted files can be **scanned**, **detonated**, and processed through **big data analysis** **machine-learning** models to reach a verdict. Turning off cloud-delivered protection limits analysis to only what the client can provide through local machine-learning models, and similar functions.

Important

[Block at first sight (BAFS)](configure-block-at-first-sight-microsoft-defender-antivirus) provides detonation and analysis to determine whether a file or process is safe. BAFS can delay the opening of a file momentarily until a verdict is reached. If you disable sample submission, BAFS is also disabled, and file analysis is limited to metadata only. We recommend keeping sample submission and BAFS enabled. To learn more, see [What is "block at first sight"?](configure-block-at-first-sight-microsoft-defender-antivirus)

## Cloud protection levels

Cloud protection is enabled by default at Microsoft Defender Antivirus. We recommend that you keep cloud protection enabled, although you can configure the protection level for your organization. See [Specify the cloud-delivered protection level for Microsoft Defender Antivirus](cloud-protection-configure#specify-the-cloud-protection-level).

## Sample submission settings

In addition to configuring your cloud protection level, you can configure your sample submission settings. You can choose from several options:

- **Send safe samples automatically** (the default behavior)
- **Send all samples automatically**
- **Do not send samples**

Tip

Using the `Send all samples automatically` option provides for better security, because phishing attacks are used for a high amount of [initial access attacks](https://attack.mitre.org/tactics/TA0001/). For information about configuration options using Intune, Configuration Manager, Group Policy, or PowerShell, see [Configure cloud protection in Microsoft Defender Antivirus](cloud-protection-configure).

## Examples of metadata sent to the cloud protection service

[![The examples of metadata sent to cloud protection in the Microsoft Defender Antivirus portal](media/cloud-protection-metadata-sample.png)](media/cloud-protection-metadata-sample.png#lightbox)

The following table lists examples of metadata sent for analysis by cloud protection:

| Type | Attribute |
| --- | --- |
| Machine attributes | `OS version``Processor``Security settings` |
| Dynamic and contextual attributes | **Process and installation**`ProcessName``ParentProcess``TriggeringSignature``TriggeringFile``Download IP and url``HashedFullPath``Vpath``RealPath``Parent/child relationships`**Behavioral**`Connection IPs``System changes``API calls``Process injection`**Locale**`Locale setting``Geographical location` |
| Static file attributes | **Partial and full hashes**`ClusterHash``Crc16``Ctph``ExtendedKcrcs``ImpHash``Kcrc3n``Lshash``LsHashs``PartialCrc1``PartialCrc2``PartialCrc3``Sha1``Sha256`**File properties**`FileName``FileSize`**Signer information**`AuthentiCodeHash``Issuer``IssuerHash``Publisher``Signer``SignerHash` |

## Samples are treated as customer data

If you're wondering what happens with sample submissions, Defender for Endpoint treats all file samples as customer data. Microsoft honors both the geographical and data retention choices your organization selected when onboarding to Defender for Endpoint.

In addition, Defender for Endpoint received multiple compliance certifications, demonstrating continued adherence to a sophisticated set of compliance controls:

- ISO 27001
- ISO 27018
- SOC I, II, III
- PCI

For more information, see the following resources:

- [Azure Compliance Offerings](/en-us/azure/storage/common/storage-compliance-offerings)
- [Service Trust Portal](https://servicetrust.microsoft.com)
- [Microsoft Defender for Endpoint data storage and privacy](data-storage-privacy)

## Other file sample submission scenarios

There are two more scenarios where Defender for Endpoint might request a file sample that isn't related to the cloud protection at Microsoft Defender Antivirus. These scenarios are described in the following table:

| Scenario | Description |
| --- | --- |
| Manual file sample collection in the Microsoft Defender portal | When onboarding devices to Defender for Endpoint, you can configure settings for [endpoint detection and response (EDR)](overview-endpoint-detection-response). For example, there's a setting to enable sample collections from the device, which can easily be confused with the sample submission settings described in this article. The EDR setting controls file sample collection from devices when requested through the Microsoft Defender portal, and is subject to the roles and permissions already established. This setting can allow or block file collection from the endpoint for features such as deep analysis in the Microsoft Defender portal. If this setting isn't configured, the default is to enable sample collection. Learn about Defender for Endpoint configuration settings, see [Onboard Windows and Mac client devices to Microsoft Defender for Endpoint](onboard-client) |
| Automated investigation and response content analysis | When [automated investigations](automated-investigations) are running on devices (when configured to run automatically in response to an alert or manually run), files that are identified as suspicious can be collected from the endpoints for further inspection. If necessary, the file content analysis feature for automated investigations can be disabled in the Microsoft Defender portal.  The file extension names can also be modified to add or remove extensions for other file types that are automatically submitted during an automated investigation.  To learn more, see [Manage automation file uploads](manage-automation-file-uploads). |