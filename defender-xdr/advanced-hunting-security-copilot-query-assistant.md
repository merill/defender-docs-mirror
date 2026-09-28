---
layout: Conceptual
title: Microsoft Security Copilot advanced hunting query assistant - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-security-copilot-query-assistant
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how Microsoft Security Copilot Threat Hunting Assistant can help you generate a KQL query.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- security-copilot
- magic-ai-copilot
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ah
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 296ea319-a839-9d79-9442-a2d7c318910c
document_version_independent_id: 296ea319-a839-9d79-9442-a2d7c318910c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-security-copilot-query-assistant.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-security-copilot-query-assistant
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-security-copilot-query-assistant.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: c2f6a3dc-053d-4c5b-30a6-f8b9f260a985
---

# Microsoft Security Copilot advanced hunting query assistant - Microsoft Defender XDR | Microsoft Learn

[Microsoft Security Copilot in Microsoft Defender](security-copilot-in-microsoft-365-defender) includes a query assistant feature for advanced hunting.

Threat hunters or security analysts who aren't familiar with or haven't learned Kusto query language (KQL) can make a request or ask a question in natural language (for example, *Get all alerts involving user admin123*). Security Copilot then generates a KQL query that matches the request by using the advanced hunting data schema.

The query assistant feature reduces the time it takes to write a hunting query from scratch, so threat hunters and security analysts can focus on hunting and investigating threats.

Users with access to Security Copilot can use the query assistant feature in advanced hunting.

Note

The advanced hunting capability is also available in the Security Copilot standalone experience through the Microsoft Defender XDR plugin. Know more about [preinstalled plugins in Security Copilot](/en-us/security-copilot/manage-plugins#preinstalled-plugins).

## Try your first request

To start using the Query assistant, follow these steps:

Note

Make sure that the Query assistant mode is active. [Get access to Security Copilot in advanced hunting](advanced-hunting-security-copilot#get-access)

1. Open the **Advanced hunting** page from the navigation bar in Microsoft Defender portal. The Security Copilot side pane for advanced hunting appears at the right hand side.

    [![Screenshot of the Copilot pane in advanced hunting.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-pane-big.png)](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-pane-big.png#lightbox)

    You can also reopen Copilot by selecting **Copilot** at the top of the query editor.
2. In the Copilot prompt bar, ask any threat hunting query that you want to run and press ![](media/advanced-hunting-security-copilot/send.png) or **Enter**.

    [![Screenshot that shows prompt bar in the Security Copilot for advanced hunting.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-query-big.png)](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-query-big.png#lightbox)
3. Copilot generates a KQL query from your text instruction or question. While Copilot is generating, you can cancel the query generation by selecting **Stop generating**.

    ![Screenshot of Security Copilot in advanced hunting showing generated query results with Add and run and Add to editor options.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-generate.png)
4. Review the generated query. To check how Copilot came up with the query, you can select **See the logic behind the query** below the query text to expand the explanation behind the query. Select **See the logic behind the query** again to minimize the explanation.

    ![Screenshot of Security Copilot option to see the logic behind the query.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-see-logic.png)

    You can then choose to run the query by selecting **Run query**.

    ![Screenshot of Security Copilot showing the Run query option.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-run-query.png)

    The generated query appears as the last query in the query editor and runs automatically.

    If you need to make further tweaks, select **Add to editor**.

    ![Screenshot of Security Copilot in advanced hunting showing the Add to editor option.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-add-editor.png)

    The generated query appears in the query editor as the last query, where you can edit it before running using the regular **Run query** above the query editor.
5. You can provide feedback about the generated response by selecting the feedback icon ![Screenshot of Security Copilot feedback option in advanced hunting.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-feedback-icon.png) and choosing **Looks right**, **Needs improvement**, or **Inappropriate**.

Tip

Providing feedback is an important way to let the Security Copilot team know how well the query assistant was able to help in generating a useful KQL query. Feel free to articulate what could make the query better, what adjustments you had to make before running the generated KQL query, or share the KQL query that you eventually used.

## Run or add the generated query

When the Threat Hunting Assistant generates a KQL query, select **Run query** to run it in advanced hunting.

To review or edit the query before running it, select the arrow next to **Run query**, then select **Add to editor**. The query is added to the query editor without running.

![Screenshot of the Run query split button in the Security Copilot side pane, showing the Add to editor option.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-settings.png)

To see how the query was constructed, select **See the logic behind the query**.