---
layout: Conceptual
title: Detect and block potentially unwanted applications with Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-pua
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Detect and block Potentially Unwanted Applications (PUA) using Microsoft Defender for Endpoint on macOS.
ms.service: defender-endpoint
author: paulinbar
ms.author: painbar
ms.reviewer: joshbregman
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.topic: concept-article
ms.subservice: macos
ms.date: 2025-04-16T00:00:00.0000000Z
locale: en-us
document_id: 6f1dce7f-67c1-2f4e-3e19-b6c582ae7a24
document_version_independent_id: 6f1dce7f-67c1-2f4e-3e19-b6c582ae7a24
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-pua.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-pua
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-pua.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: dc34036a-592a-4d49-226c-7fecabf9548c
---

# Detect and block potentially unwanted applications with Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn

The potentially unwanted application (PUA) protection feature in Microsoft Defender for Endpoint on macOS can detect and block PUA files on endpoints in your network.

These applications aren't considered viruses, malware, or other types of threats, but might perform actions on endpoints that adversely affect their performance or use. PUA can also refer to applications that are considered to have poor reputation.

These applications can increase the risk of your network being infected with malware, cause malware infections to be harder to identify, and can waste IT resources in cleaning up the applications.

## How it works

Microsoft Defender for Endpoint on macOS can detect and report PUA files. When configured in blocking mode, PUA files are moved to the quarantine.

When a PUA is detected on an endpoint, Microsoft Defender for Endpoint on macOS presents a notification to the user, unless notifications are disabled. The threat name contains the word "Application".

## Configure PUA protection

PUA protection in Microsoft Defender for Endpoint on macOS can be configured in one of the following ways:

- **Off**: PUA protection is disabled.
- **Audit**: PUA files are reported in the product logs, but not in Microsoft Defender portal. No notification is presented to the user and no action is taken by the product.
- **Block**: PUA files are reported in the product logs and in Microsoft Defender portal. The user is presented with a notification and action is taken by the product.

Warning

By default, PUA protection is configured in **Audit** mode.

You can configure how PUA files are handled from the command line or from the management console.

### Use the command-line tool to configure PUA protection

In Terminal, execute the following command to configure PUA protection:

```bash
mdatp threat policy set --type potentially_unwanted_application --action [off|audit|block]
```

### Use the management console to configure PUA protection:

In your enterprise, you can configure PUA protection from a management console, such as JAMF or Intune, similarly to how other product settings are configured. For more information, see the [Threat type settings](mac-preferences#threat-type-settings) section of the [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences) article.

### Test PUA protection

You're able to test PUA protection by going to [Potentially unwanted applications (PUA) demonstration](defender-endpoint-demonstration-potentially-unwanted-applications).