---
layout: Conceptual
title: Detect suspicious user activity using UEBA - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/tutorial-suspicious-activity
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
description: This tutorial describes the process for tuning user activity detections in Microsoft Defender for Cloud Apps.
ms.date: 2026-02-05T00:00:00.0000000Z
ms.topic: tutorial
locale: en-us
document_id: 84e966b0-6562-205a-c4c0-e7a6e9504abd
document_version_independent_id: 84e966b0-6562-205a-c4c0-e7a6e9504abd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/tutorial-suspicious-activity.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tutorial-suspicious-activity
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/tutorial-suspicious-activity.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/d6f38669-3d05-40f2-afd8-e49f7dd20884
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/55265cca-de9b-48dc-a77a-9047cc39a575
platformId: b7fdc62f-0e5f-11af-7397-7eb41e07964d
---

# Detect suspicious user activity using UEBA - Microsoft Defender for Cloud Apps | Microsoft Learn

Microsoft Defender for Cloud Apps includes detections for compromised users, insider threats, data exfiltration, and ransomware activity. The service uses anomaly detection, user and entity behavior analytics (UEBA), and rule-based activity detections to analyze user activity across connected apps.

Unauthorized or unexpected changes in a cloud environment can introduce security and operational risks. For example, changes to key corporate resources like the servers running your public website or service that you're providing to customers can be compromised.

Defender for Cloud Apps captures and analyzes data from several sources to identify app and user activities in your organization. This analysis gives your security analysts visibility into cloud use. The collected data is correlated, standardized, and enriched with threat intelligence and location details, to provide an accurate, consistent view of suspicious activities.

Before tuning detections, configure the following data sources:

