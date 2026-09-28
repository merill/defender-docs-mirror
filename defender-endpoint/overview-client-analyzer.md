---
layout: Conceptual
title: Troubleshoot sensor health using Microsoft Defender for Endpoint Client Analyzer - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/overview-client-analyzer
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot sensor health on devices to identify potential configuration, environment, connectivity, or telemetry issue affecting sensor data or capability.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.reviewer: yongrhee
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-ngp
ms.topic: troubleshooting-general
ms.subservice: ngp
ms.date: 2025-06-10T00:00:00.0000000Z
locale: en-us
document_id: 575125c6-116e-f2bf-e9e5-70000081238d
document_version_independent_id: 575125c6-116e-f2bf-e9e5-70000081238d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/overview-client-analyzer.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: overview-client-analyzer
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/overview-client-analyzer.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 3d4aa843-ee8a-31e1-db48-05bdfedfec79
---

# Troubleshoot sensor health using Microsoft Defender for Endpoint Client Analyzer - Microsoft Defender for Endpoint | Microsoft Learn

The [Microsoft Defender for Endpoint Client Analyzer](https://aka.ms/MDEClientAnalyzer) (MDECA) can be useful when diagnosing sensor health or reliability issues on [onboarded devices](onboard-configure) running either Windows, Linux, or macOS. For example, you might want to run the analyzer on a machine that appears to be unhealthy according to the displayed [sensor health status](fix-unhealthy-sensors) (Inactive, No Sensor Data or Impaired Communications) in the security portal.

Besides obvious sensor health issues, MDECA can collect other traces, logs, and diagnostic information for troubleshooting complex scenarios such as:

- Application compatibility (AppCompat), performance, network connectivity, or
- Unexpected behavior related to [Endpoint Data Loss Prevention](/en-us/purview/endpoint-dlp-learn-about).

## Use the client analyzer on devices running Windows, Linux, or macOS

- [Run the client analyzer on Windows](run-analyzer-windows)
- [Run the client analyzer on Linux](run-analyzer-linux)
- [Run the client analyzer on macOS](run-analyzer-macos)

Tip

Watch this video to get an overview of the client analyzer: [Defender for Endpoint client analyzer overview](https://www.youtube.com/watch?v=GnqDsvYYL6w)

## Privacy notice

- The Microsoft Defender for Endpoint Client Analyzer tool is regularly used by Microsoft Customer Support Services (CSS) to collect information that will help troubleshoot issues you might be experiencing with Microsoft Defender for Endpoint.
- The collected data might contain Personally Identifiable Information (PII) and/or sensitive data, such as (but not limited to) IP addresses, PC names, and usernames.
- Once data collection is complete, the tool saves the data locally on the machine within a subfolder and compressed zip file.
- No data is automatically sent to Microsoft. If you're using the tool during collaboration on a support issue, you might be asked to send the compressed data to Microsoft CSS using Secure File Exchange to facilitate the investigation of the issue.

For more information about Secure File Exchange, see [How to use Secure File Exchange to exchange files with Microsoft Support](/en-us/troubleshoot/azure/general/secure-file-exchange-transfer-files)

For more information about our privacy statement, see [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement).

## Requirements

- Before running the analyzer, we recommend ensuring your proxy or firewall configuration allows access to [Microsoft Defender for Endpoint service URLs](configure-environment#enable-access-to-microsoft-defender-for-endpoint-service-urls-in-the-proxy-server).
- The analyzer can run on supported editions of [Windows](minimum-requirements#windows-versions-supported-by-defender-for-endpoint), [Linux](mde-linux-prerequisites), or [macOS](microsoft-defender-endpoint-mac-prerequisites#system-requirements) either before of after onboarding to Microsoft Defender for Endpoint.
- For Windows devices, if you're running the analyzer directly on specific machines and not remotely via [Live Response](troubleshoot-collect-support-log), then SysInternals [PsExec.exe](/en-us/sysinternals/downloads/psexec) should be allowed (at least temporarily) to run. The analyzer calls into PsExec.exe tool to run cloud connectivity checks as Local System and emulate the behavior of the SENSE service.

    Note

    On Windows devices, if you use the attack surface reduction (ASR) rule [Block process creations originating from PSExec and WMI commands](attack-surface-reduction-rules-reference#block-process-creations-originating-from-psexec-and-wmi-commands), you might want to take one of the following actions to temporarily allow the analyzer to run cloud connectivity checks without being blocked:

    - [Configure an exclusion to the ASR rule](attack-surface-reduction-rules-overview#file-and-folder-exclusions-for-asr-rules).
    - Set the rule to **Audit** mode.
    - Disable the rule.