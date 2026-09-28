---
layout: Conceptual
title: Create cloud discovery policies - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/cloud-discovery-policies
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
description: Create app discovery policies in Microsoft Defender for Cloud Apps to detect newly discovered apps and configure anomaly detection for cloud discovery logs.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: dfc81556-3815-02eb-ccb4-93e02c386164
document_version_independent_id: dfc81556-3815-02eb-ccb4-93e02c386164
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/cloud-discovery-policies.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: cloud-discovery-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/cloud-discovery-policies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 8c900dae-6805-dc3d-93af-a132fc1fdec7
---

# Create cloud discovery policies - Microsoft Defender for Cloud Apps | Microsoft Learn

You can create app discovery policies to alert you when new apps are detected. Defender for Cloud Apps also searches all the logs in your cloud discovery for anomalies. This article explains how to create and configure app discovery policies to monitor newly discovered apps, and how to use cloud discovery anomaly detection to identify unusual usage patterns in your environment.

## Creating an app discovery policy

Discovery policies enable you to set alerts that notify you when new apps are detected within your organization.

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Then select the **Shadow IT** tab.
2. Select **Create policy** and then select **App discovery policy**.

    ![Screenshot of the Shadow IT tab showing the Create policy menu with the App discovery policy option.](media/create-policy-from-shadow-it-tab.png)
3. Give your policy a name and description. If you want, you can base it on a template. For more information on policy templates, see [Control cloud apps with policies](control-cloud-apps-with-policies).
4. Set the **Severity** of the policy.
5. To set which discovered apps trigger this policy, add filters.
6. You can set a threshold for how sensitive the policy should be. Enable **Trigger a policy match if all the following occur on the same day**. You can set criteria that the app must exceed daily to match the policy. Select one of the following criteria:

    - Daily traffic
    - Downloaded data
    - Number of IP addresses
    - Number of transactions
    - Number of users
    - Uploaded data
7. Set a **Daily alert limit** under **Alerts**. Select if the alert is sent as an email. Then provide email addresses as needed.

    - Selecting **Save alert settings as the default for your organization** enables future policies to use these alert settings.
    - If you have default alert settings saved for your organization, you can select **Use your organization's default settings**.
8. Select **Governance** actions to apply when an app matches this policy. It can tag policies as **Sanctioned**, **Unsanctioned**, **Monitored**, or a custom tag.
9. Select **Create**.

Note

- Newly created discovery policies (or policies with updated continuous reports) trigger an alert once in 90 days per app per continuous report, regardless of whether there are existing alerts for the same app. So, for example, if you create a policy for discovering new popular apps, it might trigger additional alerts for apps that have already been discovered and alerted on.
- Data from **snapshot reports** don't trigger alerts in app discovery policies.

For example, if you're interested in discovering risky hosting apps found in your cloud environment, set your policy as follows:

Set the policy filters to discover any services found in the **hosting services** category, and that have a risk score of 1, indicating they're highly risky.

In the **Trigger a policy match if all the following occur on the same day** section, set the thresholds that should trigger an alert for a certain discovered app. For instance, alert only if over 100 users in the environment used the app and if they downloaded a certain amount of data from the service. Additionally, you can set the limit of daily alerts you wish to receive.

![Screenshot of app discovery policy settings showing filter and threshold options for risky hosting apps.](media/app-discovery-policy-example.png)

## Cloud discovery anomaly detection

Defender for Cloud Apps searches all the logs in your cloud discovery for anomalies. For instance, when a user, who never used Dropbox before, suddenly uploads 600 GB to it, or when there are a lot more transactions than usual on a particular app. The anomaly detection policy is enabled by default. It's not necessary to configure a new policy for it to work. However, you can fine-tune which types of anomalies you want to be alerted about in the default policy.

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Then select the **Shadow IT** tab.
2. Select **Create policy** and select **Cloud Discovery anomaly detection policy**.

    ![Screenshot of the Create policy menu with the Cloud Discovery anomaly detection policy option selected.](media/cloud-discovery-anomaly-detection-policy-menu.png)
3. Give your policy a name and description. If you want, you can base it on a template, For more information on policy templates, see [Control cloud apps with policies](control-cloud-apps-with-policies).
4. To set which discovered apps trigger this policy, select **Add filters**.

    The filters are chosen from drop-down lists. To add filters, select **Add a filter**. To remove a filter, select the 'X'.
5. Under **Apply to** choose whether this policy applies **All continuous reports** or **Specific continuous reports**. Select whether the policy applies to **Users**, **IP addresses**, or both.

    [![Screenshot of Apply to settings for an app discovery policy with options for all or specific continuous reports and filters for users and IP addresses.](media/apply-to-continous-reports.png)](media/apply-to-continous-reports.png#lightbox)

    Important

    When you configure an app discovery policy and select **Apply to &gt; All continuous reports**, multiple alerts are generated for each discovery stream, including the global stream which aggregates data from all sources. To control alert volume, select **Apply to &gt; Specific continuous reports** and choose only the relevant streams for your policy. Learn more: [Defender for Cloud apps continuous risk assessment reports](set-up-cloud-discovery#snapshot-and-continuous-risk-assessment-reports)
6. Select the dates during which the anomalous activity occurred to trigger the alert under **Raise alerts only for suspicious activities occurring after date.**
7. Set a **Daily alert limit** under **Alerts**. Select if the alert is sent as an email. Then provide email addresses as needed.

    - Selecting **Save alert settings as the default for your organization** enables future policies to use these alert settings.
    - If you have default alert settings saved for your organization, you can select **Use your organization's default settings**.
8. Select **Create**.

    ![Screenshot of the new discovery anomaly policy page showing anomaly detection criteria and alert settings.](media/new-discovery-anomaly-policy.png)