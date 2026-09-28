---
layout: Conceptual
title: Upgrade the Microsoft Defender for IoT Micro Agent - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/upgrade-micro-agent
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
description: Learn how to upgrade your Defender for IoT micro agent for device builders.
ms.date: 2026-06-12T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: a6de8f08-916f-7a95-9ebb-a4a8a4c6bd8c
document_version_independent_id: cad6b388-cd25-01b4-940e-ace781c62b6d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/upgrade-micro-agent.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/upgrade-micro-agent
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/upgrade-micro-agent.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: e35442f9-5e81-3681-772d-802a23547414
---

# Upgrade the Microsoft Defender for IoT Micro Agent - Microsoft Defender for IoT | Microsoft Learn

This article describes how to upgrade a Microsoft Defender for IoT micro agent to the latest software version on Debian or Ubuntu-based Linux distributions. It covers upgrade procedures for both the standalone micro agent and the micro agent for Edge, including version-specific steps for upgrading from version 4.2.\* to 4.6.2 and from legacy versions (3.13.1 or lower). Device builders can use these procedures to keep their IoT devices protected with the latest security capabilities.

For more information, see our [release notes for device builders](release-notes).

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Upgrade a micro agent from version 4.2.\* to 4.6.2

When upgrading the micro agent from version 4.2.\* to 4.6.2, you would first need to remove the package and then reinstall it.

### Standalone micro agent

1. Remove the current package. Run:

    ```bash
    sudo apt-get remove defender-iot-micro-agent
    ```
2. Ensure that you've upgraded the apt. Run:

    ```bash
    sudo apt-get update
    ```
3. Install the Defender for IoT micro agent on Debian or Ubuntu-based Linux distributions. Run:

    ```bash
    sudo apt-get install defender-iot-micro-agent
    ```

### Micro agent for Edge

1. Remove the current package. Run:

    ```bash
    sudo apt-get remove defender-iot-micro-agent-edge
    ```
2. Ensure that you've upgraded the apt. Run:

    ```bash
    sudo apt-get update
    ```
3. Install the Defender for IoT micro agent on Debian or Ubuntu-based Linux distributions. Run:

    ```bash
    sudo apt-get install defender-iot-micro-agent-edge
    ```

## Upgrade a standalone micro agent

Perform the following steps to upgrade a standalone micro agent to the latest version:

1. Ensure that you've upgraded the apt. Run:

    ```bash
    sudo apt-get update
    ```
2. Install the Defender for IoT micro agent on Debian or Ubuntu-based Linux distributions. Run:

    ```bash
    sudo apt-get install defender-iot-micro-agent
    ```

## Upgrade a micro agent for Edge

Perform the following steps to upgrade a micro agent for Edge to the latest version:

1. Ensure that you've upgraded the apt. Run:

    ```bash
    sudo apt-get update
    ```
2. Install the Defender for IoT micro agent on Debian or Ubuntu-based Linux distributions for Edge. Run:

    ```bash
    sudo apt-get install defender-iot-micro-agent-edge
    ```

## Upgrade a standalone micro agent from a legacy version

The following upgrade steps apply when upgrading a standalone micro agent from version 3.13.1 or lower to version 4.1.2 or higher.

In version 4.1.2, the standalone micro agent directory changed to align with standard Linux installation directory structures. The directory change in version 4.1.2 requires customers to reauthenticate the micro agent and modify the connection string location.

1. Upgrade your micro agent as described in Upgrade a standalone micro agent: run `sudo apt-get update`, then run `sudo apt-get install defender-iot-micro-agent`.
2. Reauthenticate your micro agent. For more information, see [Authenticate the micro agent](tutorial-standalone-agent-binary-installation#authenticate-the-micro-agent).

## Install a specific version of the micro agent

Specify a version number in your command to install the specified micro agent version.

Use the following command syntax:

```bash
sudo apt-get install defender-iot-micro-agent=<version>
```