---
layout: Conceptual
title: Security Operations Guide for Teams protection - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/mdo-support-teams-sec-ops-guide
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
description: A prescriptive playbook for SecOps personnel to manage Microsoft Teams protection in Microsoft Defender for Office 365.
ms.service: defender-office-365
ms.date: 2026-10-05T00:00:00.0000000Z
locale: en-us
document_id: 92aff1cd-08c4-9c50-3fe1-dd32992345be
document_version_independent_id: 92aff1cd-08c4-9c50-3fe1-dd32992345be
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/mdo-support-teams-sec-ops-guide.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdo-support-teams-sec-ops-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/mdo-support-teams-sec-ops-guide.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 8dc085f8-1b2e-eeb3-1225-714d133654b7
---

# Security Operations Guide for Teams protection - Microsoft Defender for Office 365 | Microsoft Learn

After you [configure Microsoft Teams protection in Microsoft Defender for Office 365](mdo-support-teams-quick-configure), you need to integrate Teams protection capabilities into your Security Operations (SecOps) response processes. This process is critical to ensure a high-quality, reliable approach to protect, detect, and respond to collaboration-related security threats.

Involving the SecOps team during the deployment/pilot phases ensures your organization is ready to deal with threats. Teams protection capabilities in Defender for Office 365 are natively integrated into the existing Defender for Office 365 and Defender SecOps tools and work flows.

Another important step is to ensure SecOps team members have the appropriate permissions to do their tasks.

## Integrate user reported Teams items into SecOps incident response

