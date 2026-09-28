---
layout: Conceptual
title: Create your own incidents manually in Microsoft Sentinel in the Azure portal | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/create-incident-manually
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
description: Manually create incidents in Microsoft Sentinel based on data or information received by the SOC through alternate means or channels.
ms.author: guywild
author: guywi-ms
ms.reviewer: idpelleg
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: e7d65f5e-1cfe-7f6e-b380-ed385f4a894d
document_version_independent_id: f7dccacb-c152-864b-b327-7dfd85ff017d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/create-incident-manually.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/create-incident-manually
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/create-incident-manually.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 482699f6-7657-2267-4245-e7a20ad66bb5
---

# Create your own incidents manually in Microsoft Sentinel in the Azure portal | Microsoft Learn

Important

Manual incident creation, using the portal or Logic Apps, is currently in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

Manual incident creation is generally available using the API.

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](overview#changes-for-new-customers-starting-july-2025).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).

With Microsoft Sentinel as your security information and event management (SIEM) solution, your security operations' threat detection and response activities are centered on **incidents** that you investigate and remediate. These incidents have two main sources:

- They're generated automatically when detection mechanisms operate on the logs and alerts that Microsoft Sentinel ingests from its connected data sources.
- They're ingested directly from other connected Microsoft security services (such as [Microsoft Defender XDR](microsoft-365-defender-sentinel-integration)) that created them.

However, threat data can also come from other sources *not ingested into Microsoft Sentinel*, or events not recorded in any log, and yet can justify opening an investigation. For example, an employee might notice an unrecognized person engaging in suspicious activity related to your organization’s information assets. This employee might call or email the security operations center (SOC) to report the activity.

Microsoft Sentinel in the Azure portal allows your security analysts to manually create incidents for any type of event, regardless of its source or data, so you don't miss out on investigating these unusual types of threats.

## Common use cases

### Create an incident for a reported event

Use this option when a user, employee, or analyst reports suspicious activity that was not ingested as telemetry into Microsoft Sentinel. For example, an employee might notice an unrecognized person engaging in suspicious activity related to your organization's information assets and report it to the security operations center (SOC) by phone or email.

### Create incidents out of events from external systems

Create incidents based on events from systems whose logs are not ingested into Microsoft Sentinel. For example, an SMS-based phishing campaign might use your organization's corporate branding and themes to target employees' personal mobile devices. You may want to investigate such an attack, and you can create an incident in Microsoft Sentinel so that you have a platform to manage your investigation, to collect and log evidence, and to record your response and mitigation actions.

### Create incidents based on hunting results

Create incidents based on the observed results of hunting activities. For example, while threat hunting in the context of a particular investigation (or on your own), you might come across evidence of a completely unrelated threat that warrants its own separate investigation.

## Manually create an incident

There are three ways to create an incident manually:

- Create an incident using the Azure portal
- Create an incident using Azure Logic Apps, using the Microsoft Sentinel Incident trigger.
- Create an incident using the Microsoft Sentinel API, through the [Incidents](/en-us/rest/api/securityinsights/preview/incidents) operation group. The Incidents operation group allows you to get, create, update, and delete incidents.

After onboarding Microsoft Sentinel to the Microsoft Defender portal, manually created incidents aren't synchronized with the Defender portal, though they can still be viewed and managed in Microsoft Sentinel in the Azure portal, and through Logic Apps and the API.

### Permissions

The following roles and permissions are required to manually create an incident.

| Method | Required role |
| --- | --- |
| Azure portal and API | One of the following:- [Microsoft Sentinel Responder](/en-us/azure/role-based-access-control/built-in-roles/security#microsoft-sentinel-responder)<br>- [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles/security#microsoft-sentinel-contributor) |
| Azure Logic Apps | One of the above, plus:- [Microsoft Sentinel Playbook Operator](/en-us/azure/role-based-access-control/built-in-roles/security#microsoft-sentinel-playbook-operator) to use an existing playbook<br>- [Logic App Contributor](/en-us/azure/role-based-access-control/built-in-roles/integration#logic-app-contributor) to create a new playbook |

Learn more about [Microsoft Sentinel roles and permissions](roles).

### Create an incident using the Azure portal

To manually create an incident in the Azure portal, follow these steps:

1. Select **Microsoft Sentinel** and choose your workspace.
2. From the Microsoft Sentinel navigation menu, select **Incidents**.
3. On the **Incidents** page, select **+ Create incident (Preview)** from the button bar.

    [![Screenshot of main incident screen, locating the button to create a new incident manually.](media/create-incident-manually/create-incident-main-page.png)](media/create-incident-manually/create-incident-main-page.png#lightbox)

    The **Create incident (Preview)** panel will open on the right side of the screen.

    ![Screenshot of manual incident creation panel, all fields blank.](media/create-incident-manually/create-incident-panel.png)
4. Fill in the fields in the panel accordingly.

    - **Title**

        - Enter a title of your choosing for the incident. The incident will appear in the queue with this title.
        - Required. Free text of unlimited length. Spaces will be trimmed.
    - **Description**

        - Enter descriptive information about the incident, including details such as the origin of the incident, any entities involved, relation to other events, who was informed, and so on.
        - Optional. Free text up to 5000 characters.
    - **Severity**

        - Choose a severity from the drop-down list. All Microsoft Sentinel-supported severities are available.
        - Required. Defaults to "Medium."
    - **Status**

        - Choose a status from the drop-down list. All Microsoft Sentinel-supported statuses are available.
        - Required. Defaults to "New."
        - You can create an incident with a status of "closed," and then open it manually afterward to make changes and choose a different status. Choosing "closed" from the drop-down will activate **classification reason** fields for you to choose a reason for closing the incident and add comments. ![Screenshot of classification reason fields for closing an incident.](media/create-incident-manually/classification-reason.png)
    - **Owner**

        - Choose from the available users or groups in your tenant. Begin typing a name to search for users and groups. Select the field (click or tap) to display a list of suggestions. Choose "assign to me" at the top of the list to assign the incident to yourself.
        - Optional.
    - **Tags**

        - Use tags to classify incidents and to filter and locate them in the queue.
        - Create tags by selecting the **plus sign icon**, entering text in the dialog box, and selecting **OK**. Auto-completion will suggest tags used within the workspace over the prior two weeks.
        - Optional. Free text.
5. Select **Create** at the bottom of the panel. After a few seconds, the incident will be created and will appear in the incidents queue.

    If you assign an incident a status of "Closed," it will not appear in the queue until you change the **status** filter to show closed incidents as well. The filter is set by default to display only incidents with a status of "New" or "Active."

Select the incident in the queue to see its full details, add bookmarks, change its owner and status, and more.

If for some reason you change your mind after the fact about creating the incident, you can [delete the incident](delete-incident) from the queue grid, or from within the incident itself. You must have the [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles/security#microsoft-sentinel-contributor) role in order to delete an incident.

### Create an incident using Azure Logic Apps

Creating an incident is also available as a Logic Apps action in the Microsoft Sentinel connector, and therefore in Microsoft Sentinel [playbooks](tutorial-respond-threats-playbook).

You can find the **Create incident (preview)** action in the playbook schema for the incident trigger.

![Screenshot of create incident logic app action in Microsoft Sentinel connector.](media/create-incident-manually/create-incident-logicapp-action.png)

You need to supply parameters as described below:

- Select your **Subscription**, **Resource group**, and **Workspace name** from their respective drop-downs.
- For the remaining fields, see the field explanations in Create an incident using the Azure portal.

    ![Screenshot of create incident action parameters in Microsoft Sentinel connector.](media/create-incident-manually/create-incident-logicapp-parameters.png)

Microsoft Sentinel supplies some sample playbook templates that show you how to work with this capability:

- **Create incident with Microsoft Form**
- **Create incident from shared email inbox**

You can find them in the playbook templates gallery on the Microsoft Sentinel **Automation** page.

### Create an incident using the Microsoft Sentinel API

The [Incidents](/en-us/rest/api/securityinsights/preview/incidents) operation group allows you not only to create, but also to [update an incident](/en-us/rest/api/securityinsights/preview/incidents/create-or-update), [retrieve an incident](/en-us/rest/api/securityinsights/preview/incidents/get), [list incidents](/en-us/rest/api/securityinsights/preview/incidents/list), and [delete an incident](/en-us/rest/api/securityinsights/preview/incidents/delete).

To create or update a Microsoft Sentinel incident through the REST API, send a `PUT` request to the following endpoint. If the specified incident ID doesn't already exist, the API creates a new incident. After the request completes successfully, the incident is visible in the incident queue in the portal.

```http
PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.OperationalInsights/workspaces/{workspaceName}/providers/Microsoft.SecurityInsights/incidents/{incidentId}?api-version=2022-07-01-preview
```

The following example shows a JSON request body that creates an incident with properties such as title, description, severity, owner, status, and classification:

```json
{
  "etag": "\"0300bf09-0000-0000-0000-5c37296e0000\"",
  "properties": {
    "lastActivityTimeUtc": "2019-01-01T13:05:30Z",
    "firstActivityTimeUtc": "2019-01-01T13:00:30Z",
    "description": "This is a demo incident",
    "title": "My incident",
    "owner": {
      "objectId": "aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
    },
    "severity": "High",
    "classification": "FalsePositive",
    "classificationComment": "Not a malicious activity",
    "classificationReason": "IncorrectAlertLogic",
    "status": "Closed"
  }
}
```

## Notes

Keep the following limitations and behaviors in mind for manually created incidents:

- Incidents created manually do not contain any entities or alerts. Therefore, the **Alerts** tab in the incident page will remain empty until you [relate existing alerts to your incident](relate-alerts-to-incidents).

    The **Entities** tab will also remain empty, as adding entities *directly* to manually created incidents is not currently supported. (If you relate an alert to this incident, entities from the alert will appear in the incident.)
- Manually created incidents will also not display any **Product name** in the queue.
- The incidents queue is filtered by default to display only incidents with a status of "New" or "Active." If you create an incident with a status of "Closed," it will not appear in the queue until you change the status filter to show closed incidents as well.