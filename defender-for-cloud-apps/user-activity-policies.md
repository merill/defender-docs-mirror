---
layout: Conceptual
title: Create activity policies - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/user-activity-policies
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
description: Create and manage activity policies in Microsoft Defender for Cloud Apps to monitor user actions, automate enforcement, and generate alerts for suspicious activity.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Ronen-Refaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 22995298-6ef5-cd6f-d8b3-b9b7cf26eaf0
document_version_independent_id: 22995298-6ef5-cd6f-d8b3-b9b7cf26eaf0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/user-activity-policies.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: user-activity-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/user-activity-policies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 23c09a04-7bd0-810f-6f02-77e3bfd38b8a
---

# Create activity policies - Microsoft Defender for Cloud Apps | Microsoft Learn

Activity policies allow you to enforce a wide range of automated processes using the app provider's APIs. These policies enable you to monitor specific activities carried out by various users, or follow unexpectedly high rates of one certain type of activity.

After you set an activity detection policy, it starts to generate alerts - alerts are only generated on activities that occur after you create the policy.

Note

- Policies that trigger more than 200,000 matches per day, or 100,000 matches per 3 hours, may be disabled automatically. You can try refining policies by adding additional filters or, if you're using policies for reporting purposes, consider [saving activity filters as queries](activity-filters-queries#activity-queries) instead.
- It may take up to 15 minutes from setting up a new policy to deployment.

## Create custom alerts for activity policies

Activity policies allow custom alerts to be sent or actions taken when user activity is detected. For example, you want to know every time:

- A user tries to sign in and fails 70 times in one minute
- A user downloads 7,000 files
- A user is logged in from an unfamiliar country/region

You can set activity alerts to be sent to yourself or to the user when the activities defined in the policy are detected. You can even suspend the affected user until you have finished investigating the activity.

To create a new activity policy, follow this procedure:

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Then select the **Threat detections** tab.
2. Select **Create policy** and select **Activity policy**.

    ![Screenshot of the Threat Detection tab showing the Create policy menu with Activity policy option.](media/create-policy-from-threat-detection-tab.png)
3. Give your policy a name and description, if you want you can base it on a template, for more information on policy templates, see [Control cloud apps with policies](control-cloud-apps-with-policies).
4. To set which actions or other metrics trigger this policy, work with the **Activity filters**.

    To ensure that you only include results where the specified filter field has a value, we recommend adding the same field again using the **is set** test. For example, when filtering by **Location***does not equal* a specified list of countries/regions, also add a filter for **Location***is set*. You can also preview the filter results by selecting **Edit and preview results**. For example:

    ![Screenshot of activity filter settings with a Location does not equal filter and a Location is set filter configured together.](media/activity-example-location-isset.png)

    When a filter is set to *does not equal* and the attribute doesn't exist on the event, the event won't be filtered out. For example, filtering on **Device Tag does not equal Microsoft Entra hybrid joined** doesn't filter out events that don't contain **Device tag**, even if the device is Microsoft Entra joined.

    In case of a guest user, there may be cases where the **User From Group** filter doesn't recognize the account by its domain. To make sure all guest users are included, use the **External users** as the group, if it meets your needs for the policy.
5. Under **Create filters for the policy**, select when a policy violation will be triggered. Choose to trigger when a **Single activity** matches the filters or only when a specified number of **Repeated activities** are detected.

    - If you choose **Repeated activity**, you can set **In a single app**. This setting triggers a policy match only when the repeated activities occur in the same app. For example, five downloads in 30 minutes from Box trigger a policy match.
6. In the **Alerts** section, configure any of the following actions as needed:

    - **Create an alert for each matching event with the policy's severity**
    - **Send an alert as email**
    - **Daily alert limit per policy**. Note that governance actions are not impacted by the daily alert limit.
    - **Send alerts to Power Automate**
7. Configure the **Actions** that should be taken when a match is found.

Take a look at these examples:

- Multiple failed logins

    You can set policy so that you receive an alert when a large number of failed logins within a short time period occurs. To configure this sort of policy, choose the appropriate activity filter in the **New Activity Policy** page.

    Beneath the **Activity filters** field, configure the parameters for which the alert will be triggered.

    ![Screenshot of a policy configured to detect multiple failed sign-in attempts within a set time period.](media/multiple-failed-log-on-attempts-policy-example.png)
- High download rate

    You can set your policy so that you receive an alert when there has been an unexpected or uncharacteristic level of downloading activity. To configure this sort of policy, under **Rate** parameters, choose the parameters to trigger the alert.

    ![Screenshot of a policy example configured to detect a high download rate.](media/high-download-rate-example.png)

## Activity policy reference

This section describes activity policy types, their components, and the fields that can be configured for each policy.

An **Activity policy** is an API-based policy that enables you to monitor your organization's activities in the cloud. The policy takes into account over 20 file metadata filters including device type and location. Based on the policy results, notifications can be generated and users can be suspended from the cloud app. Each policy is composed of the following parts:

- Activity filters – Enable you to create granular conditions based on metadata.
- Activity match parameters – Enable you to set a threshold for the number of times an activity repeats to be considered to match the policy. Specify the number of repeated activities required to match the policy. For example, set a policy to alert when a user has 10 unsuccessful login attempts in a 2-minute time frame. By default, **Activity match parameters** raise a match for every single activity that meets all of the activity filters.

    - Using **Repeated activity** you can set the number of repeated activities, the duration of the time frame in which the activities are counted. You can also specify that all activities should be performed by the same user and in the same cloud app.
- Actions – The policy provides a set of governance actions that can be automatically applied when violations are detected.