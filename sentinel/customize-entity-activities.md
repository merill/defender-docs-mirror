---
layout: Conceptual
title: Customize activities on Microsoft Sentinel entity timelines | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/customize-entity-activities
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
description: Add custom activities that Microsoft Sentinel displays on entity page timelines to highlight organization-specific events and context.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 362aebb9-7121-cb92-0de4-d496367f777d
document_version_independent_id: fc0ec9da-b584-22cd-068d-b52bafb3afab
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/customize-entity-activities.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/customize-entity-activities
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/customize-entity-activities.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 1fff6b5d-8b5e-52f6-e151-41b4b0d95f55
---

# Customize activities on Microsoft Sentinel entity timelines | Microsoft Learn

Important

- Activity customization is in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.
- After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](overview#changes-for-new-customers-starting-july-2025).If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).

## Overview of custom timeline activities

Microsoft Sentinel tracks and presents activities in entity timelines out-of-the-box. You can also create custom activities and have them appear on the timeline. Custom activities are based on queries of entity data from any connected data source. The following examples show how you might use this capability:

- Add new activities to the entity timeline by modifying existing out-of-the-box activity templates.
- Add new activities from custom logs. For example, from a physical access-control log, you can add a user's entry and exit activities for a particular restricted area—say, a server room—to the user's timeline.

## Open the activity customization page

To open the activity customization page, choose the tab that matches the portal you're using:

- Users of Microsoft Sentinel in the Azure portal, select the **Azure portal** tab below.
- Users of the Microsoft Defender portal, select the **Defender portal** tab.

# [Azure portal](#tab/azure)
Follow these steps in the Azure portal to open the activity customization page:

1. From the Microsoft Sentinel navigation menu, select **Entity behavior**.
2. On the **Entity behavior** page, select **Customize entity page (Preview)** at the top of the screen.

    ![Entity behavior page](media/customize-entity-activities/entity-behavior-blade.png)

# [Defender portal](#tab/defender)
Follow these steps in the Defender portal to customize activities for an entity:

1. In the Microsoft Defender portal, open any entity page.

    1. Select **Assets &gt; Devices** or **Identities**.
    2. Select a device or a user from the list. For a user, select **View user page** on the popup that appears.
2. On the entity page, select the **Sentinel events** tab.
3. On the **Sentinel events** tab, select **Customize Sentinel activities**. ![Screenshot of Defender entity page menu.](media/customize-entity-activities/identity-entity-page-defender.png)

---

On the **Customize Sentinel activities** page, you'll see a list of any activities you've created in the **My activities** tab. In the **Activity templates** tab, you'll see the collection of activities offered out-of-the-box by Microsoft security researchers. These are the activities that are already being tracked and displayed on the timelines in your entity pages.

- As long as you have not created any user-defined activities, your entity pages will display *all* the activities listed under the **Activity templates** tab.
- Once you create or customize an activity, your entity pages will display *only* those activities, which appear in the **My activities** tab.
- If you want to continue seeing the out-of-the-box activities in your entity pages, you must create an activity for each template you want to be tracked and displayed. Follow the instructions in Create an activity from a template.

## Create an activity from a template

Use the following steps to create a custom activity from an existing out-of-the-box template.

1. Select the **Activity templates** tab to see the various activities available by default. You can filter the list by entity type as well as by data source. Selecting an activity from the list will display the following information in the details pane:

    - A description of the activity
    - The data source that provides the events that make up the activity
    - The identifiers used to identify the entity in the raw data
    - The query that results in the detection of this activity
2. Select **Create activity** at the bottom of the details pane to start the activity creation wizard.

# [Azure portal](#tab/azure)
![Screenshot of activity template list in Azure portal.](media/customize-entity-activities/activity-details.png)

# [Defender portal](#tab/defender)
![Screenshot of activity template list in Defender portal.](media/customize-entity-activities/activity-details-defender.png)

When you select **Create activity** in the Defender portal, you are redirected to the Microsoft Sentinel activity wizard in the Azure portal in a new tab.

---
3. The **Activity wizard - Create new activity from template** will open, with its fields already populated from the template. You can make changes as you like in the **General** and **Activity configuration** tabs, or leave the prepopulated settings unchanged to continue viewing the out-of-the-box activity.
4. When you are satisfied, select the **Review and create** tab. When you see the **Validation passed** message, click the **Create** button at the bottom.

## Create an activity from scratch

From the top of the activities page, click on **Add activity** to start the activity creation wizard.

The **Activity wizard - Create new activity** will open, with its fields blank.

### Configure general activity settings

On the **General** tab, provide the basic metadata for the activity.

1. Enter a name for your activity (example: "user added to group").
2. Enter a description of the activity (example: "user group membership change based on Windows event ID 4728").
3. Select the type of entity (user or host) this query will track.
4. You can filter by additional parameters to help refine the query and optimize its performance. For example, you can filter for Active Directory users by choosing the **IsDomainJoined** parameter and setting the value to **True**.
5. You can select the initial status of the activity to **Enabled** or **Disabled**.
6. Select **Next : Activity configuration** to proceed to the next tab.

    ![Screenshot - Create a new activity](media/customize-entity-activities/create-new-activity.png)

### Configure the activity query and display settings

#### Writing the activity query

On the **Activity configuration** tab, write or paste the KQL query that will be used to detect the activity for the chosen entity, and determine how it will be represented in the timeline.

Important

We recommend that your query uses an [Advanced Security Information Model (ASIM) parser](normalization-about-parsers) and not a built-in table. This ensures that the query will support any current or future relevant data source rather than a single data source.

To correlate events and detect the custom activity, the KQL query requires several parameters that depend on the entity type. These parameters are the identifiers of the entity.

Use a strong identifier for one-to-one mapping between query results and the entity. A weak identifier might yield inaccurate results. [Learn more about entities and strong vs. weak identifiers](entities).

The following table provides information about the entities' identifiers.

**Strong identifiers for account and host entities**

At least one identifier is required in a query.

| Entity | Identifier | Description |
| --- | --- | --- |
| **Account** | Account\_Sid | The on-premises SID of the account in Active Directory |
|  | Account\_AadUserId | The Microsoft Entra object ID of the user in Microsoft Entra ID |
|  | Account\_Name + Account\_NTDomain | Similar to SamAccountName (example: Contoso\Joe) |
|  | Account\_Name + Account\_UPNSuffix | Similar to UserPrincipalName (example: Joe@Contoso.com) |
| **Host** | Host\_HostName + Host\_NTDomain | similar to fully qualified domain name (FQDN) |
|  | Host\_HostName + Host\_DnsDomain | similar to fully qualified domain name (FQDN) |
|  | Host\_NetBiosName + Host\_NTDomain | similar to fully qualified domain name (FQDN) |
|  | Host\_NetBiosName + Host\_DnsDomain | similar to fully qualified domain name (FQDN) |
|  | Host\_AzureID | the Microsoft Entra object ID of the host in Microsoft Entra ID (if Microsoft Entra domain joined) |
|  | Host\_OMSAgentID | the OMS Agent ID of the agent installed on a specific host (unique per host) |

Based on the entity type you selected on the **General** tab, you'll see the available identifiers. Select an identifier to paste it into the query at the cursor location.

Note

- The query can contain **up to 10 fields**, so you must project the fields you want.
- The projected fields must include the **TimeGenerated** field, in order to place the detected activity in the entity's timeline.

```kusto
SecurityEvent
| where EventID == "4728"
| where (SubjectUserSid == '{{Account_Sid}}' ) or (SubjectUserName == '{{Account_Name}}' and SubjectDomainName == '{{Account_NTDomain}}' )
| project TimeGenerated, SubjectUserName, MemberName, MemberSid, GroupName=TargetUserName
```

![Screenshot - Enter a query to detect the activity](media/customize-entity-activities/new-activity-query.png)

#### Presenting the activity in the timeline

For the sake of convenience, you may want to determine how the activity is presented in the timeline by adding dynamic parameters to the activity output.

Microsoft Sentinel provides built-in parameters for you to use, and you can also use others based on the fields you projected in the query.

Use the following format for your parameters: `{{ParameterName}}`

After the activity query passes validation and displays the **View query results** link below the query window, you'll be able to expand the **Available values** section to view the parameters available for you to use when creating a dynamic activity title.

Select the **Copy** icon next to a specific parameter to copy that parameter to your clipboard so that you can paste it into the **Activity title** field above.

Add any of the following parameters to your query:

- Any field you projected in the query.
- Entity identifiers of any entities mentioned in the query.
- `StartTimeUTC`, to add the start time of the activity, in UTC time.
- `EndTimeUTC`, to add the end time of the activity, in UTC time.
- `Count`, to summarize several KQL query outputs into a single output.

    The `count` parameter adds the following command to your query in the background, even though it's not displayed fully in the editor:

    ```kusto
    Summarize count() by <each parameter you’ve projected in the activity>
    ```

    Then, when you use the **Bucket Size** filter in the entity pages, the following command is also added to the query that's run in the background:

    ```kusto
    Summarize count() by <each parameter you’ve projected in the activity>, bin (TimeGenerated, Bucket in Hours)
    ```

The following example shows an activity title that uses dynamic parameters:

![Screenshot - See the available values for your activity title](media/customize-entity-activities/new-activity-title.png)

When you are satisfied with your query and activity title, select **Next : Review**.

See more information about the KQL operators and functions used in the activity query samples, in the Kusto documentation:

- [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***project*** operator](/en-us/kusto/query/project-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***summarize*** operator](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***bin()*** function](/en-us/kusto/query/bin-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***count()*** aggregation function](/en-us/kusto/query/count-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)

For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

Other resources:

- [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
- [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)

### Review settings and create the activity

Use the **Review and create** tab to validate your configuration and finalize the activity.

1. Verify all the configuration information of your custom activity.
2. When the **Validation passed** message appears, click **Create** to create the activity. You can edit or change it later in the **My Activities** tab.

## Manage your activities

Manage your custom activities from the **My Activities** tab. Click on the ellipsis (...) at the end of an activity's row to:

- Edit the activity.
- Duplicate the activity to create a new, slightly different one.
- Delete the activity.
- Disable the activity (without deleting it).

## View activities in an entity page

Whenever you enter an entity page, all the enabled activity queries for that entity will run, providing you with up-to-the-minute information in the entity timeline. You'll see the activities in the timeline, alongside alerts and bookmarks.

You can use the **Timeline content** filter to present only activities (or any combination of activities, alerts, and bookmarks).

You can also use the **Activities** filter to present or hide specific activities.