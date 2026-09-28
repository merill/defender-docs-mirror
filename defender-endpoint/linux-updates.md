---
layout: Conceptual
title: Deploy updates for Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/linux-updates
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Describes how to deploy updates for Microsoft Defender for Endpoint on Linux in enterprise environments.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: gopkr
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-linux
ms.topic: install-set-up-deploy
ms.subservice: linux
ms.date: 2024-12-16T00:00:00.0000000Z
locale: en-us
document_id: e04cf44e-5fbf-63f8-9fe4-a3b0bc94bca4
document_version_independent_id: e04cf44e-5fbf-63f8-9fe4-a3b0bc94bca4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/linux-updates.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: linux-updates
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/linux-updates.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 7ecae553-2fc8-0e10-58c2-6bd5b42736ab
---

# Deploy updates for Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft regularly publishes software updates to improve performance, security, and to deliver new features.

Warning

Each version of Defender for Endpoint on Linux is set to expire automatically after 9 months. While expired versions continue to receive security intelligence updates, install the latest version to get all available fixes and enhancements. To check the expiration date, run the following command:

```bash
mdatp health --field product_expiration
```

Expired clients report a health issue and warning message when you run the following command:

```bash
mdatp health
```

Indicators of an expired client include the message, "**ATTENTION: No license found. Contact your administrator for help**." with the following attributes:

```bash
ATTENTION: No license found. Contact your administrator for help.
healthy                                     : false
health_issues                               : ["missing license"]
licensed                                    : false
```

Defender for Endpoint capabilities that are generally available are equivalent, regardless of which update channel is used for deployment (Beta (Insider), Preview (External), Current (Production)).

To update Defender for Endpoint on Linux manually, run one of the following commands:

## RHEL and variants (CentOS and Oracle Linux)

```bash
sudo yum update mdatp
```

## SLES and variants

```bash
sudo zypper update mdatp
```

## Ubuntu and Debian systems

```bash
sudo apt-get install --only-upgrade mdatp
```

Important

When Defender for Cloud is provisioning the Microsoft Defender for Endpoint agent to Linux servers, it keeps the client updated automatically.

To schedule an update of Microsoft Defender for Endpoint on Linux, see [Schedule an update for Microsoft Defender for Endpoint on Linux](linux-update-mde-linux).