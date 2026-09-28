---
layout: Conceptual
title: Create and edit workbooks with Copilot for ISOC in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-copilot-workbooks
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use Copilot for Workbooks with ISOC in Microsoft Defender to create and edit workbooks by using natural-language prompts.
ms.service: microsoft-defender
author: mberdugo
ms.author: monaberdugo
ms.date: 2026-09-02T00:00:00.0000000Z
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: how-to
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 92cee3a1-1491-a9ac-ed73-ac0a6df4b3cf
document_version_independent_id: 92cee3a1-1491-a9ac-ed73-ac0a6df4b3cf
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-copilot-workbooks.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-copilot-workbooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-copilot-workbooks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 5b70a9db-b316-f1a6-589f-5faad6affba0
---

# Create and edit workbooks with Copilot for ISOC in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Use Copilot for Workbooks with Integrated Security Operations Center (ISOC) in Microsoft Defender to create and edit workbooks by using natural-language prompts. Describe the dashboard you want, and Copilot generates the KQL, panels, parameters, and layout.

You can review the generated workbook, refine it conversationally, and save the finished workbook. You can also use the Advanced Editor to manually update generated KQL.

## Prerequisites

Before you begin, make sure the following requirements are met:

- Your tenant is [eligible for ISOC](isoc-overview).
- Microsoft Security Copilot is enabled for your tenant and has available Security Compute Units (SCUs).
- You have permission to create and save workbooks in Microsoft Defender.

Note

During this preview, Copilot for Workbooks supports Advanced Hunting tables as the data source. Log Analytics data isn't supported.

## Create a workbook with Copilot

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Go to **Workbooks**.
3. Select **Add Workbook**.
4. Select **Edit** &gt; **Edit with Copilot**.

    [![Screenshot of the Copilot panel in a Microsoft Defender workbook showing example natural-language prompts for generating workbook content.](media/defender-copilot-workbooks/copilot-workbooks-prompt-examples.png)](media/defender-copilot-workbooks/copilot-workbooks-prompt-examples.png#lightbox)
5. In the Copilot panel, describe the dashboard you want to create.
6. Submit the prompt.

    Copilot generates a draft workbook on the canvas. The draft can include a descriptive header, parameters, and one or more visualizations.

    [![Screenshot of a Microsoft Defender workbook generated with Copilot showing an endpoint investigation dashboard with charts and the Copilot panel.](media/defender-copilot-workbooks/copilot-workbooks-generated-dashboard.png)](media/defender-copilot-workbooks/copilot-workbooks-generated-dashboard.png#lightbox)
7. Review the generated workbook.
8. Refine the workbook as needed.
9. Save the workbook.

## Refine a workbook with Copilot

After Copilot generates a workbook, continue the conversation to update specific parts of the workbook.

1. In the Copilot panel, describe the change you want to make.

    For example:

    - `Group by tenant.`
    - `Add a stat card with the total volume.`
    - `Turn this into a bar chart.`
    - `Filter to Windows devices only.`
2. Submit the prompt.

    Copilot updates the workbook based on your request.
3. Review the updated workbook.
4. Continue refining the workbook as needed.

Copilot updates the workbook as you continue the conversation.

## Review and undo workbook changes

Copilot automatically updates the workbook based on your prompts. You can use **Undo** or **Redo** as you refine the workbook.

| Action | Description |
| --- | --- |
| **Undo** | Reverts the most recent Copilot change. |
| **Redo** | Restores a change that you previously undid. |
| **Save** | Saves the workbook to your account. |
| **Advanced Editor** | Opens the workbook definition and KQL for manual editing. |

Tip

Make changes incrementally so that you can use **Undo** and **Redo** predictably as you refine the workbook.

## Edit generated KQL manually

You can manually edit Copilot-generated KQL by using the workbook Advanced Editor.

1. Open the workbook panel you want to modify.
2. Open the **Advanced Editor**.
3. Review the generated KQL.
4. Make the required changes.
5. Apply the changes to the workbook.

## Prompting tips

Use the following guidance when creating or refining a workbook:

- Describe the goal of the dashboard instead of providing only a query.
- Specify a time range, such as `last 24 hours` or `last 7 days`.
- Specify the visualization you want, such as a table, bar chart, time series, stat card, or map.
- Make changes in small steps and review each update before requesting another change.
- Mention the relevant Advanced Hunting table when you know which table contains the data.

For example:

> 
> Dashboard of the top 10 signed-in users with failed sign-ins in the last 24 hours.

Or:

> 
> Timeline of Defender for Endpoint alerts by severity, grouped by device.

## Troubleshoot Copilot for Workbooks

### Edit with Copilot isn't shown

1. Verify that Microsoft Security Copilot is provisioned for your tenant.
2. Verify that Security Compute Units are available.
3. Return to the Workbooks page.
4. Refresh the page.

### A generated workbook doesn't return results

1. Check the time-range parameter.
2. Increase the time range if needed.
3. Verify that the Advanced Hunting tables referenced by the generated query contain data for your tenant.
4. Run the underlying query in Advanced Hunting to verify that it returns results.
5. If needed, ask Copilot to explain why the panel is empty and suggest a correction.

### A visualization doesn't display the expected results

Describe the specific change you want Copilot to make.

For example:

- `Show only the top 10 results.`
- `Change this to a stacked bar chart.`
- `Group the results by day.`

If the change doesn't produce the expected result, use **Undo** to revert it.