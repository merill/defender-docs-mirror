---
layout: Conceptual
title: Quarterly or Ad-hoc Operational Guide - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/ops-guide/ops-guide-quarterly
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
description: Review quarterly and ad hoc Microsoft Defender for Identity tasks, including checking service health, verifying sensor deployment in server setup processes, and validating domain controller audit policies.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: martin77s
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 7c4f6fc4-b371-4613-b4a3-3334c59418cb
document_version_independent_id: 7c4f6fc4-b371-4613-b4a3-3334c59418cb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/ops-guide/ops-guide-quarterly.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ops-guide/ops-guide-quarterly
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/ops-guide/ops-guide-quarterly.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/c4c18c0c-090d-4c28-a4be-9e6214a0c4fb
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/b22d517c-92cf-4ee3-8dca-36c6cd062217
platformId: 55c1c75f-0705-4cd0-c84b-e4a7d3a25b09
---

# Quarterly or Ad-hoc Operational Guide - Microsoft Defender for Identity | Microsoft Learn

This article reviews the Microsoft Defender for Identity activities we recommend for your team on a quarterly or ad-hoc basis, depending on your organization's needs and processes.

Perform ad hoc activities as issues arise in your organization, or as part of a quarterly operational review.

## Review Microsoft service health

Check the current status of Microsoft services to identify any known issues that might affect your environment.

**Where**: Check the following locations:

- In the Microsoft 365 admin center, select **Health &gt; Service health**
- [Microsoft 365 Service health status](https://status.office365.com/)
- X: https://twitter.com/MSFT365status

**Persona**: Security and compliance administrators

If you're experiencing issues with a cloud service, we recommend checking service health updates to determine whether it's a known issue, with a resolution in progress, before you call support or spend time troubleshooting.

For more information, see [Review Defender for Identity health issues](ops-guide-daily#review-defender-for-identity-health-issues).

## Review server setup process to include sensors

**Where**: Your organization's internal process documentation

**Persona**: Security administrators

We recommend that you periodically verify your organization's server setup process to make sure that it includes installing the Defender for Identity sensor. This ensures that all new domain controllers, AD CS, and AD FS servers are protected right away.

For more information, see [Deploy Microsoft Defender for Identity with Microsoft Defender](../deploy/deploy-defender-identity).

## Check domain configuration via PowerShell

**Where**: PowerShell on your Defender for Identity sensor machines

**Persona**: Security administrators

We recommend that you periodically run the **Test-MDIConfiguration** PowerShell command. It checks whether your domain controller audit policy settings are correct. Wrong settings can cause gaps in the Event Log and reduce Defender for Identity coverage.

For more information, see:

- [Configure audit policies for Windows event logs](../deploy/configure-windows-event-collection)
- [Test-MDIConfiguration](/en-us/powershell/module/defenderforidentity/test-mdiconfiguration) PowerShell documentation