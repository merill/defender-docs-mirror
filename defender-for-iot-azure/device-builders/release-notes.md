---
layout: Conceptual
title: What's new in Microsoft Defender for IoT for device builders - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/release-notes
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
ms.subservice: device-builders
description: Learn about the latest updates for Defender for IoT device builders.
ms.topic: whats-new
ms.date: 2025-10-05T00:00:00.0000000Z
locale: en-us
document_id: dd9b4f2f-9f55-574b-b1f3-7429d96bbf2f
document_version_independent_id: 872d0a81-29d7-c980-10a8-3c9c3ccc5a75
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/release-notes.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/release-notes
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/release-notes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: e6055090-dd8e-45a5-1e93-a63bf2a0cb89
---

# What's new in Microsoft Defender for IoT for device builders - Microsoft Defender for IoT | Microsoft Learn

This article lists new features and feature enhancements in Microsoft Defender for IoT for device builders.

Noted features are in PREVIEW. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include other legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

For more information, see [Upgrade the Microsoft Defender for IoT micro agent](upgrade-micro-agent).

## November 2024

The firmware analysis documentation is now located and maintained as part of the Azure documentation. See the full [firmware analysis documentation](/en-us/azure/firmware-analysis/overview-firmware-analysis).

## March 2024

**Updates to Defender for IoT Firmware Analysis:**

