---
layout: Conceptual
title: Delete incidents in Microsoft Sentinel in the Azure portal | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/delete-incident
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Delete incidents in Microsoft Sentinel from the Azure portal or through the API, with guidance on when deletion is appropriate.
ms.author: guywild
author: guywi-ms
ms.reviewer: idpelleg
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 8f8d8af2-f569-f0a4-7cbb-f4298793130c
document_version_independent_id: 3240d1d7-26cb-8a94-7042-8aa7485f032f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/delete-incident.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/delete-incident
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/delete-incident.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 8234ff7d-343d-84de-0fd9-7d455a215e54
---

# Delete incidents in Microsoft Sentinel in the Azure portal | Microsoft Learn

Important

Incident deletion using the portal is currently in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

Incident deletion is generally available through the API.

The ability to create incidents from scratch in Microsoft Sentinel in the Azure portal opens the possibility that you'll create an incident that you later decide you shouldn't have. For example, you may have created an incident based on an employee report, before having received any evidence (such as alerts), and soon afterward you receive alerts that automatically generate the incident in question. But now, you have a duplicate incident with no data in it. In this scenario, you can delete your duplicate incident right from the incident queue in the Azure portal.

**Deleting an incident is not a substitute for closing an incident!** Deleting an incident should only be done when at least one of the following conditions is met:

- The incident was created manually by mistake.
- The incident exactly duplicates another incident.
- Faulty incidents were generated in bulk by a broken analytics rule.
- The incident contains no data - alerts, entities, bookmarks, and so on.

In all other cases, when an incident is no longer needed, it should be **closed**, not deleted. [Closing an incident](incident-navigate-triage#close-an-incident) requires you to specify the reason for closing it, and allows you to add additional comments for context and clarification. Closing old incidents in this way preserves the transparency and integrity of your SOC, and also allows for the possibility of reopening the incident if the problem resurfaces.

## Delete an incident using the Azure portal

You can delete one or more incidents directly from the Azure portal incident queue.

**To delete a single incident:**

1. From the Microsoft Sentinel navigation menu, select **Incidents**.
2. On the **Incidents** page, select the incident you want to delete.
3. Select **View full details** in the details pane to enter the incident's full details view.
4. Select **Delete incident** from the button bar at the top. ![Screenshot of deleting incident from details screen.](media/delete-incident/delete-incident-from-details-screen.png)
5. Answer **Yes** to the confirmation prompt that appears. ![Screenshot of single incident deletion confirmation dialog.](media/delete-incident/delete-incident-confirm.png)

Alternatively, you can delete a single incident from the incident queue by selecting only one checkbox and using the multi-delete flow described in the "To delete multiple incidents" procedure.

**To delete multiple incidents:**

1. From the Microsoft Sentinel navigation menu, select **Incidents**.
2. On the **Incidents** page, select the incident or incidents you want to delete, by marking the checkboxes next to each one in the incidents grid.
3. Select **Delete** from the button bar. ![Screenshot of deleting multiple incidents from incident queue.](media/delete-incident/delete-multiple-incidents-from-queue.png)
4. Answer **Yes** to the confirmation prompt that appears. ![Screenshot of multiple-incident-deletion confirmation dialog.](media/delete-incident/delete-multiple-incidents-confirm.png)

## Delete an incident using the Microsoft Sentinel API

The [Incidents](/en-us/rest/api/securityinsights/preview/incidents) operation group allows you to delete incidents as well as to [create and update (edit)](/en-us/rest/api/securityinsights/preview/incidents/create-or-update), [get (retrieve)](/en-us/rest/api/securityinsights/preview/incidents/get), and [list incidents](/en-us/rest/api/securityinsights/preview/incidents/list).

You [delete an incident](/en-us/rest/api/securityinsights/preview/incidents/delete) by sending a `DELETE` request to the following endpoint, specifying the target incident by its incident ID. After this request is made, the incident will no longer be visible in the incident queue in the portal.

Use this request to delete an existing incident from a Microsoft Sentinel workspace by incident ID:

```http
DELETE https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.OperationalInsights/workspaces/{workspaceName}/providers/Microsoft.SecurityInsights/incidents/{incidentId}?api-version=2022-07-01-preview
```

## Notes

- To delete an incident, you must have the [**Microsoft Sentinel Contributor**](roles) role.
- Deleting an incident is not reversible! After you delete an incident, the only reference to it will be the audit data in the *SecurityIncident* table in the Logs screen. (See the [table's schema documentation in Log Analytics](/en-us/azure/azure-monitor/reference/tables/securityincident)). The *Status* field in that table will be updated to "Deleted" for that incident.

    Note

    Due to the 64 KB limit of the record size in the *SecurityIncident* table, incident comments may be truncated (beginning from the earliest) if the limit is exceeded.
- You can't delete incidents from within Microsoft Sentinel that were [imported from and synchronized with Microsoft Defender XDR](microsoft-365-defender-sentinel-integration).
- If an alert [related to a deleted incident](relate-alerts-to-incidents) gets updated, or if a new alert is grouped under a deleted incident, a new incident will be created to replace the deleted one.