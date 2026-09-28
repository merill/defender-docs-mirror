---
layout: FAQ
title: Frequently asked questions (FAQs) about tamper protection - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/tamper-protection-faq
summary: >
  <p>Get answers about tamper protection requirements, supported platforms, configuration methods, policy precedence, exclusions, and alerts.</p>

  <p><strong>Applies to:</strong></p>

  <ul>

  <li><a href="microsoft-defender-endpoint">Microsoft Defender for Endpoint Plan 1</a></li>

  <li><a href="microsoft-defender-endpoint">Microsoft Defender for Endpoint Plan 2</a></li>

  <li><a href="microsoft-defender-antivirus-windows">Microsoft Defender Antivirus</a></li>

  <li><a href="/defender-business/mdb-overview">Microsoft Defender for Business</a></li>

  <li><a href="/Microsoft-365/business-premium/m365bp-overview">Microsoft 365 Business Premium</a></li>

  </ul>

  <p><strong>Platforms</strong></p>

  <ul>

  <li>Windows</li>

  <li>macOS</li>

  </ul>
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Get answers to common questions about configuring and managing Microsoft Defender for Endpoint tamper protection on Windows and macOS devices.
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
audience: ITPro
author: paulinbar
ms.author: painbar
ms.reviewer: joshbregman, sugamar
ms.topic: faq
ms.collection:
- m365-security
ms.date: 2026-09-08T00:00:00.0000000Z
ms.custom:
- msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: ada6d2d4-09a1-4a0a-5e69-b3bf06747efb
document_version_independent_id: ada6d2d4-09a1-4a0a-5e69-b3bf06747efb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/tamper-protection-faq.yml
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tamper-protection-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/tamper-protection-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 8241c2e4-5607-9a91-3ae3-b5030c1df776
---

# Frequently asked questions (FAQs) about tamper protection - Microsoft Defender for Endpoint | Microsoft Learn

Get answers about tamper protection requirements, supported platforms, configuration methods, policy precedence, exclusions, and alerts.

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint)
- [Microsoft Defender Antivirus](microsoft-defender-antivirus-windows)
- [Microsoft Defender for Business](/en-us/defender-business/mdb-overview)
- [Microsoft 365 Business Premium](/en-us/Microsoft-365/business-premium/m365bp-overview)

**Platforms**

- Windows
- macOS

## What requirements must devices meet to receive the tamper protection setting from the Microsoft Defender portal?

See [Requirements for tamper protection](tamper-protection-overview#requirements-for-tamper-protection) for supported operating systems, permissions, product versions, onboarding, and cloud-delivered protection requirements.

## On which versions of Windows can I configure tamper protection?

Tamper protection supports Windows 10 and later, including Enterprise multi-session; Windows Server 2016 and later; Windows Server version 1803 and later; Windows Server 2012 R2 using the modern unified solution; and Azure Stack HCI OS version 23H2 and later. See [Supported operating systems](tamper-protection-overview#supported-operating-systems).

## How do I configure tamper protection on macOS devices?

See [Configure tamper protection for Microsoft Defender for Endpoint on macOS](tamper-protection-macos-configure) for configuration methods, mode behavior, status verification, exclusions, and troubleshooting guidance.

## Does tamper protection affect non-Microsoft antivirus registration in the Windows Security app?

No. Non-Microsoft antivirus apps continue to register with the Windows Security app.

## Does tamper protection work when Microsoft Defender Antivirus is in passive mode?

Tamper protection continues to protect the Microsoft Defender Antivirus service and its features when Defender Antivirus runs in passive mode. The mode used by Defender Antivirus depends on the operating system, onboarding state, and installed antivirus products. For more information, see [Microsoft Defender Antivirus compatibility with other security products](microsoft-defender-antivirus-compatibility).

## How do I turn tamper protection on or off on Windows devices?

See [Configure tamper protection on Windows devices](tamper-protection-windows-configure) for instructions that use Intune, the Microsoft Defender portal, Configuration Manager with tenant attach, or the Windows Security app.

## Does tamper protection apply to Microsoft Defender Antivirus exclusions?

Yes, when the required conditions are met. See [Protect Microsoft Defender Antivirus exclusions with tamper protection](tamper-protection-antivirus-exclusions).

## How does configuring tamper protection in Intune affect how I manage Microsoft Defender Antivirus with Group Policy?

When tamper protection is on, Group Policy changes to tamper-protected settings might appear to succeed, but tamper protection blocks the changes. To make a temporary change on a device, use [troubleshooting mode](troubleshooting-mode-enable). To make permanent changes, adjust the tamper protection policy or exclude the affected devices from tamper protection through Intune or Configuration Manager. For more help, see [Troubleshoot problems with tamper protection](tamper-protection-troubleshoot).

## If my organization uses Microsoft Intune to configure tamper protection, does the policy apply only to the entire organization?

No. You can assign the Intune policy to your entire organization or to selected user or device groups. You can also exclude groups from the policy assignment. See [Configure tamper protection in Microsoft Intune](tamper-protection-windows-configure#configure-tamper-protection-in-microsoft-intune).

## What settings can't be changed when tamper protection is turned on?

See [Tamper protection overview](tamper-protection-overview#what-happens-when-tamper-protection-is-turned-on) for the current list of protected settings.

## If tamper protection is turned on in the Microsoft Defender portal, can a policy in Intune or Configuration Manager override it?

Yes. A policy that manages tamper protection takes precedence over the organization-wide setting in the Defender portal. See [Configure tamper protection on Windows devices](tamper-protection-windows-configure).

## How do I deploy DisableLocalAdminMerge?

Use Intune to configure [DisableLocalAdminMerge](/en-us/windows/client-management/mdm/defender-csp#configurationdisablelocaladminmerge). This setting is required when you [protect Microsoft Defender Antivirus exclusions with tamper protection](tamper-protection-antivirus-exclusions).

## How can I confirm whether exclusions are tamper protected on a Windows device?

Follow the guidance in [Protect Microsoft Defender Antivirus exclusions with tamper protection](tamper-protection-antivirus-exclusions).

## When antivirus exclusions are tamper protected, do I need to disable tamper protection to apply new exclusion policy settings from Intune or Configuration Manager?

No. You don't need to disable tamper protection to apply new exclusion policy settings from Intune or Configuration Manager. See [Protect Microsoft Defender Antivirus exclusions with tamper protection](tamper-protection-antivirus-exclusions).

## Can I configure tamper protection with Configuration Manager?

Yes. Configuration Manager uses tenant attach to deploy tamper protection from the Intune admin center. See [Configure tamper protection using Microsoft Configuration Manager](tamper-protection-windows-configure#configure-tamper-protection-using-microsoft-configuration-manager).

## Can local administrators change tamper protection on organization-managed devices?

On organization-managed devices, a policy or Defender portal setting takes precedence over changes made by a local administrator in the Windows Security app. See [Configure tamper protection on Windows devices](tamper-protection-windows-configure).

## Are tampering attempts shown as alerts in the Microsoft Defender portal?

Some tampering activity generates alerts. To reduce unnecessary alert noise, activity that isn't correlated with suspicious behavior might not generate an alert. The activity is still available in the device timeline and advanced hunting. See [View information about tampering attempts](tamper-protection-overview#view-information-about-tampering-attempts).