- **Azure CLI and PowerShell commands**: Automate your workflow of analyzing firmware images by using the [Firmware Analysis Azure CLI](/en-us/cli/azure/service-page/firmware%20analysis) or the [Firmware Analysis PowerShell commands](/en-us/powershell/module/az.firmwareanalysis).
- **User choice in resource group**: Pick your own resource group or create a new resource group to use Defender for IoT Firmware Analysis during the onboarding process.

    [![Screenshot that shows resource group picker while onboarding.](media/whats-new-firmware-analysis/pick-resource-group.png)](media/whats-new-firmware-analysis/pick-resource-group.png#lightbox)
- **New UI format with Firmware inventory**: Subtabs to organize Getting started, Subscription management, and Firmware inventory.

    [![Screenshot that shows the firmware inventory in the new UI.](media/whats-new-firmware-analysis/firmware-inventory-tab.png)](media/whats-new-firmware-analysis/firmware-inventory-tab.png#lightbox)
- **Enhanced documentation**: Updates to [Tutorial: Analyze an IoT/OT firmware image](tutorial-analyze-firmware) documentation addressing the new onboarding experience.

## January 2024

**Updates to Defender for IoT Firmware Analysis since public preview in July 2023:**

- **PDF report generator**: Addition of a **Download as PDF** capability on the **Overview page** that generates and downloads a PDF report of the firmware analysis results.

    [![Screenshot that shows the new Download as PDF button.](media/whats-new-firmware-analysis/overview-pdf-download.png)](media/whats-new-firmware-analysis/overview-pdf-download.png#lightbox)
- **Reduced analysis time**: Analysis time has been shortened by 30-80%, depending on image size.
- **CODESYS libraries detection**: Defender for IoT Firmware Analysis now detects the use of CODESYS libraries, which Microsoft recently identified as having high-severity vulnerabilities. These vulnerabilities can be exploited for attacks such as remote code execution (RCE) or denial of service (DoS). For more information, see [Multiple high severity vulnerabilities in CODESYS V3 SDK could lead to RCE or DoS](https://www.microsoft.com/en-us/security/blog/2023/08/10/multiple-high-severity-vulnerabilities-in-codesys-v3-sdk-could-lead-to-rce-or-dos/).
- **Enhanced documentation**: Addition of documentation addressing the following concepts:

    - [Azure role-based access control for Defender for IoT Firmware Analysis](defender-iot-firmware-analysis-rbac), which explains roles and permissions needed to upload firmware images and share analysis results, and an explanation of how the **FirmwareAnalysisRG** resource group works
    - [Frequently asked questions](defender-iot-firmware-analysis-faq)
- **Improved filtering for each report**: Each subtab report now includes more fine-grained filtering capabilities.
- **Firmware metadata**: Addition of a collapsible tab with firmware metadata that is available on each page.

    [![Screenshot that shows the new metadata tab in the Overview page.](media/whats-new-firmware-analysis/overview-firmware-metadata.png)](media/whats-new-firmware-analysis/overview-firmware-metadata.png#lightbox)
- **Improved version detection**: Improved version detection of the following libraries:

    - pcre
    - pcre2
    - net-tools
    - zebra
    - dropbear
    - bluetoothd
    - WolfSSL
    - sqlite3
- **Added support for file systems**: Defender for IoT Firmware Analysis now supports extraction of the following file systems. For more information, see [Firmware Analysis FAQs](defender-iot-firmware-analysis-faq#what-types-of-firmware-images-does-defender-for-iot-firmware-analysis-support):

    - ISO
    - RomFS
    - Zstandard and non-standard LZMA implementations of SquashFS

## July 2023

**Firmware Analysis public preview announcement**

Microsoft Defender for IoT Firmware Analysis is now available in public preview. Defender for IoT can analyze your device firmware for common weaknesses and vulnerabilities, and provide insight into your firmware security. This analysis is useful whether you build the firmware in-house or receive firmware from your supply chain.

For more information, see [Firmware analysis for device builders](overview-firmware-analysis).

[![Screenshot that shows clicking view results button for a detailed analysis of the firmware image.](media/whats-new-firmware-analysis/overview.png)](media/whats-new-firmware-analysis/overview.png#lightbox)

## December 2022

**Version 4.6.2**:

When upgrading the micro agent from version 4.2.\* to 4.6.2, you would first need to remove the package and then reinstall it. For more information, see [Upgrade the Microsoft Defender for IoT micro agent](upgrade-micro-agent).

- **Peripheral collector**: Addition of a new collector that detects physical plugins of devices. For more information, see [Micro agent event collection - Peripheral events](concept-event-aggregation#peripheral-events-event-based-collector).
- **File system collector**: Addition of a new collector that monitors specified file systems. For more information, see [Micro agent event collection - File system events](concept-event-aggregation#file-system-events-event-based-collector).
- **Statistics collector**: Addition of a new collector that reports for each collection cycle, data regarding the different collectors in the agent. For more information, see [Micro agent event collection - Statistics events](concept-event-aggregation#statistics-data-trigger-based-collector).
- **System information collector**: System information collector now collects the agent type (Edge/Standalone) and version. For more information, see [Micro agent event collection - System information events](concept-event-aggregation).
- **New alerts**: Now supporting new peripheral and file system alerts. For more information, see [Micro agent security alerts](concept-agent-based-security-alerts).
- **DMI decode alternative**: Now supporting new alternative to report device information in case device does not support DMI decoder. For more information, see [How to configure DMI decoder](how-to-configure-dmi-decoder).
- **Firmware information**: Now supporting device firmware vendor and version collected using DMI decoder or its alternative. For more information, see [How to configure DMI decoder](how-to-configure-dmi-decoder).
- **Device Provisioning Service support**: Now you can use DPS to provision your micro agent and devices at scale. For more information, see [How to provision the micro agent using DPS](how-to-provision-micro-agent).
- **AMQP protocol over web socket protocol support**: Now supporting AMQP over web socket protocol that can be added after installing your micro agent. For more information, see [Add AMQP over websocket protocol support](tutorial-standalone-agent-binary-installation#add-amqp-protocol-support).
- **SBoM collector bug fix**: Now supporting collection of all packages instead of first ingested 500. For more information, see [Micro agent event collection - SBoM events](concept-event-aggregation#sbom-trigger-based-collector).
- **Debian 10 ARM 64 buster support**: Now supporting Debian 10 ARM 64 devices. For more information, see [Agent portfolio overview and OS support](concept-agent-portfolio-overview-os-support).
- **22.04 Ubuntu support**: Now supporting Ubuntu 22.04 devices. For more information, see [Agent portfolio overview and OS support](concept-agent-portfolio-overview-os-support).