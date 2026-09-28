---
layout: Conceptual
title: Details and results of AIR in Defender for Office 365 Plan 2 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/air-view-investigation-results
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: article
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
description: Learn about the information that's available from automated investigation and response (AIR) in Microsoft Defender for Office 365 Plan 2.
ms.date: 2024-07-10T00:00:00.0000000Z
ms.service: defender-office-365
ms.custom: sfi-image-nochange
locale: en-us
document_id: 9e335e07-6102-48e6-6c44-b0d647243828
document_version_independent_id: 9e335e07-6102-48e6-6c44-b0d647243828
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/air-view-investigation-results.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: air-view-investigation-results
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/air-view-investigation-results.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 5bfdd4fb-8fa5-7fca-c277-5cdbeedb1a80
---

# Details and results of AIR in Defender for Office 365 Plan 2 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In Microsoft 365 organizations with [Microsoft Defender for Office 365 Plan 2](mdo-about#defender-for-office-365-plan-2-capabilities), details about active and completed investigations from [automated investigation and response (AIR) in Defender for Office 365](air-about) are available on the **Investigations** page in the Microsoft Defender portal at https://security.microsoft.com/airinvestigation. Investigation details provide you with up-to-date status and (with the right permissions) the ability to approve any pending actions.

Tip

AIR details and results are also available in Microsoft Defender XDR on the **Investigations** page at https://security.microsoft.com/incidents. For more information, see [Unified investigation page](/en-us/defender-xdr/m365d-autoir-results#new-unified-investigation-page).

## What do you need to know before you begin?

