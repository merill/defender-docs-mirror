---
layout: Conceptual
title: Multi-forest considerations - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/deploy/multi-forest
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn about how Microsoft Defender for Identity supports multiple Active Directory forests.
ms.date: 2023-08-10T00:00:00.0000000Z
ms.topic: article
ms.reviewer: martin77s
locale: en-us
document_id: b59dfd88-a72c-71be-cc35-dde16f978377
document_version_independent_id: b59dfd88-a72c-71be-cc35-dde16f978377
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/deploy/multi-forest.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy/multi-forest
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/deploy/multi-forest.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: 42f38fcc-54af-5734-3c92-7dde7f8f60ad
---

# Multi-forest considerations - Microsoft Defender for Identity | Microsoft Learn

Microsoft Defender for Identity supports organizations with multiple Active Directory forests, giving you the ability to easily monitor activity and profile users across forests.

Enterprise organizations typically have several Active Directory forests - often used for different purposes, including legacy infrastructure from corporate mergers and acquisitions, geographical distribution, and security boundaries (red forests).

Securing your multiple Active Directory forests with Defender for Identity provides the following advantages:

- **View and investigate** activities performed by users across multiple forests from a single location
- **Gain improved detection** and reduce false positives with advanced Active Directory integration and account resolution
- **Gain greater control and easier deployment**, with an improved set of health issues and reporting for cross-org coverage when your domain controllers are all monitored from a single Defender for Identity server

Note

Each Defender for Identity sensor can only report to a single Defender for Identity workspace.

## Detection activity across multiple forests

To detect cross-forest activities, Defender for Identity sensors query domain controllers in remote forests to create profiles for all entities involved, including users and computers from remote forests.

- Defender for Identity sensors can be installed on domain controllers in all forests, even forests with no trust.
- [Add additional credentials](create-directory-service-account-gmsa#configure-a-directory-service-account-in-microsoft-defender-portal) on the **Directory services accounts** page to support any untrusted forests in your environment.

    - Only one credential is required to support all forests with a two-way trust.
    - Additional credentials are required for each forest with non-Kerberos trust or no trust.
    - There's a default limit of 30 credentials per Defender for Identity workspace. [Contact support](../support) if you need to add more than 30 credentials.

For more information, see [Microsoft Defender for Identity Directory Service account recommendations](directory-service-accounts).

## Network traffic impact for multi-forest support

When Defender for Identity maps your forests, it uses the following process:

1. After the Defender for Identity sensor starts running, the sensor queries the remote Active Directory forests and retrieves a list of users and machine data for profile creation.
2. Every 5 minutes, each Defender for Identity sensor queries one domain controller from each domain, from each forest, to map all the forests in the network.

    The Defender for Identity sensors map the forests using the `trustedDomain` Active Directory object, by signing in and checking the trust type.

You may see ad-hoc traffic when the Defender for Identity sensor detects cross forest activity. When this occurs, the Defender for Identity sensors will send an LDAP query to the relevant domain controllers to retrieve entity information.