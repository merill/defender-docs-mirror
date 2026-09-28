---
layout: Conceptual
title: Troubleshoot installation issues for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-support-install
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot installation issues in Microsoft Defender for Endpoint on macOS.
ms.service: defender-endpoint
author: paulinbar
ms.author: painbar
ms.reviewer: joshbregman
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.topic: troubleshooting-general
ms.subservice: macos
ms.date: 2025-04-16T00:00:00.0000000Z
locale: en-us
document_id: 11345406-498a-2cad-c12b-c3decfb8004a
document_version_independent_id: 11345406-498a-2cad-c12b-c3decfb8004a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-support-install.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-support-install
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-support-install.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: a001ce81-5d7e-a499-f14e-02cc2394fffa
---

# Troubleshoot installation issues for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn

## Installation failed

For manual installation, the Summary page of the installation wizard says, "An error occurred during installation. The Installer encountered an error that caused the installation to fail. Contact the software publisher for assistance." For MDM deployments, it displays as a generic installation failure as well.

While we don't display an exact error to the end user, we keep a log file with installation progress in `/Library/Logs/Microsoft/mdatp/install.log`. Each installation session appends to this log file. You can use `sed` to output the last installation session only:

```bash
sed -n 'H; /^preinstall com.microsoft.wdav begin/h; ${g;p;}' /Library/Logs/Microsoft/mdatp/install.log
```

```Output
preinstall com.microsoft.wdav begin [2020-03-11 13:08:49 -0700] 804
INSTALLER_SECURE_TEMP=/Library/InstallerSandboxes/.PKInstallSandboxManager/CB509765-70FC-4679-866D-8A14AD3F13CC.activeSandbox/89FA879B-971B-42BF-B4EA-7F5BB7CB5695
correlation id=CB509765-70FC-4679-866D-8A14AD3F13CC
[ERROR] Downgrade from 100.88.54 to 100.87.80 is not permitted
preinstall com.microsoft.wdav end [2020-03-11 13:08:49 -0700] 804 => 1
```

In this example, the actual reason is prefixed with `[ERROR]`. The installation failed because a downgrade between these versions isn't supported.

## MDATP installs log missing or not updated

In rare cases, installation leaves no trace in MDATP's /Library/Logs/Microsoft/mdatp/install.log file. First, verify that an installation happened. Then analyze possible errors by querying macOS logs. It's helpful to do this in MDM deployments, when there's no client UI. We recommend that you use a narrow time window to run a query and filter by the logging process name, as there will be a huge amount of information.

```bash
grep '^2020-03-11 13:08' /var/log/install.log
```

```Output
log show --start '2020-03-11 13:00:00' --end '2020-03-11 13:08:50' --info --debug --source --predicate 'processImagePath CONTAINS[C] "install"' --style syslog
```