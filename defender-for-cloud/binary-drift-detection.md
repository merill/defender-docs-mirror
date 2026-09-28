---
layout: Conceptual
title: Binary drift detection and blocking - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/binary-drift-detection
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
description: Learn how binary drift detecting and blocking can help you detect unauthorized external processes within containers.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: b3f07454-1e60-8a4d-880a-dfeb226a639f
document_version_independent_id: 45a432c2-bf3b-1af2-4a00-b5561266a7f4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/binary-drift-detection.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/binary-drift-detection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/binary-drift-detection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 2f2315a7-e89b-dad0-db5c-a57e8d21478a
---

# Binary drift detection and blocking - Microsoft Defender for Cloud | Microsoft Learn

Binary drift happens when a container runs an executable that didn't come from the original image. This drift can be intentional and legitimate, or it can indicate an attack. Container images should be immutable, so treat processes that start from binaries outside the original image as suspicious activity.

Binary drift detection alerts you when the running container workload differs from the image workload. It detects unauthorized external processes in containers and raises alerts for potential threats. You can define drift policies to control alert conditions and distinguish legitimate activity from suspicious behavior.

Binary drift blocking prevents unauthorized external processes from running in containers. When enabled, it enforces your policies so only approved processes run. This approach helps maintain application integrity and reduces security risk.

