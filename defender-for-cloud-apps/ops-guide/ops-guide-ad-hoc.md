---
layout: Conceptual
title: Ad-hoc operational guide - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/ops-guide/ops-guide-ad-hoc
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article provides ad-hoc operational recommendations to help security operations teams to plan and run security activities.
ms.date: 2023-12-17T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 8db11bac-6c56-f2b7-baf7-6eacf93e5aaa
document_version_independent_id: 8db11bac-6c56-f2b7-baf7-6eacf93e5aaa
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/ops-guide/ops-guide-ad-hoc.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ops-guide/ops-guide-ad-hoc
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/ops-guide/ops-guide-ad-hoc.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/c4c18c0c-090d-4c28-a4be-9e6214a0c4fb
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b22d517c-92cf-4ee3-8dca-36c6cd062217
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: e14e4e23-6730-d120-c9ff-4cf0480a779d
---

# Ad-hoc operational guide - Microsoft Defender for Cloud Apps | Microsoft Learn

This article lists monthly operational activities that we recommend you perform with Microsoft Defender for Cloud Apps.

Monthly activities can be performed more frequently or as needed, depending on your environment and needs.

## Review Microsoft service health

**Where**: Check the following locations:

- In the Microsoft 365 admin center, select **Health &gt; Service health**
- [Microsoft 365 Service health status](https://status.office365.com/)
- X: https://twitter.com/MSFT365status

If you're experiencing issues with a cloud service, we recommend checking service health updates to determine whether it's a known issue, with a resolution in progress, before you call support or spend time troubleshooting.

## Run advanced hunting queries

**Where**: In the Microsoft Defender portal at https://security.microsoft.com, select **Hunting &gt; Advanced hunting** and query for Defender for Cloud Apps data.

**Persona**: SOC analysts

Similar to reviewing activity logs, advanced hunting can be used as a scheduled activity, using custom detections or ad-hoc queries to proactively hunt for threats.

Advanced hunting is a unified tool that allows you to hunt for threats in Microsoft Defender. We recommend that you save frequently used queries for faster manual threat hunting and remediation.

The following sample queries are useful when querying for Defender for Cloud Apps data:

### Search for *Office - FileDownloaded Events* records

```kusto
CloudAppEvents
| where ActionType == "FileDownloaded"
| extend FileName = RawEventData.SourceFileName, Site = RawEventData.SiteUrl, FileLabel = RawEventData.SensitivityLabelId, SiteLabel = RawEventData.SiteSensitivityLabelId
| project Timestamp,AccountObjectId,ActionType,Application,FileName,Site,FileLabel,SiteLabel
```

### Search for *Office - MailItemsAccessed Details* records

```kusto
CloudAppEvents
| where ActionType == "MailItemsAccessed" //Defines the action type we want to filter on 16
| extend Folders = RawEventData.Folders[0] //Set variable and then use the index to trim the [] to data can be accessed
| extend MailboxPath = Folders.Path //set a variable for the path
| mv-expand Folders.FolderItems //expand the list of items because some entries might contain multiple items which were accessed
| extend MessageIDs = tostring(Folders_FolderItems.InternetMessageId) //extend and then convert to string so table can be joined
| join EmailEvents on $left.MessageIDs == $right.InternetMessageId //join the email events table to access subject and mailbox information
| project Timestamp,AccountType,AccountDisplayName,AccountObjectId,UserAgent,IPAddress,CountryCode,City,ISP,NetworkMessageId,MailboxPath,Subject,SenderFromAddress,RecipientEmailAddress
| sort by Timestamp desc
```

### Search for *Extract activity objects* records

```kusto
CloudAppEvents
| take 100
| mv-expand(ActivityObjects)
| evaluate bag_unpack(ActivityObjects)
```

### Search for *Microsoft Entra ID - Add to Role* records

```kusto
CloudAppEvents
| where ActionType in ("Add member to role.") 
| extend FirstElement = ActivityObjects[0], SecondElement = ActivityObjects[1], ThirdElement = ActivityObjects[2]
| extend Type = FirstElement.ServiceObjectType, RoleName = FirstElement.Name,  UserAddedName = SecondElement.Name, UserAddedId = SecondElement.Id
| project Timestamp,Type,ActionType,RoleName,UserAddedName,UserAddedId,AccountId,Account DisplayName
```

### Search for *Microsoft Entra ID - Group Adds* records

```kusto
CloudAppEvents
| where ActionType in ("Add member to group.") and AccountType == "Regular"
| extend SecondElement = RawEventData.ModifiedProperties[1]
| extend UserAddedId = RawEventData.ObjectId, GroupName = 
SecondElement.NewValue
| project Timestamp, ActionType,UserAddedId,PerformedBy = 
AccountDisplayName,GroupName
```

## Review file quarantines

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select **Cloud apps &gt; Files**. Query for items where **Quarantined** = **True**.

**Persona**: Compliance administrators

Use Defender for Cloud Apps to detect unwanted files that are stored in your cloud and leave you vulnerable. Take immediate action to stop them in their tracks by using the Admin quarantine to lock down the files that pose a threat. Admin quarantine can help you protect files in the cloud, remediate problems, and prevent future leaks from occurring.

Files in Admin quarantine might be reviewed as part of an alert investigation, and you might be required to manage quarantined files for governance and compliance reasons.

For more information, see [Understand how quarantine works](../use-case-admin-quarantine#understand-how-quarantine-works).

## Review app risk scores

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select **Cloud apps &gt; Cloud app catalog**.

**Persona**: Compliance administrators

The cloud app catalog rates risk for your cloud apps based on regulatory certification, industry standards, and best practices. We recommend reviewing the score for each of the apps in your environment to make sure it aligns with your company regulations.

After checking an app's risk score, you might want to submit a request to change the score, or customize the risk score in **Cloud Discovery &gt; Score metrics**.

For more information, see [Find your cloud app and calculate risk scores](../risk-score).

## Delete cloud discovery data

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select **Settings &gt; Cloud apps &gt; Cloud Discovery &gt; Delete Data**.

**Persona**: Compliance administrators

We recommend deleting cloud discovery data in the following scenarios:

- If you have older, manually uploaded log files and you don't want old data affecting your results.
- When you want a new custom data view to include events in all log file data, including older files. Custom data views only apply to new data available from that point onward, so we recommend deleting any old data and uploading it again to include it in custom data views.
- When many users or IP addresses started working again after being offline for some time, delete old data to prevent the new activity from being identified as anomalous, with false positive violations.

For more information, see [Deleting cloud discovery data](../discovered-apps#deleting-cloud-discovery-data).

## Generate a cloud discovery executive report

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select **Cloud apps &gt; Cloud discovery &gt; Dashboard &gt; Actions**

**Persona**: Compliance administrators

We recommend using a cloud discovery executive report to get an overview of Shadow IT used across your organization. cloud discovery executive reports identify the top potential risks and help you plan a workflow to mitigate and manage risks until they're resolved.

For more information, see [Generate cloud discovery executive report](../discovered-apps#generate-a-cloud-discovery-executive-report).

## Generate a cloud discovery snapshot report

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select **Cloud apps &gt; Cloud discovery &gt; Dashboard &gt; Actions**

**Persona**: Security and Compliance administrators

If you don't have a log yet and want to see a sample of what one might look like, download a sample log file.

For more information, see [Create snapshot cloud discovery reports](../create-snapshot-cloud-discovery-reports).