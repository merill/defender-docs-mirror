---
layout: Conceptual
title: Improve regulatory compliance in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/regulatory-compliance-dashboard
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
description: Learn how to improve regulatory compliance in Microsoft Defender for Cloud.
ms.topic: tutorial
ms.date: 2025-07-15T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 75087a1f-ca9d-bd06-5159-326afa6b18fb
document_version_independent_id: c3d247e2-8b60-d861-bba8-9f9414d6623d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/regulatory-compliance-dashboard.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/regulatory-compliance-dashboard
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/regulatory-compliance-dashboard.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 587fe98a-26c8-b7a4-09fe-68241cbf8d2b
---

# Improve regulatory compliance in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud helps you to meet regulatory compliance requirements by continuously assessing resources against compliance controls, and identifying issues that are blocking you from achieving a particular compliance certification.

In the Regulatory compliance dashboard, you manage and interact with compliance standards. You can see which compliance standards are assigned, turn standards on and off for Azure, AWS, and GCP, review the status of assessments against standards, and more.

## Integration with Purview

Compliance data from Defender for Cloud now seamlessly integrates with [Microsoft Purview Compliance Manager](/en-us/microsoft-365/compliance/compliance-manager), allowing you to centrally assess and manage compliance across your organization's entire digital estate.

When you add any standard to your compliance dashboard (including compliance standards monitoring other clouds like AWS and GCP), the resource-level compliance data is automatically surfaced in Compliance Manager for the same standard.

Compliance Manager thus provides improvement actions and status across your cloud infrastructure and all other digital assets in this central tool. For more information, see [multicloud support in Microsoft Purview Compliance Manager](/en-us/microsoft-365/compliance/compliance-manager-multicloud).

## Before you start

- By default, when you enable Defender for Cloud on an Azure subscription, AWS account, or GCP plan, the MCSB plan is enabled.
- You can add more non-default compliance standards when at least one paid plan is enabled in Defender for Cloud.
- You must be signed in with an account that has reader access to the policy compliance data. The **Reader** role for the subscription has access to the policy compliance data, but the **Security Reader** role doesn't. At a minimum, you need to have **Resource Policy Contributor** and **Security Admin** roles assigned.

## Assess regulatory compliance

The Regulatory compliance dashboard shows which compliance standards are enabled. It shows the controls within each standard, and security assessments for those controls. The status of these assessments reflects your compliance with the standard.

The dashboard helps you to focus on gaps in standards, and to monitor compliance over time.

