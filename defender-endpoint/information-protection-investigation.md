---
layout: Conceptual
title: Use Microsoft Defender for Endpoint sensitivity labels to protect your data and prioritize security incident response - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/information-protection-investigation
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how Microsoft Defender for Endpoint sensitivity labels help protect sensitive data and prioritize incident investigation.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- ContentEngagementFY23
- tier2 - EngageScoreSep2022
ms.topic: how-to
ms.subservice: edr
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: a769c13c-5f1e-d492-1cdf-f07947badd12
document_version_independent_id: a769c13c-5f1e-d492-1cdf-f07947badd12
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/information-protection-investigation.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: information-protection-investigation
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/information-protection-investigation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 0e3d9740-917a-90ba-caca-660cdb297120
---

# Use Microsoft Defender for Endpoint sensitivity labels to protect your data and prioritize security incident response - Microsoft Defender for Endpoint | Microsoft Learn

A typical advanced persistent threat (APT) lifecycle involves data exfiltration, where data is *taken* from the organization. Sensitivity labels help security teams know where to start. They show which data has the highest priority to protect.

Defender for Endpoint uses sensitivity labels to simplify how you prioritize security incidents. For example, labels help you quickly spot incidents that involve devices with sensitive or confidential information.

Here's how to use sensitivity labels in Defender for Endpoint.

## Investigate incidents that involve sensitive data on devices with Defender for Endpoint

Learn how to use data sensitivity labels to prioritize incident investigation.

Note

Labels are detected for Windows 10, version 1809 or later, and Windows 11.

1. In Microsoft Defender portal, select **Incidents & alerts** &gt; **Incidents**.
2. Scroll over to see the **Data sensitivity** column. This column shows the sensitivity labels found on devices related to each incident. Use it to check whether sensitive files are affected.

    [![The Highly confidential option in the data sensitivity column](media/data-sensitivity-column.png)](media/data-sensitivity-column.png#lightbox)

    You can also filter based on **Data sensitivity**

    [![The data sensitivity filter](media/data-sensitivity-filter.png)](media/data-sensitivity-filter.png#lightbox)
3. Open the incident page to further investigate.

    [![The incident page details](media/incident-page.png)](media/incident-page.png#lightbox)
4. Select the **Devices** tab to identify devices storing files with sensitivity labels.

    [![The Device tab](media/investigate-devices-tab.png)](media/investigate-devices-tab.png#lightbox)
5. Select the devices that store sensitive data. Search the timeline to find which files might be affected. Then take action to protect that data.

    To narrow the results, search the device timeline for a specific sensitivity label. Only events for files that match that label name appear.

    [![The device timeline with narrowed down search results based on label](media/machine-timeline-labels.png)](media/machine-timeline-labels.png#lightbox)

Tip

Sensitivity label and file protection status data are also exposed through the 'DeviceFileEvents' in advanced hunting, allowing advanced queries and schedule detection to take into account sensitivity labels and file protection status.

## Related information about sensitivity labels

For more details about sensitivity labels, see the following articles:

- [Learn about sensitivity labels in Office 365](/en-us/purview/sensitivity-labels)
- [Apply sensitivity labels in email or Office apps](https://support.microsoft.com/Office/security-privacy/apply-sensitivity-labels-to-your-files)
- [Use sensitivity labels as a condition in Data Loss Prevention policies](/en-us/purview/dlp-sensitivity-label-as-condition)