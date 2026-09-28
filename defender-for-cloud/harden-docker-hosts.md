---
layout: Conceptual
title: Review Docker host hardening recommendations - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/harden-docker-hosts
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
description: How to protect your Docker hosts and verify they're compliant with the CIS Docker benchmark with Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 6c7dcb31-7eb2-2ba4-1151-59c28e45f438
document_version_independent_id: 107dfdef-bb87-f3ee-20bf-7fb7925da3c4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/harden-docker-hosts.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/harden-docker-hosts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/harden-docker-hosts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 8a6ea5a9-8f49-076c-c580-d0c2f8f8d3fd
---

# Review Docker host hardening recommendations - Microsoft Defender for Cloud | Microsoft Learn

The Defender for Servers plan in Microsoft Defender for Cloud identifies unmanaged containers hosted on IaaS Linux VMs, or other Linux machines running Docker containers. Defender for Servers continuously assesses the configuration of these Docker hosts, and compares them with the [Center for Internet Security (CIS) Docker Benchmark](https://www.cisecurity.org/benchmark/docker/).

This article explains how to review Docker host hardening recommendations, identify configuration issues, and remediate findings in Defender for Cloud.

- Defender for Cloud includes the entire ruleset of the CIS Docker Benchmark and alerts you if your containers don't satisfy any of the controls.
- When Defender for Servers finds misconfigurations, it generates security recommendations to address the findings.
- When vulnerabilities are found, they're grouped inside a single recommendation.

## Prerequisites

Before you review Docker host hardening recommendations, make sure the following prerequisites are met:

- You need [Defender for Servers Plan 2](defender-for-servers-overview) to use this feature.
- These CIS benchmark checks will not run on AKS-managed instances or Databricks-managed VMs.
- You need Reader permissions on the workspace to which the host connects.

## Identify Docker configuration issues

Use the following steps to find and remediate Docker host misconfigurations in Defender for Cloud.

1. From Defender for Cloud's menu, open the **Recommendations** page.
2. Filter to the recommendation **Vulnerabilities in container security configurations should be remediated** and select the recommendation.

    The recommendation page shows the affected resources (Docker hosts).

    ![Recommendation to remediate vulnerabilities in container security configurations.](media/monitor-container-security/docker-host-vulnerabilities-found.png)

    Note

    Machines that aren't running Docker will be shown in the **Not applicable resources** tab. They'll appear in Azure Policy as Compliant.
3. To view and remediate the CIS controls that a specific host failed, select the host you want to investigate.

    Tip

    If you started at the asset inventory page and reached this recommendation from there, select the **Take action** button on the recommendation page.

    ![Take action button to launch Log Analytics.](media/monitor-container-security/host-security-take-action-button.png)

    Log Analytics opens with a custom operation ready to run. The default custom query includes a list of all failed rules that were assessed, along with guidelines to help you resolve the issues.

    ![Log Analytics page with the query showing all failed CIS controls.](media/monitor-container-security/docker-host-vulnerabilities-in-query.png)
4. Tweak the query parameters if necessary.
5. When you're sure the command is appropriate and ready for your host, select **Run**.