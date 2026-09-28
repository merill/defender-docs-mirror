---
layout: Conceptual
title: Respond to Defender for Resource Manager alerts - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-resource-manager-usage
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Investigate and remediate security alerts from Defender for Resource Manager. Covers connected Azure resources, subscriptions, and user activity.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 7bdf257c-7973-32a3-40d7-c19dd9d097d8
document_version_independent_id: bfc3e912-a4d1-fab8-a3d9-2bd79d339528
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-resource-manager-usage.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-resource-manager-usage
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-resource-manager-usage.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e834929-0ce1-4c1d-9c81-fcb14721edfb
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/75670257-a3f0-4627-9981-8046f99219e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 83609f0f-2bab-8c3c-2635-bbacacec898e
---

# Respond to Defender for Resource Manager alerts - Microsoft Defender for Cloud | Microsoft Learn

Use this article to investigate and mitigate security alerts from Microsoft Defender for Resource Manager. It helps you validate suspicious activity and take immediate containment steps for affected accounts, subscriptions, and virtual machines.

## Investigate and respond to alerts

Investigate and respond to alerts from Microsoft Defender for Resource Manager by using the guidance in this document. Defender for Resource Manager protects all connected resources. Verify the situation around every alert, even if you're familiar with the application or user that triggered it.

## Respond to an alert

Contact the resource owner to determine whether the behavior was expected or intentional. Dismiss the alert if the activity is expected. If the activity is unexpected, treat related user accounts, subscriptions, and virtual machines as compromised. Investigate and mitigate the threat by using the remediation steps below.

## Investigate alerts from Microsoft Defender for Resource Manager

Security alerts from Defender for Resource Manager are based on threats detected by monitoring Azure Resource Manager operations. Defender for Cloud uses internal log sources and Azure Activity log. Azure Activity log is an Azure platform log that provides insight into subscription-level events.

Defender for Resource Manager provides visibility into activities from non-Microsoft service providers that delegate access as part of Resource Manager alerts. For example, `Azure Resource Manager operation from suspicious proxy IP address - delegated access`.

`Delegated access` refers to access granted through Azure Lighthouse or Delegated administration privileges. For details, see [Azure Lighthouse](/en-us/azure/lighthouse/overview) and [Delegated administration privileges](/en-us/partner-center/dap-faq).

Alerts that show `Delegated access` also include a customized description and remediation steps.

Azure Activity log provides subscription-level events for investigations. For details, see [Azure Activity log documentation](/en-us/azure/azure-monitor/essentials/activity-log).

To investigate security alerts from Defender for Resource Manager:

1. Open Azure Activity log.

    ![How to open Azure Activity log](media/defender-for-resource-manager-introduction/opening-azure-activity-log.png)
2. Filter the events to:

    - The subscription mentioned in the alert
    - The time frame of the detected activity
    - The related user account (if relevant)
3. Look for suspicious activities.

Tip

For a richer investigation experience, stream your Azure Activity logs to Microsoft Sentinel. For setup steps, see [Connect data from Azure Activity log](/en-us/azure/sentinel/data-connectors/azure-activity).

## Mitigate immediately

To contain the threat and prevent further damage, perform these steps immediately:

1. Remediate compromised user accounts:

    - Delete accounts that you don't recognize because a threat actor might have created them.
    - For accounts you recognize, change their authentication credentials.
    - Review all user activities in Azure Activity logs and identify suspicious actions.
2. Remediate compromised subscriptions:

    - Remove unfamiliar runbooks from any compromised automation accounts.
    - Review IAM permissions for the subscription and remove permissions for unfamiliar user accounts.
    - Review all Azure resources in the subscription and delete any unfamiliar resources.
    - Review and investigate security alerts for the subscription in Microsoft Defender for Cloud.
    - Use Azure Activity logs to review all activities in the subscription and identify suspicious actions.
3. Remediate compromised virtual machines:

    - Change passwords for all users.
    - Run a full antimalware scan on each machine.
    - Reimage machines from a verified malware-free source.