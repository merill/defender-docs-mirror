---
layout: Conceptual
title: How to use the Microsoft Defender Experts service - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-experts/defender-experts-mdr-start-using
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: 
description: Learn about the different in-portal experiences in Microsoft Defender where you can view and perform Defender Experts notifications and activities
ms.service: defender-experts-for-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
audience: ITPro
ms.collection:
- m365-security
- tier1
- essentials-manage
ms.topic: how-to
search.appverid: met150
ms.date: 2026-06-16T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 0c842b35-2265-2741-3df5-ae5d6e72d09c
document_version_independent_id: 0c842b35-2265-2741-3df5-ae5d6e72d09c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-experts/defender-experts-mdr-start-using.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-experts/defender-experts-mdr-start-using
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-experts/defender-experts-mdr-start-using.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 40c89475-12ad-5307-9ffa-c7298a00e414
---

# How to use the Microsoft Defender Experts service - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender Experts MDR](defender-experts-mdr-overview)
- [Microsoft Defender Experts for Servers](defender-experts-servers-overview)

After you complete the [onboarding steps and readiness checks](defender-experts-mdr-get-started) for the Microsoft Defender Experts service and the experts start performing comprehensive response work on your behalf, you receive notifications about incidents that require remediation steps and targeted recommendations on critical incidents. You can also start chatting with the experts or your security delivery experts (SDXs) and view reports on the number of incidents they investigated and resolved.

This article describes the different in-portal experiences in Microsoft Defender where you can view and perform the previously mentioned Defender Experts notifications and activities, among others. These experiences provide you visibility into the experts' activities and clear entry points into tasks that require your attention.

## Where to find Microsoft Defender Experts in Microsoft Defender portal

You can view and monitor Defender Experts activities in the following sections of the Microsoft Defender portal:

- As a status card in the portal home page
- In the portal navigation menu

[![Screenshot of the Microsoft Defender portal with the Defender Experts experiences highlighted.](media/start-using-mdex-xdr/defender-experts-experiences.png)](media/start-using-mdex-xdr/defender-experts-experiences.png#lightbox)

### Find Defender Experts from the home page card

The Defender Experts status card in the Defender portal home page is located in the upper portion. You see a summary of the experts' activities and items requiring your attention immediately when you open the portal.

By default, this status card is located in the top row immediately after the home page banner. It surfaces the following information, depending on the state of your environment:

- Onboarding and readiness calls to action
- Managed response incidents that require customer action
- Messages that might be awaiting your response
- Incidents that Defender Experts handled in the last month
- A call to action to open Defender Experts overview page for more details

### Navigation menu

When you subscribe to the Defender Experts service, you see **Defender Experts** as a distinct entry in the Defender portal navigation menu. This feature provides you with consistent and predictable access to the service across the portal.

From this navigation menu, you can go directly to the Defender Experts overview page or check your communications with the experts.

#### Open the Overview page

The **Defender Experts Overview** page provides a consolidated view of Defender Experts activity, status, and outcomes. It helps you easily understand what Defender Experts needs you to do and observe the value of the service without navigating to multiple areas of the portal.

[![Screenshot of Defender Experts overview page.](media/start-using-mdex-xdr/defender-experts-overview-page.png)](media/start-using-mdex-xdr/defender-experts-overview-page.png#lightbox)

The information on the Defender Experts Overview page helps you answer the following questions:

- What does Defender Experts need me to do right now?
- What did Defender Experts recently investigate or hunt for?

The page brings together high-signal information in a single place, including:

- **Items that require your action:** A summary of incidents or findings where customer input or acknowledgment is needed.
- **XDR highlights:** Recent Defender Experts investigations, detections, or completed work along with their outcomes.
- **Hunting highlights:** A snapshot of notable hunting activity and results.

#### View Defender Experts messages

The Defender Experts messages page lets you track your managed response chat conversations and inquiries you submitted through Ask Defender Experts.

[![Screenshot of Defender Experts messages page.](media/start-using-mdex-xdr/defender-experts-messages.png)](media/start-using-mdex-xdr/defender-experts-messages.png#lightbox)

Select a message topic to open a side panel where you can read through the conversation and reply. You can also perform several actions to manage your messages, including:

- Export the list of messages into a .CSV file
- Mark messages as unread or read
- Group messages according to status, submitter, and reference (for example, incident ID)
- Display messages from a given time period

## How Defender Experts in-portal experiences work together

The home page card, navigation menu, and overview page work together to give you a cohesive user experience flow:

1. You discover Defender Experts from the portal homepage left navigation menu.
2. To open the Defender Experts overview page, select **Defender Experts** &gt; **Overview** from the navigation menu.
3. From the overview page, drill down into specific incidents, investigations, or hunting-related experiences.

This flow reduces friction, improves visibility into managed hunting activity, and helps you more easily understand the scope and impact of Defender Experts.