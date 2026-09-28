---
layout: Conceptual
title: Enable cloud infrastructure entitlement management (CIEM) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-permissions-management
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
description: Enable CIEM to enforce least privilege access and manage user entitlements across Azure, AWS, and GCP as part of Defender for Cloud's CNAPP solution.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: ced8d1d0-90f5-fe06-ceca-c4d95b4bf555
document_version_independent_id: c5211bed-9017-cd2d-1b2d-36f27cbc1757
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/enable-permissions-management.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/enable-permissions-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/enable-permissions-management.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: aec75ec0-e415-fd0d-0e8c-76070ecb2162
---

# Enable cloud infrastructure entitlement management (CIEM) - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud provides a cloud infrastructure entitlement management (CIEM) security model. It helps organizations manage and control user access and entitlements in cloud infrastructure. CIEM is a core part of the Cloud Native Application Protection Platform (CNAPP) solution. It shows who or what has access to resources and helps enforce least-privilege access. With CIEM, users and workload identities get only the access they need to do their tasks. CIEM also helps you monitor and manage permissions across Azure, Amazon Web Services (AWS), and Google Cloud Platform (GCP).

This article explains how to enable CIEM for Azure, AWS, and GCP in Defender for Cloud. Before you begin, review the prerequisites to make sure your environment is ready.

## Before you start

Before you enable CIEM, make sure you meet the following prerequisites. Permissions Management is the CIEM extension in Defender cloud security posture management (Defender CSPM) that lets you analyze and manage identity permissions.

