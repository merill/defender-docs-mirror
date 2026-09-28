---
layout: Conceptual
title: Security solutions integrations (legacy) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/partner-integration
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
description: Learn about how Microsoft Defender for Cloud integrates with partner solutions to enhance your security posture and protect your Azure resources.
ms.topic: concept-article
ms.date: 2025-04-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d65dd27d-2294-c27a-19e6-514e69e4b197
document_version_independent_id: 69118275-2cf6-b465-5e1a-4b032b4c4ae0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/partner-integration.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/partner-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/partner-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: b38b3b2e-1cb5-4a7b-f961-da054f6703b0
---

# Security solutions integrations (legacy) - Microsoft Defender for Cloud | Microsoft Learn

This article provides information about security solutions that integrate with Microsoft Defender for Cloud.

Defender for Cloud integrates with Microsoft services and partner solutions. These integrations help you:

- **Simplify deployment**: Defender for Cloud offers streamlined provisioning of integrated partner solutions. For solutions like antimalware and vulnerability assessment, Defender for Cloud can provision the agent on your virtual machines. For firewall appliances, Defender for Cloud can take care of much of the network configuration required.
- **Integrate detection**: Security events from partner solutions are automatically collected, aggregated, and displayed as part of Defender for Cloud alerts and incidents. These events are also fused with detections from other sources to provide advanced threat-detection capabilities.
- **Unify monitoring and management**: Integrated events in Defender for Cloud help you to monitor partner solutions at a glance. Basic management is available, with easy access to advanced setup by using the partner solution.
- **Extend capabilities**: Some integrations extend Defender for Cloud capabilities. For example:

    - Defender for Cloud supports [third-party integrations](defender-partner-applications) to help enhance runtime security capabilities provided by Defender for APIs.
    - Defender for Cloud [integrates with ServiceNow](integration-servicenow) to help prioritize remediation of security recommendations, and to create and monitor tickets.

## Integrations

Integrated solutions appear in the Azure portal, in **Defender for Cloud** -&gt; **Management** -&gt; **Security solutions**.

Azure security solutions that are deployed from Defender for Cloud are automatically connected. You can also connect other security data sources, including computers running on-premises or in other clouds.

[![Screenshot showing the Security solutions page.](media/partner-integration/security-solutions-page-01-2023.png)](media/partner-integration/security-solutions-page-01-2023.png#lightbox)

### Connected solutions

The **Connected solutions** section includes security solutions that are currently connected to Defender for Cloud.

![Screenshot that shows the available connectable solutions.](media/partner-integration/connected-solutions.png)

The status of a security solution can be:

- **Healthy** (green): No health issues.
- **Unhealthy** (red): There's a health issue that requires immediate attention. If no health data is available and no alerts were received within the last 14 days, Defender for Cloud indicates that the solution is unhealthy or not reporting.
- **Stopped reporting** (orange): The solution stopped reporting health status.
- **Not reported** (gray): No health data is available. The solution hasn't reported any health data yet. A solution's status might be unreported if it was connected recently and is still deploying.

If health status isn't available, Defender for Cloud shows the date and time of the last event received to indicate whether the solution is reporting or not.

You can drill down into each solution to manage it.

### Discovered solutions

Defender for Cloud automatically discovers security solutions that are running in Azure but not connected to Defender for Cloud, and displays them in the **Discovered solutions** section. You can connect solutions as needed to integrate them with Defender for Cloud.

### Add data sources

The **Add data sources** section includes other available data sources that can be connected. For instructions on adding data from any of these sources, select **ADD**.

![Screenshot that shows the available additional data sources.](media/partner-integration/add-data-sources.png)