- To see the permissions and licensing requirement for AIR, see [Required permissions and licensing for AIR](air-about#required-permissions-and-licensing-for-air).
- Email counts are calculated at the time of the investigation. Some counts are recalculated when you open investigation flyouts (based on the underlying query).

    The following email count values are calculated at the time of investigation and don't change:

    - Email clusters on the **Email** tab.
    - The email quantity value shown on the email clusters flyout.

    The following email count values reflect email messages that were received after the initial analysis of the investigation:

    - The email count shown at the bottom of the **Email** tab of the email clusters flyout.
    - The email count shown in Explorer (Threat Explorer)

        For example, an email cluster that shows an original quantity of 10 messages shows an email list total of 15 if five more messages arrive between the investigation analysis phase and when an admin reviews the investigation. Likewise, old investigations might show higher message counts than Threat Explorer queries, because data in Microsoft Defender for Office 365 Plan 2 expires seven days after the end of a trial and 30 days later for paid licenses.

        Historical and current email message counts are shown in different views to give the following information:

        - The email effect at the time of investigation.
        - The current email effect up to when the remediation is run.
- For email, you might see a volume anomaly threat as part of the investigation. A *volume anomaly* indicates a spike in similar email messages around the investigation event time compared to earlier times. A spike in email traffic together with similarity in certain message properties (for example, subject, message body, sender domain, and sender IP) typically indicates the beginning of email attacks. But bulk email, spam, and legitimate email campaigns commonly share these same message properties.

## Investigations from AIR in Defender for Office 365 Plan 2

In the Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Investigations**. Or, to go directly to the **Investigations** page, use https://security.microsoft.com/airinvestigation.

By default, investigation details from yesterday and today are shown, but you can change the date range.

The following information shown on the **Investigations** page. You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. By default, all available columns are selected:

- **ID**: The unique ID of the investigation. Select ![](media/defender-portal-icon-copy.png)**Open in new window** to open the details of the investigation as described in the View investigation details section.
- **Status**: The available status values are described in the Investigation Status values section.
- **Detection Source**: This value is always **Office365**.
- **Investigation**
- **Users**
- **Creation Time**
- **Last Changed Time**
- **Threat count**
- **Action count**
- **Duration of investigation**

To filter the entries, select ![](media/defender-portal-icon-filter.png)**Filter**. The following filters are available in the **Filter** flyout that opens:

- **Investigation type**section: Select one or more of the following values:
    - **Manual investigation**
    - **User-reported messages**
    - **Zapped File**
    - **Zapped URL**
    - **URL verdict change**
    - **User compromised**
- **Time range** section: Select **Start date** and **End date** values. Data is available for the last 72 days.
- **Status** section: Select one or more of the following values described in the Investigation Status valuessection:
    - **Starting**
    - **Running**
    - **No Threats Found**
    - **Terminated by System**
    - **Pending Action**
    - **Threats Found**
    - **Remediated**
    - **Partially Remediated**
    - **Terminated by User**
    - **Failed**
    - **Queued by Throttling**
    - **Terminated by Throttling**

When you're finished in the **Filter** flyout, select **Apply**. To clear the filters, select ![](media/defender-portal-icon-clear-filters.png)**Clear filters**.

Use the ![](media/defender-portal-icon-search.png)**Search** box to find information on the page. Type text in the box and then press the ENTER key.

Use ![](media/defender-portal-icon-download.png)**Export** to save the visible information to a CSV file. The default filename is Investigations - Microsoft Defender.csv, and the default location is the local Downloads folder. If an exported report already exists in that location, the filename is incremented (for example, Investigations - Microsoft Defender (1).csv).

### Investigation Status values

The **Status** values of an investigation indicate the progress of the analysis and actions. As the investigation runs, the **Status** value is updated to indicate whether threats were found, and whether actions have been approved.

The **Status** values that are used in investigations are described in the following list:

- **Failed**: At least one investigation analyzer ran into a problem where it couldn't complete properly.

    If an investigation fails after remediation actions were approved, the remediation actions might still have succeeded. For more information, view the investigation details.
- **No Threats Found**: The investigation finished and no threats were identified (compromised user accounts, email messages, URLs, or files).

    If you suspect something malicious was missed (a false negative), you can take action using [Threat Explorer (Explorer)](threat-explorer-real-time-detections-about).
- **Partially Investigated** (formerly known as **Threats found**): The automated investigation found issues, but without specific remediation actions to resolve the issues. Occurs when some type of user activity was identified, but no cleanup actions are available. Examples include any of the following user activities:

    - A [data loss prevention (DLP)](/en-us/purview/dlp-learn-about-dlp) event.
    - An email sending anomaly.
    - Sent malware.
    - Sent phishing.
    - The investigation found nothing to do. For example:
        - No malicious URLs, files, or email messages to remediate.
        - No mailbox activity to fix (for example, turn off forwarding rules or delegation).

    If you suspect something malicious was missed (a false negative), you can take action using [Threat Explorer (Explorer)](threat-explorer-real-time-detections-about).
- **Partially Remediated**: The investigation resulted in remediation actions, and some were approved and completed. Other actions are still [pending approval](air-review-approve-pending-completed-actions).
- **Pending Action**: The investigation found a threat (for example, a malicious email, a malicious URL, or a risky mailbox setting), and an action to remediate the threat is [awaiting approval](air-review-approve-pending-completed-actions).

    The list of pending actions can increase as an investigation runs. View the investigation details to see if other items are still pending completion.
- **Queued By Throttling**: An investigation is being held in a queue. When other investigations complete, queued investigations begin. Throttling helps avoid poor service performance.

    Pending actions can limit how many new investigations can run. Make sure to [approve or reject pending actions](air-review-approve-pending-completed-actions#approve-or-reject-pending-actions-from-the-investigations-page-in-defender-for-office-365).
- **Remediated**: The investigation finished and all remediation actions were approved (noted as fully remediated).

    Approved remediation actions can have errors that prevent the actions from being taken. Regardless of whether remediation actions are successfully completed, the investigation status doesn't change. For more information, view the investigation details.
- **Running**: The investigation process is underway. This status value also occurs when [pending actions](air-review-approve-pending-completed-actions#approve-or-reject-pending-actions-from-the-investigations-page-in-defender-for-office-365) are approved.
- **Starting**: The investigation has been triggered and is waiting to start running.
- **Terminated By System**: The investigation stopped. For example:

    - Pending actions have expired (available for a maximum of one week).
    - Too many actions. For example, too many users clicking on malicious URLs can exceed the investigation's ability to run all the analyzers, so the investigation halts.

    If an investigation halts before actions were taken, try using [Threat Explorer (Explorer)](threat-explorer-real-time-detections-about) to find and address threats.
- **Terminated By Throttling**: An investigation automatically stops after it's been queued for too long, it stops.

    You can [start an investigation from Threat Explorer (Explorer)](air-examples#example-a-security-administrator-triggers-an-investigation-from-threat-explorer).

## View investigation details from AIR in Defender for Office 365 Plan 2

When you select ![](media/defender-portal-icon-copy.png)**Open in new window** in the **ID** column of an entry on the **Investigations** page at https://security.microsoft.com/airinvestigation, a new page opens with the investigation details.

The tile of the page is the **Investigation** (name) value on the **Investigations** page. For example, **Clicked url Verdict changed to malicious - &lt;URL&gt;**.

The subtitle of the page contains the **ID** and status of the investigation. For example, **Investigation #660b79 is complete - Remediated**.

The rest of the details page contains several tabs that contain detailed information about the investigation. Some tabs are common to all investigations. Other tabs are available based on the nature and status of the investigation.

The tabs are described in the following subsections.

[![Screenshot of the investigation details page in the Defender portal.](media/mdo-investigations-investigation-details-page.png)](media/mdo-investigations-investigation-details-page.png#lightbox)

### Investigation graph tab in the investigation details

On the investigation details page, the **Investigation graph** tab is the default tab that visually represents the current state and results of the investigation.

On the **Investigation graph** tab, the **Investigation summary** pane contains the following details:

- **Investigation status time line**section:
    - **Started**
    - **Ended**: This value is present only for the following **Status**values:
        - **No threats found**
        - **Partially remediated**
        - **Remediated**
        - **Terminated by system**
        - **Terminated by throttling**
        - **Terminated by user**
        - **Threats found**
        - **Failed**
    - **Duration**
    - **Total pending time**: This value is present only for investigations that had pending actions awaiting approval that were eventually approved or expired.
- **Investigation details**section:
    - **Status**: The status of the investigation. If the value is **No threats found**, no other values are present in the section.
    - **Alert severity**: The value **Low**, \*\*Medium, or **High**.
    - **Category**: The alert category.
    - **Detection source**: Typically, the value is **MDO**.

The graph pane contains a visual representation of the elements and activities in the investigation. Some elements are common to all investigations, while others depend on the nature and progress of the investigation.

- **Alert received**: Shows the related alerts. Select ![](media/mdo-investigations-alert-received-icon.png) to go to the **Alerts** tab for more information.
- **Mailbox**: Shows the related mailboxes. Select ![](media/mdo-investigations-mailbox-icon.png) to go to the **Mailboxes** tab for more information.
- **Entities analyzed**: Shows the number and type of related entities that were analyzed during the investigation. For example:

    - URLs
    - Email messages
    - Files
    - Email clusters, which might include the number of malicious and the number of remediated.

    Select ![](media/mdo-investigations-entities-analyzed-icon.png) to go to the **Entities** tab for more information.
- **Evidence**: Shows the number of entities found. Select ![](media/mdo-investigations-evidence-icon.png) to go to the **Evidence** tab for more information.
- **Pending approval**: Shows how long the system has been waiting for an admin to do the suggested manual remediation action (for example, soft delete an email message). Select ![](media/mdo-investigations-pending-approval-icon.png) to go to the **Pending actions** tab for more information.

    After an admin does the action, this item is replaced by **Waited for user approval**.
- **Waited for user approval**: Shows how long it took for an admin to do the suggested manual remediation action. Select ![](media/mdo-investigations-waited-for-user-approval-icon.png) to go to the **Pending actions history** tab for more information.
- **Result**: This item is available after the investigation is finished, and is duplicated in the following locations on the page:

    - In the center of the graph. Select the icon to go to the **Log** tab.
    - In the page title.
    - In the **Investigation summary** pane &gt; **Investigation details** section &gt; **Status** value.

    For example:

    - **Remediated**![](media/mdo-investigations-result-remediated-icon.png)
    - **Terminated by system**: ![](media/mdo-investigations-result-terminated-by-system-icon.png)
    - **No threats found**![](media/mdo-investigations-result-no-threats-found-icon.png)
    - **Partially investigated**![](media/mdo-investigations-result-partially-investigate-icon.png)

        Some findings might require review. Use the **Evidence** and **Entities** tabs to manually investigate and remediate any potential issues.
    - **Partially remediated**![](media/mdo-investigations-result-partially-remediated-icon.png)

        A problem prevented the remediation of some malicious entities. Use the **Evidence** and **Entities** tabs to manually investigate and remediate any potential issues.

[![Screenshot of the Investigation graph tab of the investigation details page.](media/mdo-investigations-investigation-details-page-investigation-graph-tab.png)](media/mdo-investigations-investigation-details-page-investigation-graph-tab.png#lightbox)

### Alerts tab in the investigation details

On the investigation details page, the **Alerts** tab shows the alerts related to the investigation.

You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. The default columns are marked with an asterisk ^\*^:

- **Alert name**^\*^
- **Tags**^\*^
- **Severity**^\*^
- **Incident Name**^\*^
- **Incident ID**^\*^
- **Status**^\*^
- **Category**^\*^
- **Impacted assets**
- **User**^\*^
- **Service Source**^\*^
- **Detection source**
- **Investigation state**^\*^
- **Last activity**^\*^
- **Classification**^\*^
- **Determination**
- **Assigned to**^\*^

Clicking on the **Alert name** value in a row takes you to the details page for the alert. This details page is the same as clicking on the **Alert name** value in the corresponding entry on the **Alerts** page at https://security.microsoft.com/alerts. For more information, see [Analyze an alert](/en-us/defender-xdr/investigate-alerts#analyze-an-alert).

Clicking anywhere else in the row other than the **Alert name** value or the check box next to the first column opens a details flyout for the alert. This details flyout is the same as clicking anywhere in the row other than the **Alert name** value or the check box next to the first column on the corresponding entry on the **Alerts** page at https://security.microsoft.com/alerts.

The actions that are available at the top of the alert details flyout depend on the nature of the alert contain the same actions that are available in the details flyout of the corresponding alert on the **Alerts** page at https://security.microsoft.com/alerts. For example, alerts named **Email messages containing malicious URL removed after delivery** have the following actions available in the alert details flyout:

- ![](media/defender-portal-icon-open-url-page.png)**Open alert page**: Opens the same details page as when you click on the **Alert name** value of an entry on the **Alerts** page at https://security.microsoft.com/alerts. For more information, see [Analyze an alert](/en-us/defender-xdr/investigate-alerts#analyze-an-alert).
- ![](media/defender-portal-icon-edit.png)**Manage alert**: Opens a **Manage alert** flyout where you can view and modify details about the incident. For more information, see [Manage alerts](/en-us/defender-xdr/investigate-alerts#manage-alerts).
- ![](media/defender-portal-icon-graph.png)**View messages in Explorer**: Opens Explorer (Threat Explorer) in the **All email** view filtered by the **Alert ID**. For more information about the **All email** view of Threat Explorer, see [All email view in Threat Explorer](threat-explorer-real-time-detections-about#all-email-view-in-threat-explorer).
- ![](media/defender-portal-icon-more-actions.png)**More actions** &gt; ![](media/defender-portal-icon-link-alert.png)**Link alert to another incident**: In the **Link alert to another incident** flyout that opens, configure the following options:

    - Select one of the following values:
        - **Create a new incident**
        - **Link to an existing incident**: In the **Incident name or ID** box that appears, start typing a value to find and select the existing incident.
    - **Comment**: Enter an optional comment.

    When you're finished in the **Link alert to another incident** flyout, select **Save**
- ![](media/defender-portal-icon-more-actions.png)**More actions** &gt; ![](media/defender-portal-icon-wrench.png)**Tune alert**: Opens a **Tune alert** flyout. For more information, see Step 3 and later in [Create rule conditions to tune alerts](/en-us/defender-xdr/investigate-alerts#create-rule-conditions-to-tune-alerts).
- ![](media/defender-portal-icon-more-actions.png)**More actions** &gt; ![](media/defender-portal-icon-question-mark.png)**Ask Defender Experts**. Opens an **Ask Defender Experts** flyout. For more information, see [Collaborate with experts on demand](/en-us/defender-xdr/experts-on-demand).

### Mailboxes tab in the investigation details

On the investigation details page, the **Mailboxes** tab is available if any mailboxes were inspected as part of the investigation.

You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. By default, all available columns are selected:

- **Username**
- **Risk level**
- **Risk**
- **Risky activities**
- **Upn**
- **Urn**

Clicking anywhere in a row other than the check box next to the first column opens a mailbox details flyout with the following information:

- **Verdict**
- **Display name**
- **Primary email address**
- **UPN**
- **Object ID**
- **Risk level**
- **Risk**

Select ![](media/defender-portal-icon-open.png)**More details about user** to open the User entity page in Microsoft Defender XDR. For more information, see [User entity page in Microsoft Defender XDR](/en-us/defender-xdr/investigate-users).

### Evidence tab in the investigation details

On the investigation details page, the **Evidence** tab shows the suspicious entities that were analyzed, and the results of the analysis.

You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. The default columns are marked with an asterisk ^\*^:

- **First seen**^\*^
- **Entity**^\*^
- **Verdict**^\*^
- **Remediation status**^\*^
- **Status details**
- **Impacted assets**^\*^
- **Detection origin**^\*^
- **Threats**

To filter the entries, select ![](media/defender-portal-icon-filter.png)**Filter**. The following filters are available in the **Filter** flyout that opens:

- **Entity**: Type some or all of the entity name in the box.
- **Verdict**: The values you can select depend on the **Verdict** values on the tab.
- **Detection origin**: The values you can select depend on the **Detection origin** values on the tab.

When you're finished in the **Filter** flyout, select **Apply**. To clear the filters, select ![](media/defender-portal-icon-clear-filters.png)**Clear filters**.

Clicking anywhere in a row other than the check box next to the first column opens a details flyout. What's available in the flyout depends on the nature of the evidence (email message, file, URL, etc.).

### Entities tab in the investigation details

On the investigation details page, the **Entities** tab shows details about the different types of entities that were encountered and analyzed during the investigation.

[![Screenshot of the Entities tab of the investigation details page.](media/mdo-investigations-investigation-details-page-entities-tab-evidence-summary-view.png)](media/mdo-investigations-investigation-details-page-entities-tab-evidence-summary-view.png#lightbox)

The **Entities** tab is organized by a view selection pane (a summary view and a view for each entity type) and a corresponding details table for that view:

- **Evidence summary** view: This view is the default.

    You can sort the entries in the details table by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. By default, all available columns are selected:

    - **Entity type** (you can't deselect this value): Contains the same values as the view selection pane, depending on the incident. For example:

        - **Files**
        - **URLs**
        - **Email submissions**
        - **Emails**
        - **IP addresses**
        - **Email clusters**

        The following columns show the count for each entity type (row):

        - **Total**
        - **Remediated**
        - **Malicious**
        - **Suspicious**
        - **Verified**
        - **No threats found**
        - **Unknown**
        - **Not found**
        - **Unremediated**
        - **Partially Remediated**

    Clicking anywhere in a row anywhere other than the check box next to the **Entity type** column takes you to the related view from the selection page (for example, **Emails**).
- **Files** view: You can sort the entries in the details table by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. The default columns are marked with an asterisk ^\*^:

    - **Verdict**^\*^
    - **Remediation status**^\*^
    - **Status details**
    - **File path**^\*^
    - **File name**^\*^ (you can't deselect this value)
    - **Device**^\*^
- **URLs** view: You can sort the entries in the details table by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. By default, all available columns are selected:

    - **Verdict**
    - **Remediation status**
    - **Address** (you can't deselect this value)

    Clicking anywhere in a row other than the check box next to the first column opens a details flyout that contains the following information:

    - **Original URL**
    - **Detection** section
    - **Domain details** section
    - **Registrant contact info** section
    - **URL prevalence (last 30 days)** section

    The following actions for the URL are also available in the flyout:

    - **Open URL page**
    - **Submit for analysis**
    - **Manage indicator**
    - **View in Explorer**
    - **Go hunt**
- **Email submissions** view: You can sort the entries in the details table by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. By default, all available columns are selected:

    - **Verdict**
    - **Remediation status**
    - **Subject**
    - **Sender**
    - **Recipient**
    - **Reported by**
    - **Report type**

    Clicking anywhere in a row other than the check box next to the first column opens a details flyout that contains the following information:

    - **Email submission details** section

    The **Go hunt** action for the email submission is also available in the flyout.
- **Emails** view: You can sort the entries in the details table by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. By default, all available columns are selected:

    - **Verdict**
    - **Remediation status**
    - **Email Received Date** (you can't deselect this value)
    - **Delivery Status**
    - **Subject**
    - **Sender**
    - **Recipient**

    Clicking anywhere in a row other than the check box next to the first column opens a details flyout that contains the following information:

    - **Email details** section

    Select **More details about email** to view the Email entity page in Defender for XDR. 

    The following actions for the email message are also available in the flyout:

    - **Go hunt**
    - **Open in Explorer**
- **IP addresses** view: You can sort the entries in the details table by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. By default, all available columns are selected:

    - **Verdict**
    - **Remediation status**
    - **Address** (you can't deselect this value)

    Clicking anywhere in a row other than the check box next to the first column opens a details flyout that contains the following information:

    - **IP details** section
    - **Detection** section
    - **IP observed in organization devices** section

    The following actions for the IP addresses are also available in the flyout:

    - **Open IP address page**
    - **Add indicator**
    - **Open cloud app IP settings**
    - **Investigate in Activity log**
    - **Go hunt**
- **Email Clusters** view: You can sort the entries in the details table by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. By default, all available columns are selected:

    - **Verdict**
    - **Remediation status**
    - **Mail cluster name** (you can't deselect this value)
    - **Threats**
    - **Email count**
    - **Malware**
    - **Phish**
    - **High confidence phish**
    - **Spam**
    - **Delivered**
    - **Junked**
    - **Replaced**
    - **Blocked**
    - **Mailbox**
    - **Not in mailbox**
    - **On-prem/External**
    - **Volume anomaly**

    Clicking anywhere in a row other than the check box next to the first column opens a details flyout that contains the following information:

    - **Email cluster details** section
    - **Threats** section
    - **Latest delivery locations** section
    - **Original delivery locations** section

    The following actions for the email cluster are also available in the flyout:

    - **Go hunt**
    - **Open in Explorer**

### Log tab in the investigation details

On the investigation details page, the **Log** tab shows all actions that were taken during the investigation.

You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. The default columns are marked with an asterisk ^\*^:

- **ID**
- **Action type**
- **Action**^\*^
- **Status**^\*^
- **Device name**^\*^
- **Description**^\*^
- **Comments**
- **Time created**
- **Execution start time**^\*^
- **Duration**^\*^
- **Pending duration**
- **Queued Duration**

Use ![](media/defender-portal-icon-download.png)**Export** to save the visible information to a CSV file. The default filename is AirLogs.csv, and the default location is the local Downloads folder. If an exported report already exists in that location, the filename is incremented (for example, AirLogs (1).csv).

Clicking anywhere in a row other than the check box next to the first column opens a summary flyout that contains the following information:

- **Status**
- **Create**
- **Execution start**
- **Duration**
- **Description**

Tip

To see details about other entries without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

### Pending approval tab in the investigation details

On the investigation details page, the **Pending approval** tab shows pending actions that are waiting for approval to complete (for example, soft deleting messages).

The **Pending approval** tab is organized by a view selection pane (a view for each action type) and a corresponding details table for that view:

- **Soft delete emails**: You can sort the entries in the details table by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. The default columns are marked with an asterisk ^\*^:
    - **Investigation ID**
    - **First seen**
    - **Details**
    - **Email count**
    - **Malware**
    - **Phish**
    - **High Confidence Phish**
    - **Spam**
    - **Delivered**
    - **Junked**
    - **Replaced**
    - **Blocked**
    - **Mailbox**
    - **Not in mailbox**
    - **On-prem/External**
    - **Mailbox**
    - **Entity type**
    - **Threat type**
    - **Subject**

Use ![](media/defender-portal-icon-download.png)**Export** to save the visible information to a CSV file. The default filename is AirActions.csv, and the default location is the local Downloads folder. If an exported report already exists in that location, the filename is incremented (for example, AirActions (1).csv).

Clicking anywhere in a row other than the check box next to the first column opens a details flyout that contains the following information:

- **Email cluster details**section
    - **Verdict**
    - **Remediation status**
    - **Email count**
    - **Name**
    - **Volume anomaly**
    - **Query time**
- **Threats**section:
    - **Threats**: Summarizes the threats found in the email cluster. For example, `MaliciousUrl, HighConfPhish, Volume anomaly`.
    - Counts for the following threat types found in the email cluster:
        - **Malware**
        - **Phish**
        - **High Confidence Phish**
        - **Spam**
- **Latest delivery location**section: Counts for the following delivery locations for messages in the email cluster:
    - **Mailbox**
    - **Not in mailbox**
    - **On-prem/External**
- **Original delivery locations**section: Counts for the following original delivery locations for messages in the email cluster:
    - **Delivered**
    - **Junked**
    - **Replaced**
    - **Blocked**

The following actions for the email messages are also available in the flyout:

- **Go hunt**
- **Open in Explorer**

![](media/defender-portal-icon-check-mark.png)**Approve** and ![](media/defender-portal-icon-remove.png)**Reject** are described in the next subsection.

#### Approve actions on the Pending approval tab in the investigation details

On the **Pending approval** tab on the investigation details page, select a pending action by clicking anywhere in the row other than the check box next to the first column.

The details flyout that opens is named after the pending action (for example, **Soft delete emails**). Read the information in the flyout, and then select one of the following values:

- ![](media/defender-portal-icon-check-mark.png)**Approve**.
- ![](media/defender-portal-icon-remove.png)**Reject**.

Tip

Approving and/or rejecting all actions in the investigation fully closes it (the **Status** value becomes **Remediated**). Failing to approve and/or reject all actions in the investigation doesn't fully close it (the **Status** value remains **Partially Remediated**).

You don't need to approve every action. If you don't agree with the recommended action or your organization doesn't choose certain types of actions, you can reject the action or take no action.

### Pending actions history tab in the investigation details

On the investigation details page, the **Pending actions history** tab shows pending actions that were completed.

You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. By default, all available columns are selected:

- **Action type**
- **Wait time**
- **Entity**
- **Status**
- **Handled by**
- **Time**

Use ![](media/defender-portal-icon-download.png)**Export** to save the visible information to a CSV file. The default filename is AirActions.csv, and the default location is the local Downloads folder. If an exported report already exists in that location, the filename is incremented (for example, AirActions (1).csv).

Clicking on the **Entity** value in a row opens a details flyout with the following information about the email cluster:

- **Email cluster details** section
- **Threats** section
- **Latest delivery locations** section
- **Original delivery locations** section

The following actions for the email cluster are also available in the flyout:

- **Go hunt**
- **Open in Explorer**

Clicking anywhere in a row other than the check box next to the first column or the **Entity** value opens an action history details flyout that contains the following information:

- **Summary**section:
    - **Status**
    - **Create**
    - **Execution start**
    - **Description**

## View details about an alert related to an investigation

Certain kinds of alerts trigger automated investigation in Microsoft 365. To learn more, see [Threat management alert policies](/en-us/defender-xdr/alert-policies#threat-management-alert-policies).

1. In the Microsoft 365 Defender portal a https://security.microsoft.com, go to **Actions & submissions** &gt; **Action center**. Or, to go directly to the **Action center** page, use https://security.microsoft.com/action-center/.
2. On the **Action center** page, use the **Pending** or **History** tabs to find the action.
3. Select an action from the table by selecting the link in the **Investigation ID** column.

The investigation details page opens.