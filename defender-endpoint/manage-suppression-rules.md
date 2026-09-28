---
layout: Conceptual
title: Manage Microsoft Defender for Endpoint suppression rules - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/manage-suppression-rules
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: You might need to prevent alerts from appearing in the portal by using suppression rules. Learn how to manage your suppression rules in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.subservice: edr
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 60030c9d-ba37-0325-095a-3437d2f2d666
document_version_independent_id: 60030c9d-ba37-0325-095a-3437d2f2d666
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/manage-suppression-rules.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-suppression-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/manage-suppression-rules.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: ec5e47e1-e6c3-7242-87fa-b9a4f8b599bf
---

# Manage Microsoft Defender for Endpoint suppression rules - Microsoft Defender for Endpoint | Microsoft Learn

There might be scenarios where you need to suppress alerts from appearing in the portal. You can create suppression rules for specific alerts that are known to be innocuous such as known tools or processes in your organization. For more information on how to suppress alerts, see [Suppress alerts](/en-us/defender-xdr/investigate-alerts?toc=/defender-endpoint/toc.json&amp;bc=/defender-endpoint/breadcrumb/toc.json#manage-alerts).

You can view a list of all the suppression rules and manage them in one place. You can also turn an alert suppression rule on or off.

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

1. Sign in to the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139) using an account with the Security administrator or Global Administrator role assigned.
2. In the navigation pane, select **Settings** &gt; **Endpoints** &gt; **Rules** &gt; **Alert suppression**. The list of suppression rules that users in your organization have created is displayed.
3. Select a rule by clicking on the check-box beside the rule name.
4. Click **Turn rule on**, **Edit rule**, or **Delete rule**. When making changes to a rule, you can choose to release alerts that the rule has already suppressed, regardless whether or not these alerts match the new criteria.

## View details of a suppression rule

To view the details of a suppression rule, perform the following steps:

1. In the navigation pane, select **Settings** &gt; **Endpoints** &gt; **Rules** &gt; **Alert suppression**. The list of suppression rules that users in your organization have created is displayed.
2. Select a rule name. Details of the rule is displayed. You'll see the rule details such as status, scope, action, number of matching alerts, created by, and date when the rule was created. You can also view associated alerts and the rule conditions.