1. In the Defender for Cloud portal, open the **Regulatory compliance** page.

    [![Screenshot that shows the exploration of the details of compliance with a specific standard.](media/regulatory-compliance-dashboard/compliance-drilldown.png)](media/regulatory-compliance-dashboard/compliance-drilldown.png#lightbox)
2. Use the dashboard in accordance with the numbered items in the image.

    - (1). Select a compliance standard to see a list of all controls for that standard.
    - (2). View the subscriptions on which the compliance standard is applied.
    - (3). Select and expand a control to view the assessments associated with it. Select an assessment to view the associated resources, and possible remediation actions.
    - (4). Select **Control details** to view the **Overview**, **Your Actions**, and **Microsoft Actions** tabs.
    - (5). In **Your Actions**, you can see the automated and manual assessments associated with the control.
    - (6). Automated assessments show the number of failed resources and resource types, and link you directly to the remediation information.
    - (7). Manual assessments can be manually attested, and evidence can be linked to demonstrate compliance.

## Investigate issues

You can use information in the dashboard to investigate issues that might affect compliance with the standard.

1. In the Defender for Cloud portal, open **Regulatory compliance**.
2. Select a regulatory compliance standard, and select a compliance control to expand it.
3. Select **Control details**.

    [![Screenshot that shows you where to navigate to select control details on the screen.](media/regulatory-compliance-dashboard/control-detail.png)](media/regulatory-compliance-dashboard/control-detail.png#lightbox)

    - Select **Overview** to see the specific information about the Control you selected.
    - Select **Your Actions** to see a detailed view of automated and manual actions you need to take to improve your compliance posture.
    - Select **Microsoft Actions** to see all the actions Microsoft took to ensure compliance with the selected standard.
4. Under **Your Actions**, you can select a down arrow to view more details and resolve the recommendation for that resource.

    [![Screenshot that shows you where the down arrow is on the screen.](media/regulatory-compliance-dashboard/down-arrow.png)](media/regulatory-compliance-dashboard/down-arrow.png#lightbox)

    For more information about how to apply recommendations, see [Implementing security recommendations in Microsoft Defender for Cloud](review-security-recommendations).

    Note

    Assessments run approximately every 12 hours, so you'll see the impact on your compliance data only after the next run of the relevant assessment.

## Remediate an automated assessment

The regulatory compliance has both automated and manual assessments that might need to be remediated. Using the information in the regulatory compliance dashboard, improve your compliance posture by resolving recommendations directly within the dashboard.

1. In the Defender for Cloud portal, open **Regulatory compliance**.
2. Select a regulatory compliance standard, and select a compliance control to expand it.
3. Select any of the failing assessments that appear in the dashboard to view the details for that recommendation. Each recommendation includes a set of remediation steps to resolve the issue.
4. Select a particular resource to view more details and resolve the recommendation for that resource. For example, in the **Azure CIS 1.1.0** standard, select the recommendation **Disk encryption should be applied on virtual machines**.

    [![Screenshot that shows that selecting a recommendation from a standard leads directly to the recommendation details page.](media/regulatory-compliance-dashboard/sample-recommendation.png)](media/regulatory-compliance-dashboard/sample-recommendation.png#lightbox)
5. In this example, when you select **Take action** from the recommendation details page, you arrive in the Azure Virtual Machine pages of the Azure portal, where you can enable encryption from the **Security** tab:

    [![Screenshot that shows the take action button on the recommendation details page leads to the remediation options.](media/regulatory-compliance-dashboard/encrypting-vm-disks.png)](media/regulatory-compliance-dashboard/encrypting-vm-disks.png#lightbox)

    For more information about how to apply recommendations, see [Implementing security recommendations in Microsoft Defender for Cloud](review-security-recommendations).
6. After you take action to resolve recommendations, you'll see the result in the compliance dashboard report because your compliance score improves.

Assessments run approximately every 12 hours, so you'll see the impact on your compliance data only after the next run of the relevant assessment.

## Remediate a manual assessment

The regulatory compliance has automated and manual assessments that might need to be remediated. Manual assessments are assessments that require input from the customer to remediate them.

1. In the Defender for Cloud portal, open **Regulatory compliance**.
2. Select a regulatory compliance standard, and select a compliance control to expand it.
3. Under the **Manual attestation and evidence** section, select an assessment.
4. Select the relevant subscriptions.
5. Select **Attest**.
6. Enter the relevant information and attach evidence for compliance.
7. Select **Save**.

## Generate compliance status reports and certificates

1. To generate a PDF report with a summary of your current compliance status for a particular standard, select **Download report**.

    The report provides a high-level summary of your compliance status for the selected standard based on Defender for Cloud assessments data. The report's organized according to the controls of that particular standard. The report can be shared with relevant stakeholders, and might provide evidence to internal and external auditors.

    [![Screenshot that shows using the toolbar in Defender for Cloud's regulatory compliance dashboard to download compliance reports.](media/regulatory-compliance-dashboard/download-report.png)](media/regulatory-compliance-dashboard/download-report.png#lightbox)
2. To download Azure and Dynamics **certification reports** for the standards applied to your subscriptions, use the **Audit reports** option.

    [![Screenshot that shows using the toolbar in Defender for Cloud's regulatory compliance dashboard to download Azure and Dynamics certification reports.](media/release-notes/audit-reports-regulatory-compliance-dashboard.png)](media/release-notes/audit-reports-regulatory-compliance-dashboard.png#lightbox)
3. Select the tab for the relevant reports types (PCI, SOC, ISO, and others) and use filters to find the specific reports you need:

    [![Screenshot that shows filtering the list of available Azure Audit reports using tabs and filters.](media/release-notes/audit-reports-list-regulatory-compliance-dashboard-ga.png)](media/release-notes/audit-reports-list-regulatory-compliance-dashboard-ga.png#lightbox)

    For example, from the PCI tab you can download a ZIP file containing a digitally signed certificate demonstrating Microsoft Azure, Dynamics 365, and Other Online Services' compliance with ISO22301 framework, together with the necessary collateral to interpret and present the certificate.

When you download one of these certification reports, you're shown the following privacy notice:

*By downloading this file, you're giving consent to Microsoft to store the current user and the selected subscriptions at the time of download. This data is used in order to notify you if there are changes or updates to the downloaded audit report. This data is used by Microsoft and the audit firms that produce the certification/reports only when notification is required.*

## Continuously export compliance status

If you want to track your compliance status with other monitoring tools in your environment, Defender for Cloud includes an export mechanism to make this straightforward. Configure **continuous export** to send select data to an Azure Event Hubs or a Log Analytics workspace. Learn more in [continuously export Defender for Cloud data](continuous-export).

Use continuous export data to an Azure Event Hubs or a Log Analytics workspace:

1. Export all regulatory compliance data in a **continuous stream**:

    [![Screenshot that shows how to continuously export a stream of regulatory compliance data.](media/regulatory-compliance-dashboard/export-compliance-data-stream.png)](media/regulatory-compliance-dashboard/export-compliance-data-stream.png#lightbox)
2. Export **weekly snapshots** of your regulatory compliance data:

    [![Screenshot that shows how to continuously export a weekly snapshot of regulatory compliance data.](media/regulatory-compliance-dashboard/export-compliance-data-snapshot.png)](media/regulatory-compliance-dashboard/export-compliance-data-snapshot.png#lightbox)

Tip

You can also manually export reports about a single point in time directly from the regulatory compliance dashboard. Generate these **PDF/CSV reports** or **Azure and Dynamics certification reports** using the **Download report** or **Audit reports** toolbar options.

## Trigger a workflow when assessments change

Defender for Cloud's workflow automation feature can trigger Logic Apps whenever one of your regulatory compliance assessments changes state.

For example, you might want Defender for Cloud to email a specific user when a compliance assessment fails. You need to first create the logic app (using [Azure Logic Apps](/en-us/azure/logic-apps/logic-apps-overview)) and then set up the trigger in a new workflow automation as explained in [Automate responses to Defender for Cloud triggers](workflow-automations).

[![Screenshot that shows how to use changes to regulatory compliance assessments to trigger a workflow automation.](media/release-notes/regulatory-compliance-triggers-workflow-automation.png)](media/release-notes/regulatory-compliance-triggers-workflow-automation.png#lightbox)