Review [binary drift and blocking availability](support-matrix-defender-for-containers#runtime-protection-features).

## Prerequisites

Meet the following requirements before you create or manage binary drift detection and blocking policies.

- Run the Defender for Container sensor.
- **Binary drift blocking only**:
    - AKS: Helm provisioning with sensor version **0.10.2** or above.
    - Multicloud: Helm provisioning with sensor version **0.10.2** or above, or the ARC extension.
- [Enable the Defender for Container sensor](defender-for-containers-azure-enable-portal#configure-plan-components) on the subscriptions and connectors.
- The following roles and permissions:
    - **To create and modify drift policies**: Security Admin or higher permissions on the tenant.
    - **To view drift policies**: Security Reader or higher permissions on the tenant.

## Configure drift and block policies

Create drift and block policies to define when alerts should be generated. Each policy consists of rules that define the conditions for generating alerts. This policy-and-rule structure lets you tailor the feature to your specific needs and reduce false positives. You can create exclusions by setting higher priority rules for specific scopes or clusters, images, pods, Kubernetes labels, or namespaces.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Containers drift policy**.

    [![Screenshot of Select Containers drift policy in Environment settings.](media/binary-drift-detection/select-containers-drift-policy.png)](media/binary-drift-detection/select-containers-drift-policy.png#lightbox)
4. Select the applicable rule:

    - **Alert on Kube-System namespace** - can be modified like any other rule.
    - **Default binary drift** - applies to everything if no other rule matches. You can only modify the actions to either **Drift detection alert**, **Drift detection blocking**, or **Ignore drift detection** (default).

        [![Screenshot of Default rule appears at the bottom of the list of rules.](media/binary-drift-detection/default-rule.png)](media/binary-drift-detection/default-rule.png#lightbox)

## Add a new rule

Binary drift rules define what behavior is considered suspicious, what to alert on, and what to block. Add a new rule to enforce better control, different enforcement levels, or more granular security behavior for specific workloads. You can also set blocking rules to prevent unauthorized processes from running in your containers.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Containers drift policy**.
4. Select **Add rule**.

    [![Screenshot of Select Add rule to create and configure a new rule.](media/binary-drift-detection/add-rule.png)](media/binary-drift-detection/add-rule.png#lightbox)
5. Define the following fields:

    - **Rule name**: A descriptive name for the rule.
    - **Action**:

        - **Drift detection alert** if the rule should generate an alert.
        - **Drift detection blocking** if the rule should block the drifted process.
        - **Ignore drift detection** to exclude it from alert generation.
    - **Scope description**: A description of the scope to which the rule applies.
    - **Cloud scope**: The cloud provider to which the rule applies. You can choose any combination of Azure, Amazon Web Services (AWS), or Google Cloud Platform (GCP). If you expand a cloud provider, you can select specific subscription. If you don't select the entire cloud provider, new subscriptions added to the cloud provider aren't included in the rule.
    - **Resource scope**: Add conditions based on the following categories: **Container name**, **Image name**, **Namespace**, **Pod labels**, **Pod name**, or **Cluster name**. Then choose an operator: **Starts with**, **Ends with**, **Equals**, or **Contains**. Finally, enter the value to match. You can add as many conditions as needed by selecting **+Add condition**.
    - **Allow list for processes**: A list of processes that are allowed to run in the container. Any process not on this list detected, generates an alert.

        Sample rule that allows the `dev1.exe` process to run in containers in the Azure cloud scope, whose image names start with either *Test123* or *env123*:

        [![Example of a rule configuration with all the fields defined.](media/binary-drift-detection/rule-configuration.png)](media/binary-drift-detection/rule-configuration.png#lightbox)
6. Select **Apply**.
7. Assign priority to the rule by moving the rule up or down on the list. The rule with the highest priority is evaluated first. If there's a match, the evaluation stops. If no match is found, the next rule is evaluated. If there's no match for any rule, the default rule is applied.
8. Select **Save**.

Within 30 minutes, the sensors on the protected clusters update by using the new policy.

## Manage a rule

Binary drift policies are flexible and customizable, allowing you to manage and adjust them as needed. You can edit rules to refine their conditions or actions, duplicate rules to create similar ones with minor changes, or delete rules that are no longer necessary. Regularly reviewing and managing your rules ensures that your binary drift detection and blocking policies remain effective and aligned with your security needs.

# [Edit an existing drift detection rule](#tab/edit-rule)
Rules can be edited to refine their conditions or actions. The ability to edit rule conditions or actions allows you to adjust your policies based on the alerts you receive and your review of them, ensuring that they effectively balance security needs with operational efficiency.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Containers drift policy**.
4. Select a rule.
5. Select **Edit**.
6. Select **Save**.

Within 30 minutes, the sensors on the protected clusters update by using the new policy.

# [Duplicate an existing drift detection rule](#tab/duplicate-rule)
Rules can be duplicated to create similar ones with minor changes. Duplicating a rule is useful if you want to create a new rule that is similar to an existing one, allowing you to save time and maintain consistency in your policies.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Containers drift policy**.
4. Select a rule.
5. Select **Duplicate rule**.
6. Select **Save**.

Within 30 minutes, the sensors on the protected clusters update by using the new policy.

# [Delete a drift detection rule](#tab/delete-rule)
Rules can be deleted when they are no longer necessary or if they generate too many false positives. Regularly reviewing and cleaning up your rules helps maintain the effectiveness of your binary drift detection and blocking policies.

Warning

Deleting a rule removes its enforcement conditions and can change alerting or blocking behavior for matching workloads. Make sure the rule is no longer needed before you proceed.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Containers drift policy**.
4. Select a rule.
5. Select **Delete rule**.
6. Select **Save**.

Within 30 minutes, the sensors on the protected clusters update by using the new policy.

---

## Additional information

Defender for Cloud's alerts notify you of any binary drifts, so you can maintain the integrity of your container images. If the system detects an unauthorized external process that matches your defined policy conditions, it generates a high-severity alert for you to review. If you configure blocking rules, the system blocks the execution of those unauthorized processes.

Based on the alerts generated and your review of them, you might need to adjust your rules in the binary drift or blocking policy. Adjusting the binary drift or blocking policy could involve refining conditions, adding new rules, or removing ones that generate too many false positives. The goal is to ensure that the defined binary drift and blocking policies with their rules effectively balance security needs with operational efficiency.

The effectiveness of binary drift detection and blocking relies on your active engagement in configuring, monitoring, and adjusting policies to suit your environment's unique requirements.