---
layout: Conceptual
title: Deploy Microsoft Defender for Endpoint on Linux using golden images - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/linux-deploy-defender-for-endpoint-using-golden-images
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use preconfigured virtual machine templates (golden images) for rapid, consistent Microsoft Defender for Endpoint deployment on Linux.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: meghapriya
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-linux
ms.topic: install-set-up-deploy
ms.subservice: linux
ms.date: 2025-09-16T00:00:00.0000000Z
locale: en-us
document_id: 3ea4d58e-c2c0-3ad8-dce0-673b9b1019d0
document_version_independent_id: 3ea4d58e-c2c0-3ad8-dce0-673b9b1019d0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/linux-deploy-defender-for-endpoint-using-golden-images.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: linux-deploy-defender-for-endpoint-using-golden-images
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/linux-deploy-defender-for-endpoint-using-golden-images.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
platformId: 5a912d32-4244-bfc8-b3be-e40440888471
---

# Deploy Microsoft Defender for Endpoint on Linux using golden images - Microsoft Defender for Endpoint | Microsoft Learn

Golden images are preconfigured virtual machine templates used to rapidly and consistently deploy multiple identical systems across an organization. Microsoft Defender for Endpoint on Linux supports golden image deployment across cloud and on-premises environments, with improved handling of machine identifiers and hostnames, ensuring reliable telemetry and device correlation.

This guide walks you through:

- Deploying Microsoft Defender for Endpoint on a golden image.
- Preparing the image for cloning.
- Ensuring unique identifiers for each virtual machine instance.
- Specific steps for cloud and on-premises environments.

## Step 1: Deploy Microsoft Defender for Endpoint on a golden image

1. Prepare the base virtual machine

    - Install your preferred [supported Linux distribution](mde-linux-prerequisites#supported-linux-distributions) and apply all necessary system updates.
2. Deploy Microsoft Defender for Endpoint on a golden image

    There are several methods and tools that you can use to deploy Microsoft Defender for Endpoint on Linux (applicable to AMD64 and ARM64 Linux servers):

    - [Installer script based deployment](linux-installer-script)
    - [Ansible based deployment](linux-install-with-ansible)
    - [Chef based deployment](linux-deploy-defender-for-endpoint-with-chef)
    - [Puppet based deployment](linux-install-with-puppet)
    - [SaltStack based deployment](linux-install-with-saltack)
    - [Manual deployment](linux-install-manually)
    - [Direct onboarding with Defender for Cloud](/en-us/azure/defender-for-cloud/onboard-machines-with-defender-for-endpoint)
    - [Guidance for Defender for Endpoint on Linux Server with SAP](mde-linux-deployment-on-sap)
3. Validate the deployment

    Check the health status of the product by running the following command. A return value of `true` denotes that the product is functioning as expected:

    ```bash
    mdatp health
    ```

Note

Once Defender is successfully deployed on the golden image, there's no requirement to install and onboard it individually on each cloned machine.

## Step 2: Prepare the golden image for cloning

When deploying Defender for Endpoint on virtual machines, the hardware UUID reported by the system (system-uuid from dmidecode) is used to uniquely identify each instance.

Before making a snapshot of the virtual machine, ensure that each virtual machine clone gets a unique hardware UUID, as described in the following sections.

### On-premises machines

For on-premises environments, configure your virtualization platform so that each clone receives a unique hardware UUID from the underlying hypervisor. Follow these guidelines:

**KVM/libvirt**

- Don't hard-code the `<uuid>` element in the virtual machine's domain XML; if it's omitted, libvirt generates a random one at definition time.
- Alternatively, explicitly create a new UUID using `uuidgen`.
- For streamlined cloning, use `virt-clone` or `virt-manager`, which automatically assign unique UUIDs.

**VMware**

- During cloning, VMware prompts whether to keep the existing UUID or to create a new one. Always select **Create**, or configure `uuid.action = "create"` in the virtual machine's *.vmx* file.
- In VMware Cloud Director, set `backend.cloneBiosUuidOnVmCopy = 0` to force the creation of new UUIDs.

**Hyper-V**

Hyper-V automatically generates a new hardware UUID when you create a virtual machine using Hyper-V Manager or PowerShell ([New-VM](/en-us/powershell/module/hyper-v/new-vm)).

### Cloud virtual machines

Cloud platforms (for example, Azure, AWS, GCP) automatically inject unique metadata and identifiers via their instance metadata services (IMDS). No manual steps are required. Microsoft Defender for Endpoint automatically detects and uses these values to generate unique machine IDs.

## Hostname Management

If the hostname of a Linux server is changed after successful deployment of Defender, then you must restart the `mdatp` service to ensure the new hostname is correctly recognized by product.