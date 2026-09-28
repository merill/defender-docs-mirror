---
layout: Conceptual
title: Detect and block potentially unwanted applications with Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/linux-pua
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Detect and block Potentially Unwanted Applications (PUA) using Microsoft Defender for Endpoint on Linux.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: gopkr
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-linux
ms.topic: concept-article
ms.subservice: linux
ms.date: 2024-10-11T00:00:00.0000000Z
locale: en-us
document_id: fb389aac-9574-8287-26b9-51b629d7b359
document_version_independent_id: fb389aac-9574-8287-26b9-51b629d7b359
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/linux-pua.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: linux-pua
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/linux-pua.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 39ffbdd2-70c9-983b-ff03-98f987ff7890
---

# Detect and block potentially unwanted applications with Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn

The potentially unwanted application (PUA) protection feature in Defender for Endpoint on Linux can detect and block PUA files on endpoints in your network.

These applications are not considered viruses, malware, or other types of threats, but might perform actions on endpoints that adversely affect their performance or use. PUA can also refer to applications that are considered to have poor reputation.

These applications can increase the risk of your network being infected with malware, cause malware infections to be harder to identify, and can waste IT resources in cleaning up the applications.

## How it works

Defender for Endpoint on Linux can detect and report PUA files. When configured in blocking mode, PUA files are moved to the quarantine.

When a PUA is detected on an endpoint, Defender for Endpoint on Linux keeps a record of the infection in the threat history. The history can be visualized from the Microsoft Defender portal or through the `mdatp` command-line tool. The threat name will contain the word "Application".

## Configure PUA protection

PUA protection in Defender for Endpoint on Linux can be configured in one of the following ways:

- **Off**: PUA protection is disabled.
- **Audit**: PUA files are reported in the product logs, but not in the Defender portal. No record of the infection is stored in the threat history and no action is taken by the product.
- **Block**: PUA files are reported in the product logs and in the Defender portal. A record of the infection is stored in the threat history and action is taken by the product.

Warning

By default, PUA protection is configured in **Audit** mode.

You can configure how PUA files are handled from the command line or from the management console.

### Use the command-line tool to configure PUA protection:

In Terminal, execute the following command to configure PUA protection:

```bash
mdatp threat policy set --type potentially_unwanted_application --action [off|audit|block]
```

### Use the management console to configure PUA protection:

In your enterprise, you can configure PUA protection from a management console, such as Puppet or Ansible, similarly to how other product settings are configured. For more information, see [Threat type settings](linux-preferences#threat-type-settings) in [Set preferences for Defender for Endpoint on Linux](linux-preferences).