1. Make sure you have the right roles and permissions for each cloud environment to enable the Permissions Management (CIEM) extension in Defender CSPM:

    - For AWS and GCP, you need the [Security Admin role](/en-us/azure/role-based-access-control/built-in-roles/security#security-admin) at the account or organization level.
    - For Azure, you need the [Security Admin role](/en-us/azure/role-based-access-control/built-in-roles/security#security-admin) at the subscription level.
2. Onboard your AWS or GCP environment to Defender for Cloud:

    - For AWS, [connect your AWS account to Defender for Cloud](quickstart-onboard-aws).
    - For GCP, [connect your GCP project to Defender for Cloud](quickstart-onboard-gcp).
3. [Enable Defender CSPM](tutorial-enable-cspm-plan) on your Azure subscription, AWS account, or GCP project.

## Enable CIEM for Azure

When you enable the Defender CSPM plan on your Azure account, the **Azure CSPM**[regulatory compliance standard](concept-regulatory-compliance-standards) is assigned to your subscription. This standard includes CIEM recommendations.

If CIEM is turned off, these recommendations aren't calculated.

To enable CIEM for Azure:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Navigate to **Environment settings**.
4. Select the relevant subscription.
5. Locate the Defender CSPM plan and select **Settings**.
6. Enable **Permissions Management (CIEM)**.

    [![Screenshot that shows you where the toggle is for the permissions management is located.](media/enable-permissions-management/permissions-management-on.png)](media/enable-permissions-management/permissions-management-on.png#lightbox)
7. Select **Continue**.
8. Select **Save**.

The applicable CIEM recommendations appear on your subscription within a few hours.

List of Azure recommendations:

- Azure overprovisioned identities should have only the necessary permissions
- Permissions of inactive identities in your Azure subscription should be revoked

## Enable CIEM for AWS

Note

Starting August 6, 2026, to improve performance and scalability, Microsoft Defender for Cloud will no longer publish unused permission action details for the **AWS overprovisioned identities should have only the necessary permissions** recommendation. The recommendation will continue to identify overprovisioned identities, but the detailed list of unused AWS permission actions won't be calculated or shown in Defender for Cloud. This change helps reduce assessment payload size and improve recommendation performance, especially for environments with a large number of identities, permissions, or multi-cloud connectors. If you need to review unused AWS permissions, use AWS IAM last accessed information directly in AWS. AWS IAM provides last accessed details for users, roles, groups, and policies to help you identify permissions that haven't been used and right-size access. To review unused permissions in AWS:

1. Sign in to the AWS Management Console.
2. Open the IAM console.
3. In the navigation pane, select **Users**, **Roles**, **User groups**, or **Policies**.
4. Select the relevant identity or policy.
5. Open the **Last Accessed** tab.
6. Review services and supported actions that were not accessed during the AWS tracking period. For more information, see [View last accessed information for IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_last-accessed-view-data.html) and [Refine permissions in AWS using last accessed information.](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_last-accessed.html)

When you enable the Defender CSPM plan on your AWS account, the **AWS CSPM**[regulatory compliance standard](concept-regulatory-compliance-standards) is automatically assigned to your subscription. The AWS CSPM standard provides CIEM recommendations. When Permissions Management is disabled, the CIEM recommendations in the AWS CSPM standard aren't calculated. When you enable the Defender CSPM plan on your AWS account, the **AWS CSPM**[regulatory compliance standard](concept-regulatory-compliance-standards) is added to your subscription. This standard includes CIEM recommendations. If Permissions Management (CIEM) is turned off, these recommendations aren't calculated.

To enable CIEM for AWS:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Navigate to **Environment settings**.
4. Select the relevant AWS account.
5. Locate the Defender CSPM plan and select **Settings**.

    [![Screenshot that shows an AWS account and the Defender CSPM plan enabled and where the settings button is located.](media/enable-permissions-management/settings.png)](media/enable-permissions-management/settings.png#lightbox)
6. Enable **Permissions Management (CIEM)**.
7. [Ingest AWS CloudTrail logs](/en-us/azure/defender-for-cloud/integrate-cloud-trail) to get more accurate CIEM recommendations and insights.
8. Select **Configure access**.
9. Select a deployment method.
10. Run the CloudFormation deployment script on your AWS environment by using the onscreen instructions.
11. Check the **CloudFormation template has been updated on AWS environment (Stack)** checkbox.

    ![Screenshot that shows where the checkbox is located on the screen.](media/enable-permissions-management/checkbox.png)
12. Select **Review and generate**.
13. Select **Update**.

The applicable CIEM recommendations appear on your AWS account within a few hours.

List of AWS recommendations:

- AWS overprovisioned identities should have only the necessary permissions
- Permissions of inactive identities in your AWS account should be revoked

## Enable CIEM for GCP

Note

Starting August 6, 2026, to improve performance and scalability, Microsoft Defender for Cloud will no longer publish unused permission action details for the **GCP overprovisioned identities should have only necessary permissions** recommendation. The recommendation will continue to identify overprovisioned identities, but the detailed list of unused GCP permission actions won't be calculated or shown in Defender for Cloud. This change helps reduce assessment payload size and improve recommendation performance, especially for environments with a large number of identities, permissions, or multi-cloud connectors. If you need to review unused GCP permissions, use Google Cloud Policy Intelligence and IAM role recommendations directly in Google Cloud. Google Cloud policy insights can help identify principals with permissions they don't need, and role recommendations can help right-size access. To review unused permissions in GCP:

1. Sign in to the Google Cloud console.
2. Go to the **IAM** page.
3. Select the relevant project, folder, or organization.
4. Review the **Security insights** column for policy insights about excess or unused permissions.
5. Review IAM role recommendations to determine whether a role should be removed or replaced with a more appropriate role. For more information, see [Manage policy insights for projects, folders, and organizations](https://docs.cloud.google.com/policy-intelligence/docs/policy-insights) and [IAM role recommendations overview](https://docs.cloud.google.com/policy-intelligence/docs/role-recommendations-overview).

When you enable the Defender CSPM plan on your GCP project, the **GCP CSPM**[regulatory compliance standard](concept-regulatory-compliance-standards) is automatically assigned to your subscription. The GCP CSPM standard provides CIEM recommendations. When you enable the Defender CSPM plan on your GCP project, the **GCP CSPM**[regulatory compliance standard](concept-regulatory-compliance-standards) is added to your subscription. This standard includes CIEM recommendations.

If you disable Permissions Management (CIEM), Defender for Cloud doesn't calculate these recommendations.

To enable CIEM for GCP:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Navigate to **Environment settings**.
4. Select the relevant GCP project.
5. Locate the Defender CSPM plan and select **Settings**.

    [![Screenshot that shows where to select settings for the Defender CSPM plan for your GCP project.](media/enable-permissions-management/settings-google.png)](media/enable-permissions-management/settings-google.png#lightbox)
6. Toggle Permissions Management (CIEM) to **On**.
7. [Ingest GCP cloud logging](/en-us/azure/defender-for-cloud/enable-permissions-management) to ensure your GCP identities are evaluated for permission risks.
8. Select **Save**.
9. Select **Next: Configure access**.
10. Select the relevant permissions type.
11. Select a deployment method.
12. Run the Cloud Shell or Terraform deployment script on your GCP environment by using the onscreen instructions.
13. Add a check to the **I ran the deployment template for the changes to take effect** checkbox.

    [![Screenshot that shows the checkbox that needs to be selected.](media/enable-permissions-management/gcp-checkbox.png)](media/enable-permissions-management/gcp-checkbox.png#lightbox)
14. Select **Review and generate**.
15. Select **Update**.

The applicable CIEM recommendations appear on your GCP project within a few hours.

List of GCP recommendations:

- GCP overprovisioned identities should have only necessary permissions
- Permissions of inactive identities in your GCP project should be revoked

## Limitations

Be aware of the following CIEM limitations:

- Serverless and compute identities for AWS are no longer included in CIEM inactivity logic, which can change recommendation counts.
- The Permissions Creep Index (PCI) metric is being deprecated and will no longer appear in Defender for Cloud recommendations.