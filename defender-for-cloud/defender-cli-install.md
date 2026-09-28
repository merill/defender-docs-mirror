---
layout: Conceptual
title: Install the Defender for Cloud CLI - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-cli-install
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how to download and install the Defender for Cloud CLI on Windows, macOS, and Linux.
ms.topic: how-to
ms.date: 2026-05-25T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: cd3a3732-b779-5d4b-f852-9ad85caaaa87
document_version_independent_id: 7b906911-0867-4a59-e033-e6d2a4d265e2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-cli-install.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-cli-install
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-cli-install.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 7ffc5bdd-0415-6a66-6730-9f16085c843e
---

# Install the Defender for Cloud CLI - Microsoft Defender for Cloud | Microsoft Learn

This article explains how to download and install the Defender for Cloud command-line interface (CLI) on supported operating systems. You can use the CLI to run scans and automate security workflows.

## Download the CLI

The Defender for Cloud CLI is distributed as a standalone executable. Download the binary that matches your operating system and CPU architecture.

| Operating system | Architecture | Download URL |
| --- | --- | --- |
| Windows | x64 (64-bit) | https://aka.ms/defender-cli_win-x64 |
| Windows | x86 (32-bit) | https://aka.ms/defender-cli_win-x86 |
| Windows | ARM64 | https://aka.ms/defender-cli_win-arm64 |
| macOS | Apple silicon (M-series) | https://aka.ms/defender-cli_osx-arm64 |
| macOS | Intel | https://aka.ms/defender-cli_osx-x64 |
| Linux | x64 | https://aka.ms/defender-cli_linux-x64 |
| Linux | ARM64 | https://aka.ms/defender-cli_linux-arm64 |

## Set execution permissions (Linux and macOS)

On Linux and macOS, you must grant the downloaded binary permission to run.

Grant execution permission to the Defender binary so it can run on your system:

```bash
chmod +x defender
```

Tip

On macOS, you might see a **Developer cannot be verified** warning when running the CLI for the first time. To allow the binary, go to **System Settings** &gt; **Privacy & Security**, and then select **Open Anyway**.

## Add the CLI to your PATH (recommended)

Adding the CLI to your system PATH lets you run the `defender` command from any directory.

### Linux and macOS

Move the Defender binary to `/usr/local/bin`, which is a standard location in your PATH. This lets you run the command from any directory:

```bash
sudo mv defender /usr/local/bin/defender
```

### Windows

To add the Defender CLI directory to your Windows PATH, complete the following steps:

1. Create a folder. For example, `C:\tools\defender`
2. Move `defender.exe` into that folder.
3. In Windows Search, select **Edit the system environment variables**.
4. Select **Environment Variables**, then edit the **Path** variable under **System variables**.
5. Add the path to the folder you created. For example, `C:\tools\defender`
6. Save your changes.

## Verify the installation

Verify that Defender is installed and available in your PATH by checking the version:

```bash
defender --version
```

If the CLI is installed correctly, the command returns the current version.