When users report Teams messages or calls or report meetings or meeting participants as malicious or non malicious, the reported items are sent to Microsoft and/or the reporting mailbox as defined by the [Teams user reported settings in Defender for Office 365](submissions-teams#user-reporting-settings-for-teams-items).

The following alerts are automatically generated and correlated to Defender Incidents for malicious and nonmalicious user reported items in Teams:

- **Teams message reported by user as security risk**
- **Teams message reported by user as not security risk**
- **Teams call reported by user as a security risk**
- **Teams call reported by user as a not security risk**

Reported meetings and meeting participants generate the same alert policies as reported calls.

Tip

Currently, these alerts don't generate automated investigation and response (AIR) investigations.

We strongly recommend that SecOps team members start triage and investigation from the [Defender incidents queue in the Microsoft Defender portal](/en-us/defender-office-365/mdo-sec-ops-manage-incidents-and-alerts) or SIEM/SOAR integration.

SecOps team members can review submitted Teams message, call, meeting, or meeting participant details in the following locations in the Defender portal:

- The **View submission** action in the Defender XDR incident.
- The **User reported** tab of the **Submissions** page at https://security.microsoft.com/reportsubmission?viewid=user:
    - Admins can submit user reported Teams messages to Microsoft for analysis from the **User reported** tab. Entries on the **Teams messages** tab are the result of manually submitting user reported Teams message to Microsoft ([converting the user submission to an admin submission](submissions-admin#submit-user-reported-messages-to-microsoft-for-analysis)).
    - Admins can use **Mark and notify** on reported Teams items to send response email to users who reported them.

SecOps team members can also use block entries in the Tenant Allow/Block List to block the following indicators of compromise:

- Suspicious URLs as yet unidentified by Defender for Office 365. URL block entries are enforced at time of click in Teams when [Teams integration in Safe Links policies is turned on](mdo-support-teams-quick-configure#step-2-verify-safe-links-integration-for-microsoft-teams).
- Files by using the SHA256 hash value.

## Enable SecOps to proactively manage false negatives in Microsoft Teams

SecOps team members can use threat hunting or information from external threat intelligence feeds to proactively respond to false negative Teams messages (bad messages allowed). They can use the information to proactively block threats. For example:

- [Create URL block entries](tenant-allow-block-list-urls-configure#create-block-entries-for-urls) in the Tenant Allow/Block List in Defender for Office 365. Block entries apply at time of click for URLs in Teams.
- [Block domains in Teams using the Tenant Allow/Block List](tenant-allow-block-list-teams-domains-configure).
- Submit undetected URLs to Microsoft using [admin submission](submissions-admin#report-questionable-urls-to-microsoft).

Tip

As previously described, admins can't proactively submit Teams messages to Microsoft for analysis. Instead, they submit user reported Teams messages to Microsoft ([converting the user submission to an admin submission](submissions-admin#submit-user-reported-messages-to-microsoft-for-analysis)).

## Enable SecOps to manage false positives in Microsoft Teams

SecOps team members can triage and respond to false positive Teams messages (good messages blocked) on the **Quarantine** page in Defender for Office 365 at https://security.microsoft.com/quarantine. Teams messages detected by zero-hour auto protection (ZAP) are available on the **Teams messages** tab. SecOps team members can [take action](quarantine-admin-manage-messages-files#take-action-on-quarantined-teams-messages) on these messages. For example, preview messages, download messages, submit messages to Microsoft for review, and release the messages from quarantine.

SecOps team members can also use allow entries in the Tenant Allow/Block List to allow the misclassified indicators:

- URLs misidentified by Defender for Office 365 via the [URL tab on the Submissions page](submissions-admin#report-good-urls-to-microsoft). URL allows entries are enforced at time of click in Teams when [Teams integration in Safe Links policies is turned on](mdo-support-teams-quick-configure#step-2-verify-safe-links-integration-for-microsoft-teams).
- Files by using the SHA256 hash value from the [Email attachments tab on the Submissions page](submissions-admin#report-good-email-attachments-to-microsoft)

Tip

Teams messages released from quarantine are available to senders and recipients in the original location in Teams chats and channel posts.

## Enable SecOps to hunt for threats and detections in Microsoft Teams

SecOps team members can proactively hunt for potentially malicious Teams messages, URL clicks in Teams, and file detected as malicious. You can use this information to find potential threats, analyze patterns, and develop custom detections in Microsoft Defender to automatically generate incidents.

- On the **Explorer** page (Threat Explorer) in the Defender portal at https://security.microsoft.com/threatexplorerv3:

    - **Content malware** tab: This tab contains files detected by Safe Attachments for SharePoint, OneDrive, and Microsoft Teams. You can use the [available filters](threat-explorer-real-time-detections-about#filterable-properties-in-the-content-malware-view-in-threat-explorer-and-real-time-detections) to hunt on detection data.
    - **URL click** tab: This tab contains all user clicks on URLs in email, in supported Office files in SharePoint and OneDrive, and in Microsoft Teams. You can use the [available filters](threat-explorer-real-time-detections-about#filterable-properties-in-the-url-clicks-view-in-threat-explorer) to hunt on detection data.
- On the **Advanced hunting** page in the Defender portal at https://security.microsoft.com/v2/advanced-hunting. The following hunting tables are available for Teams-related threats:

    - [MessageEvents](/en-us/defender-xdr/advanced-hunting-messageevents-table): Contains raw data about every internal and external Teams message that included a URL. Sender address, Sender display name, Sender type, and more are available in this table.
    - [MessagePostDeliveryEvents](/en-us/defender-xdr/advanced-hunting-messagepostdeliveryevents-table): Contains raw data about ZAP events on Teams messages.
    - [MessageUrlInfo](/en-us/defender-xdr/advanced-hunting-messageurlinfo-table): Contains raw data about URLs in Teams messages.
    - [UrlClickEvents](/en-us/defender-xdr/advanced-hunting-urlclickevents-table): Contains raw data about every allowed or blocked URL click by users in Teams clients.

    SecOps team members can join these hunting tables with other workload tables (for example, EmailEvents or Device-related tables) to gain insight into end to end user activities.

    For example, you can use the following query to hunt for allowed clicks on URLs in Teams messages that were removed by ZAP:

    ```kusto
    MessagePostDeliveryEvents
    | join MessageUrlInfo on TeamsMessageId
    | join UrlClickEvents on Url
    | join EmailUrlInfo on Url
    | where Workload == "Teams" and ActionType1 == "ClickAllowed"
    | project TimeGenerated, TeamsMessageId, ActionType, RecipientDetails, LatestDeliveryLocation, Url, ActionType1
    ```

    [Community queries in advanced hunting](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/use-community-queries-to-hunt-more-effectively-across-email-and-collaboration-th/4254664) also offers Teams query examples.