| Source | Description |
| --- | --- |
| **[Activity log](activity-filters)** | Activities from your [API connected apps](enable-instant-visibility-protection-and-governance-actions-for-your-apps). |
| **[Discovery log](tutorial-shadow-it)** | Activities extracted from firewall and proxy traffic log that you forward to Defender for Cloud Apps. The logs are analyzed against the [cloud app catalog](risk-score), ranked, and scored based on more than 90 risk factors. |
| **[Proxy log](proxy-intro-aad)** | Activities from your [conditional access app control apps](tutorial-proxy#phase-1-monitor-user-activities-for-anomalies). |

Fine-tune the following policies by setting filters and dynamic thresholds (UEBA) to train their detection models. You can also set suppressions to reduce common false positive detections:

- Anomaly detection
- Cloud discovery anomaly detection
- Rule-based activity detection

Learn how to tune user activity detections to identify true compromises and reduce unnecessary alerts that result from large volumes of false positive detections:

- Configure IP address ranges
- Tune anomaly detection policies
- Tune cloud discovery anomaly detection policies
- Tune rule-based detection policies
- Configure alerts
- Investigate and remediate

## Phase 1: Configure IP address ranges

- Set up IP ranges to fine-tune any type of suspicious user activity detection policies.

[Setting up known IP addresses](ip-tags) helps machine learning algorithms identify known locations and consider them as part of the machine learning models. For example, adding the IP address range of your VPN helps the model to correctly classify this IP range and automatically exclude it from impossible travel detections because the VPN location doesn't represent the true location of that user.

Note

Defender for Cloud Apps uses IP ranges across the service, not only for detections. IP ranges are used in the activity log, Conditional Access, and more. For example, identifying your physical office IP addresses lets you customize the way you view and investigate logs and alerts.

### Review anomaly detection alerts

Defender for Cloud Apps includes a set of anomaly detection alerts to identify different security scenarios. They start to profile user activity and generate alerts as soon as you connect the relevant [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

Start by familiarizing yourself with the [different detection policies](control-cloud-apps-with-policies). Prioritize the top scenarios that you think are most relevant for your organization, and tune the policies accordingly.

## Phase 2: Tune anomaly detection policies

Defender for Cloud Apps includes several built-in [anomaly detection policies](anomaly-detection-policy#anomaly-detection-policies) that are preconfigured for common security use cases. Popular detections include:

| Detection | Description |
| --- | --- |
| **Impossible travel** | Activities from the same user in different locations within a period that's shorter than the expected travel time between the two locations. |
| **Activity from infrequent country** | Activity from a location that wasn't recently or never visited by the user. |
| **Malware detection** | Scans files in your cloud apps and runs suspicious files through Microsoft's threat intelligence engine to check whether they're associated with known malware. |
| **Ransomware activity** | File uploads to the cloud that might be infected with ransomware. |
| **Activity from suspicious IP addresses** | Activity from an IP address that Microsoft Threat Intelligence identified as risky. |
| **Suspicious inbox forwarding** | Detects suspicious inbox forwarding rules set on a user's inbox. |
| **Unusual multiple file download activities** | Detects multiple file download activities in a single session with respect to the baseline learned, which could indicate an attempted breach. |
| **Unusual administrative activities** | Detects multiple administrative activities in a single session with respect to the baseline learned, which could indicate an attempted breach. |

Note

Some anomaly detections focus on detecting problematic security scenarios, while others help identify and investigate anomalous user behavior that might not necessarily indicate a compromise. For such detections, you can use [Behaviors](behaviors) which is available in the Microsoft Defender advanced hunting experience.

1. **Scope policies to specific users or groups**

    Scoping policies to specific users can help reduce noise from alerts that aren't relevant to your organization. You can [configure each policy to include or exclude specific users and groups](anomaly-detection-policy#scope-anomaly-detection-policies), such as in the following examples:

    - **Attack simulations** Many organizations use a user or a group to constantly simulate attacks. Constantly receiving alerts from these users' activities creates unnecessary noise. Set up your policies to exclude these users or groups. This action helps machine learning models identify these users and fine-tune their dynamic thresholds.
    - **Targeted detections** You might want to investigate a specific group of VIP users like members of an admin or Chief Experience Officer (CXO) group. In this case, create a policy for the activities you want to detect and choose to only include the set of users or groups you're interested in.
2. **Tune anomalous sign-in detections**

    Alerts resulting from [failed sign-in activities](anomaly-detection-policy#multiple-failed-login-attempts) might indicate that someone is attempting to target one or more user accounts.

    Compromised credentials are a common cause of account takeover and unauthorized activity. The [impossible travel](anomaly-detection-policy#impossible-travel), [activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses), and [infrequent country or region](anomaly-detection-policy#activity-from-infrequent-country) detections alerts help you discover activities that suggest an account is potentially compromised.
3. **Tune sensitivity of [impossible travel](anomaly-detection-policy#impossible-travel)**[Configure the sensitivity slider](anomaly-detection-policy#tune-anomaly-detection-policies) that determines the level of suppressions applied to anomalous behavior before triggering an impossible travel alert. Organizations interested in high fidelity should consider increasing the sensitivity level. If your organization has many users that travel, consider lowering the sensitivity level to suppress activities from a user's common locations learned from previous activities. You can choose from the following sensitivity levels:

    - **Low**: System, tenant, and user suppressions
    - **Medium**: System and user suppressions
    - **High**: Only system suppressions

    Where:

    | Suppression type | Description |
    | --- | --- |
    | **System** | Built-in detections that are always suppressed. |
    | **Tenant** | Common activities based on previous activity in the tenant. For example, suppressing activities from an ISP previously alerted on in your organization. |
    | **User** | Common activities based on previous activity of the specific user. For example, suppressing activities from a location that is commonly used by the user. |

## Phase 3: Tune cloud discovery anomaly detection policies

You can fine-tune several built-in [cloud discovery anomaly detection policies](cloud-discovery-policies#cloud-discovery-anomaly-detection) or create your own policies to identify other scenarios worth investigating. These policies use cloud discovery logs, with [tuning capabilities](cloud-discovery-policies#cloud-discovery-anomaly-detection) that focus on anomalous app behavior and data exfiltration.

**Tune usage monitoring**

Set the usage filters to control the scope, and activity period for detecting anomalous behavior. For example, receive alerts for anomalous activities from executive-level employees.

**Tune alert sensitivity**

To reduce unnecessary alerts, set up the sensitivity of alerts. Use the sensitivity slider to control the number of high-risk alerts sent per 1,000 users per week. Higher sensitivities require less variance to be considered an anomaly and generate more alerts. In general, set low sensitivity for users who don't have access to confidential data.

## Phase 4: Tune rule-based detection (activity) policies

[Rule-based detection policies](user-activity-policies) complement anomaly detection policies with organization-specific requirements. Create rule-based policies using one of the Activity policy templates.

If your organization doesn't have any presence in a particular country or region, create a policy that detects the anomalous activities from that location. For organizations with large branches in that country or region, such activities are normal and it doesn't make sense to detect such activities.

1. Go to **Policies** &gt; **Policy templates** and set the **Type** filter to **Activity policy**. [Set up activity filters](activity-filters-queries) to detect behaviors that aren't normal for your environment.
2. **Tune activity volume** Choose the volume of activity required before the detection raises an alert. If your organization has no presence in a country or region, even a single activity is significant and warrants an alert. A single sign-in failure could be human error and only of interest if there are many failures in a short period.
3. **Tune [activity filters](activity-filters-queries)** Set the filters you require to detect the type of activity you want to alert on. For example, to detect activity from a country or region, use the **Location** parameter.
4. **Tune alerts** To reduce unnecessary alerts, set the **daily alert limit**.

## Phase 5: Configure alerts

Note

Microsoft deprecated the Alerts/SMS (text messages) feature on December 15, 2022. If you want to receive text alerts, use Microsoft Power Automate for custom alert automation. For more information, see [Integrate with Microsoft Power Automate for custom alert automation](flow-integration).

To get immediate alerts at any time of the day, choose to receive them through email.

You might also want the ability to analyze alerts in the context of other alerts triggered by other products in your organization. This analysis gives you a holistic view of a potential threat. For example, you might want to correlate between cloud-based and on-premises events to see if there's any other mitigating evidence that confirms an attack.

You can use the [Microsoft Power Automate](flow-integration) to trigger custom alert automation. When an alert is triggered, you can:

- Set up a playbook
- Create an issue in [ServiceNow](/en-us/connectors/service-now/)
- Send an approval email to run a custom governance action when an alert is triggered

Use the following guidelines to configure your alerts:

1. **Email** Choose this option to receive alerts by email.
2. **SIEM** Several SIEM integration options exist, including [Microsoft Sentinel](siem-sentinel), [Microsoft Graph Security API](/en-us/graph/security-integration#list-of-connectors-from-microsoft), and other [generic SIEMs](siem). Choose the integration that best meets your requirements.
3. **Power Automate automation** Create the automation playbooks you require and set it as the policy's alert to Power Automate action.

## Phase 6: Investigate and remediate

To optimize your protection, set up automatic remediation actions to minimize the risk to your organization. The policies let you apply [governance actions](governance-actions) with the alerts so that the risk to your organization is reduced even before you start investigating. The policy type determines the available actions, including actions like pausing a user or blocking access to the requested resource.