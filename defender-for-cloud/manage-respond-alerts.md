---
layout: Conceptual
title: Manage and Respond to Security Alerts - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/manage-respond-alerts
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
description: Learn how to use Microsoft Defender for Cloud capabilities to manage and respond to security alerts.
ms.date: 2026-05-28T00:00:00.0000000Z
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1013
- sfi-image-nochange
- ge-structured-content-pilot
ai-usage: ai-assisted
locale: en-us
document_id: a64ecb75-0218-c927-72fd-b451a159d2fb
document_version_independent_id: 18f148f8-665e-3fb5-1f9e-5785413c73b6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/manage-respond-alerts.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/manage-respond-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/manage-respond-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 2186578c-1427-05c5-f2aa-d65255249154
---

# Manage and Respond to Security Alerts - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud collects, analyzes, and integrates log data from your Azure, hybrid, and multicloud resources, the network, and connected partner solutions, such as firewalls and endpoint agents. Defender for Cloud uses the log data to detect real threats and reduce false positives. Defender for Cloud shows a list of prioritized security alerts along with the information you need to quickly investigate the problem and the steps to take to remediate an attack.

## View, investigate, and respond to security alerts in Defender for Cloud

This article shows you how to view and process Defender for Cloud's alerts and protect your resources.

When you triage security alerts, prioritize alerts based on their alert severity. Address higher severity alerts first. To learn more, see [how alerts are classified](alerts-overview#how-are-alerts-classified).

Tip

You can connect Microsoft Defender for Cloud to SIEM solutions including Microsoft Sentinel and consume the alerts from your tool of choice. Learn more how to [stream alerts to a SIEM, SOAR, or IT Service Management solution](export-to-siem).

## Prerequisites

For prerequisites and requirements, see [Support matrices for Defender for Cloud](support-matrix-defender-for-cloud).

## Manage your security alerts

Follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Security alerts**.

    ![Screenshot that shows the security alerts page from Microsoft Defender for Cloud's overview page.](media/managing-and-responding-alerts/overview-page-alerts-links.png)
3. (Optional) Filter the alerts list with any of the relevant filters. Add extra filters by selecting **Add filter**.

    [![Screenshot that shows you how to add filters to the alerts view.](media/managing-and-responding-alerts/alerts-adding-filters-small.png)](media/managing-and-responding-alerts/alerts-adding-filters-large.png#lightbox)

    The alerts list updates according to the filters you select. For example, you might want to address security alerts that occurred in the last 24 hours to investigate a potential breach in the system.

## Investigate a security alert

Each alert contains information that helps you investigate the alert.

To investigate a security alert:

1. Select an alert. A pane opens and shows a description of the alert and all the affected resources.

    ![Screenshot of the high-level details view of a security alert.](media/managing-and-responding-alerts/alerts-details-pane.png)
2. Review the high-level information about the security alert.

    - Alert severity, status, and activity time
    - Description that explains the precise activity that was detected
    - Affected resources
    - Kill chain intent of the activity on the MITRE ATT&CK matrix, if applicable
3. Select **View full details**.

    The right pane includes the **Alert details** tab that contains more details to help you investigate the alert, such as IP addresses, files, and processes.

    ![Screenshot that shows the full details page for an alert.](media/managing-and-responding-alerts/security-center-alert-remediate.png)

    The right pane also includes the **Take action** tab. Use this tab to take further actions regarding the security alert, such as:

    - **Inspect resource context**: Takes you to the resource's activity logs that support the security alert.
    - **Mitigate the threat**: Provides manual remediation steps for this security alert.
    - **Prevent future attacks**: Provides security recommendations to help reduce the attack surface, increase security posture, and thus prevent future attacks.
    - **Trigger automated response**: Provides the option to trigger a logic app as a response to this security alert.
    - **Suppress similar alerts**: Provides the option to suppress future alerts with similar characteristics if the alert isn't relevant for your organization.

    ![Screenshot that shows the options available in the Take action tab.](media/managing-and-responding-alerts/alert-take-action.png)

    To learn more about the alert, contact the resource owner to verify whether the detected activity is a false positive. You can also investigate the raw logs generated by the attacked resource.

## Change the status of multiple security alerts at once

The alerts list includes checkboxes so you can handle multiple alerts at once. For example, for triaging purposes you might decide to dismiss all informational alerts for a specific resource.

1. Filter according to the alerts you want to handle in bulk.

    In this example, the alerts with severity of `Informational` for the resource `ASC-AKS-CLOUD-TALK` are selected.

    ![Screenshot that shows how to filter alerts to show related alerts.](media/managing-and-responding-alerts/processing-alerts-bulk-filter.png)
2. Use the checkboxes to select the alerts to process.

    In this example, you select all alerts. The **Change status** button is now available.

    ![Screenshot of selecting all alerts to handle in bulk.](media/managing-and-responding-alerts/processing-alerts-bulk-select.png)
3. Use the **Change status** options to set the desired status.

    ![Screenshot of the security alerts status tab.](media/managing-and-responding-alerts/processing-alerts-bulk-change-status.png)

    Change the status for the alerts shown on the Security alerts page to the selected value.

## Respond to a security alert

After investigating a security alert, you can respond to the alert from within Microsoft Defender for Cloud.

To respond to a security alert:

1. Open the **Take action** tab to see the recommended responses.

    [![Screenshot of the security alerts take action tab.](media/managing-and-responding-alerts/alert-details-take-action.png)](media/managing-and-responding-alerts/alert-details-take-action.png#lightbox)
2. Review the **Mitigate the threat** section for the manual investigation steps necessary to mitigate the issue.
3. To harden your resources and prevent future attacks of this kind, remediate the security recommendations in the **Prevent future attacks** section.
4. To trigger a logic app with automated response steps, use the **Trigger automated response** section and select **Trigger logic app**.
5. If the detected activity *isn't* malicious, you can suppress future alerts of this kind by using the **Suppress similar alerts** section and selecting **Create suppression rule**.
6. Select **Configure email notification settings** to view who receives emails regarding security alerts on this subscription. Contact the subscription owner to configure the email settings.
7. When you complete the investigation into the alert and respond in the appropriate way, change the status to **Dismissed**.

    ![Screenshot of the alert's status drop down menu.](media/managing-and-responding-alerts/set-status-dismissed.png)

    The alert is removed from the main alerts list. You can use the filter from the alerts list page to view all alerts with **Dismissed** status.
8. We encourage you to provide feedback about the alert to Microsoft:

    1. For **Was this useful?**, select **Yes** or **No**.
    2. Select a reason and add a comment.

    ![Screenshot of the provide feedback to Microsoft window that allows you to select the usefulness of an alert.](media/managing-and-responding-alerts/alert-feedback.png)

Tip

Microsoft reviews your feedback to improve the algorithms and provide better security alerts.

To learn about alert types, see [Security alerts - a reference guide](alerts-reference).

For information about how Defender for Cloud detects and responds to threats, see [How Microsoft Defender for Cloud detects and responds to threats](alerts-overview).

## Review the agentless scan's results

You can see the results for both the agent-based and agentless scanners on the **Security alerts** page.

[![Screenshot of the security alerts page that shows the results of both the agent-based and agentless scan results.](media/managing-and-responding-alerts/agent-and-agentless-results.png)](media/managing-and-responding-alerts/agent-and-agentless-results.png#lightbox)

Note

Remediating the agent-based alert doesn't remediate the corresponding agentless alert until the next scan is completed.