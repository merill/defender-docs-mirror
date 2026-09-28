---
layout: Conceptual
title: Azure Monitor workbooks with Defender for Cloud data - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/custom-dashboards-azure-workbooks
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
description: Learn how to create rich, interactive reports for your Microsoft Defender for Cloud data by using workbooks from the integrated Azure Monitor workbooks gallery.
ms.topic: concept-article
ms.date: 2025-08-14T00:00:00.0000000Z
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 3c45a1b9-ea55-1d6c-eeb2-a4a37ba7af0a
document_version_independent_id: 79dbfa1c-e2b0-5f40-42d6-38c1b3620dea
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/custom-dashboards-azure-workbooks.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/custom-dashboards-azure-workbooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/custom-dashboards-azure-workbooks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 13a45ad4-4c2a-256f-8616-a58a2fec0501
---

# Azure Monitor workbooks with Defender for Cloud data - Microsoft Defender for Cloud | Microsoft Learn

[Azure workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview) are flexible canvas that you can use to analyze data and create rich, visual reports in the Azure portal. In workbooks, you can access multiple data sources across Azure. Combine workbooks into unified, interactive experiences.

Workbooks provide a rich set of capabilities for visualizing your Azure data. For detailed information about each visualization type, see the [visualizations examples and documentation](/en-us/azure/azure-monitor/visualize/workbooks-text-visualizations).

In Microsoft Defender for Cloud, you can access built-in workbooks to track your organization’s security posture. You can also build custom workbooks to view a wide range of data from Defender for Cloud or other supported data sources.

![Screenshot that shows the Secure Score Over Time workbook.](media/custom-dashboards-azure-workbooks/secure-score-over-time-snip.png)

For pricing, see the [pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

## Prerequisites

**Required roles and permissions**: To save a workbook, you must have at least [Workbook Contributor](/en-us/azure/role-based-access-control/built-in-roles#workbook-contributor) permissions for the relevant resource group.

## Use Defender for Cloud gallery workbooks

In Defender for Cloud, you can use integrated Azure workbooks functionality to build custom, interactive workbooks that display your security data. Defender for Cloud includes a workbooks gallery that has the following workbooks ready for you to customize:

- Coverage workbook: Track the coverage of Defender for Cloud plans and extensions across your environments and subscriptions.
- Secure Score Over Time workbook: Track your subscription scores and changes to recommendations for your resources.
- System Updates workbook: View missing system updates by resource, OS, severity, and more.
- Vulnerability Assessment Findings workbook: View the findings of vulnerability scans of your Azure resources.
- Compliance Over Time workbook: View the status of a subscription's compliance with regulatory standards or industry standards that you select.
- Active Alerts workbook: View active alerts by severity, type, tag, MITRE ATT&CK tactics, and location.
- Price Estimation workbook: View monthly, consolidated price estimations for plans in Defender for Cloud, based on the resource telemetry in your environment. The numbers are estimates that are based on retail prices and don't represent actual billing or invoice data.
- Governance workbook: Use the governance report in the governance rules settings to track progress of the rules that affect your organization.
- DevOps Security (preview) workbook: View a customizable foundation that helps you visualize the state of your DevOps posture for the connectors that you set up.

Along with built-in workbooks, you can find useful workbooks in the **Community** category. These workbooks are provided as-is and have no SLA or support. You can choose one of the provided workbooks or create your own workbook.

![Screenshot that shows the gallery of built-in workbooks in Microsoft Defender for Cloud.](media/custom-dashboards-azure-workbooks/workbooks-gallery-microsoft-defender-for-cloud.png)

Tip

To customize any of the workbooks, select the **Edit** button. When you're done editing, select **Save**. The changes are saved in a new workbook.

![Screenshot that shows how to edit a supplied workbook to customize it for your needs.](media/custom-dashboards-azure-workbooks/editing-supplied-workbooks.png)

### Coverage workbook

If you enable Defender for Cloud across multiple subscriptions and environments (Azure, Amazon Web Services, and Google Cloud Platform), you might find it challenging to keep track of which plans are active. It's especially true if you have multiple subscriptions and environments.

The Coverage workbook helps you keep track of which Defender for Cloud plans are active in which parts of your environments. This workbook can help you ensure that your environments and subscriptions are fully protected. By having access to detailed coverage information, you can identify areas that might need more protection so that you can take action to address those areas.

[![Screenshot that shows the Coverage workbook, which displays the plans and extensions that are enabled in various subscriptions and environments.](media/custom-dashboards-azure-workbooks/coverage.png)](media/custom-dashboards-azure-workbooks/coverage.png#lightbox)

In this workbook, you can select a subscription (or all subscriptions), and then view the following tabs:

- **Additional information**: Shows release notes and an explanation of each toggle.
- **Relative coverage**: Shows the percentage of subscriptions or connectors that have a specific Defender for Cloud plan enabled.
- **Absolute coverage**: Shows each plan's status per subscription.
- **Detailed coverage**: Shows additional settings that can be enabled or that must need to be enabled on relevant plans to get each plan's full value.

You also can select the Azure, Amazon Web Services, or Google Cloud Platform environment in each or all subscriptions to see which plans and extensions are enabled for the environments.

### Secure Score Over Time workbook

The Secure Score Over Time workbook uses secure score data from your Log Analytics workspace. The data must be exported by using the continuous export tool as described in [Set up continuous export for Defender for Cloud in the Azure portal](continuous-export?tabs=azure-portal).

When you set up continuous export, under **Export frequency**, select both **Streaming updates** and **Snapshots (Preview)**.

![Screenshot that shows the export frequency options to select for continuous export in the Secure Score Over Time workbook.](media/custom-dashboards-azure-workbooks/export-frequency-both.png)

Note

Snapshots are exported weekly. There's a delay of at least one week after the first snapshot is exported before you can view data in the workbook.

Tip

To configure continuous export across your organization, use the provided `DeployIfNotExist` policies in Azure Policy that are described in [Set up continuous export at scale](continuous-export?tabs=azure-policy).

The Secure Score Over Time workbook has five graphs for the subscriptions that report to the selected workspaces:

| Graph | Example |
| --- | --- |
| **Score trends for the last week and month**Use this section to monitor the current score and general trends of the scores for your subscriptions. | ![Screenshot that shows trends for secure score on the built-in workbook.](media/custom-dashboards-azure-workbooks/secure-score-over-time-table-1.png) |
| **Aggregated score for all selected subscriptions**Hover your mouse over any point in the trend line to see the aggregated score at any date in the selected time range. | ![Screenshot that shows an aggregated score for all selected subscriptions.](media/custom-dashboards-azure-workbooks/secure-score-over-time-table-2.png) |
| **Recommendations with the most unhealthy resources**This table helps you triage the recommendations that had the most resources that changed to an unhealthy status in the selected period. | ![Screenshot that shows recommendations that have the most unhealthy resources.](media/custom-dashboards-azure-workbooks/secure-score-over-time-table-3.png) |
| **Scores for specific security controls**The security controls in Defender for Cloud are logical groupings of recommendations. This chart shows you at a glance the weekly scores for all your controls. | ![Screenshot that shows scores for your security controls over the selected time period.](media/custom-dashboards-azure-workbooks/secure-score-over-time-table-4.png) |
| **Resources changes**Recommendations that have the most resources that changed state (healthy, unhealthy, or not applicable) during the selected period are listed here. Select any recommendation in the list to open a new table that lists the specific resources. | ![Screenshot that shows recommendations that have the most resources that changed health state during the selected period.](media/custom-dashboards-azure-workbooks/secure-score-over-time-table-5.png) |

### System Updates workbook

The System Updates workbook is based on the security recommendation that system updates should be installed on your machines. The workbook helps you identify machines that have updates to apply.

You can view the update status for selected subscriptions by:

- A list of resources that have outstanding updates to apply.
- A list of updates that are missing from your resources.

![Defender for Cloud's system updates workbook based on the missing updates security recommendation.](media/custom-dashboards-azure-workbooks/system-updates-report.png)

### Vulnerability Assessment Findings workbook

Defender for Cloud includes vulnerability scanners for your machines, containers in container registries, and computers running SQL Server.

Learn more about using these scanners:

- [Find vulnerabilities with Microsoft Defender Vulnerability Management](deploy-vulnerability-assessment-defender-vulnerability-management)
- [Scan your SQL resources for vulnerabilities](defender-for-sql-on-machines-vulnerability-assessment)

Findings for each resource type are reported in separate recommendations:

- [Vulnerabilities in your virtual machines should be remediated](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/1195afff-c881-495e-9bc5-1486211ae03f) (includes findings from Microsoft Defender Vulnerability Management, the integrated Qualys scanner, and any configured [BYOL VA solutions](deploy-vulnerability-assessment-byol-vm))
- [Container registry images should have vulnerability findings resolved](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/dbd0cb49-b563-45e7-9724-889e799fa648)
- [SQL databases should have vulnerability findings resolved](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/82e20e14-edc5-4373-bfc4-f13121257c37)
- [SQL servers on machines should have vulnerability findings resolved](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/f97aa83c-9b63-4f9a-99f6-b22c4398f936)

The Vulnerability Assessment Findings workbook gathers these findings and organizes them by severity, resource type, and category.

![Screenshot that shows the Defender for Cloud vulnerability assessment findings report.](media/custom-dashboards-azure-workbooks/vulnerability-assessment-findings-report.png)

### Compliance Over Time workbook

Microsoft Defender for Cloud continually compares the configuration of your resources with requirements in industry standards, regulations, and benchmarks. Built-in standards include NIST SP 800-53, SWIFT CSP CSCF v2020, Canada Federal PBMM, HIPAA HITRUST, and more. You can select standards that are relevant to your organization by using the regulatory compliance dashboard. Learn more in [Customize the set of standards in your regulatory compliance dashboard](assign-regulatory-compliance-standards).

The Compliance Over Time workbook tracks your compliance status over time by using the various standards that you add to your dashboard.

![Screenshot that shows how to select the standards for your Compliance Over Time report.](media/custom-dashboards-azure-workbooks/compliance-over-time-select-standards.png)

When you select a standard from the overview area of the report, the lower pane displays a more detailed breakdown:

![Screenshot that shows how to a detailed breakdown of the changes regarding a specific standard.](media/custom-dashboards-azure-workbooks/compliance-over-time-details.png)

To view the resources that passed or failed each control, you can keep drilling down, all the way to the recommendation level.

Tip

For each panel of the report, you can export the data to Excel by using the **Export to Excel** option.

![Screenshot that shows how to export a compliance workbook data to Excel.](media/custom-dashboards-azure-workbooks/export-workbook-data.png)

### Active Alerts workbook

The Active Alerts workbook displays the active security alerts for your subscriptions on one dashboard. Security alerts are the notifications that Defender for Cloud generates when it detects threats against your resources. Defender for Cloud prioritizes and lists the alerts with the information that you need to quickly investigate and remediate.

This workbook benefits you by helping you be aware of and prioritize the active threats in your environment.

Note

Most workbooks use Azure Resource Graph to query data. For example, to display a map view, data is queried in a Log Analytics workspace. [Continuous export](continuous-export) should be enabled. Export the security alerts to the Log Analytics workspace.

You can view active alerts by severity, resource group, and tag.

![Screenshot that shows a sample view of the alerts viewed by severity, resource group, and tag.](media/custom-dashboards-azure-workbooks/active-alerts-pie-charts.png)

You can also view your subscription's top alerts by attacked resources, alert types, and new alerts.

![Screenshot that highlights the top alerts for your subscriptions.](media/custom-dashboards-azure-workbooks/top-alerts.png)

To see more details about an alert, select the alert.

![Screenshot that shows all high-severity active alerts for a specific resource.](media/custom-dashboards-azure-workbooks/active-alerts-high.png)

The **MITRE ATT&CK tactics** tab lists alerts in the order of the "kill chain" and the number of alerts that the subscription has at each stage.

![Screenshot that shows the order of the chain and the number of alerts.](media/custom-dashboards-azure-workbooks/mitre-attack-tactics.png)

You can see all the active alerts in a table and filter by columns.

![Screenshot that shows the table of active alerts.](media/custom-dashboards-azure-workbooks/active-alerts-table.png)

To see details for a specific alert, select the alert in the table, and then select the **Open Alert View** button.

![Screenshot that shows an alert's details and the Open Alert View button.](media/custom-dashboards-azure-workbooks/alert-details-screen.png)

To see all alerts by location in a map view, select the **Map View** tab.

![Screenshot that shows the alerts when viewed in a map in Map View.](media/custom-dashboards-azure-workbooks/alerts-map-view.png)

Select a location on the map to view all the alerts for that location.

![Screenshot that shows the alerts in a specific location in Map View.](media/custom-dashboards-azure-workbooks/map-alert-details.png)

To view the details for an alert, select an alert, and then select the **Open Alert View** button.

### DevOps Security workbook

The DevOps Security workbook provides a customizable visual report of your DevOps security posture. You can use this workbook to view insights about your repositories that have the highest number of common vulnerabilities and exposures (CVEs) and weaknesses, active repositories that have Advanced Security turned off, security posture assessments of your DevOps environment configurations, and much more. Customize and add your own visual reports by using the rich set of data in Azure Resource Graph to fit the business needs of your security team.

[![Screenshot that shows a sample results page after you select the DevOps workbook.](media/custom-dashboards-azure-workbooks/devops-workbook.png)](media/custom-dashboards-azure-workbooks/devops-workbook.png#lightbox)

Note

To use this workbook, your environment must have a [GitHub connector](quickstart-onboard-github), [GitLab connector](quickstart-onboard-gitlab), or [Azure DevOps connector](quickstart-onboard-devops).

To deploy the workbook:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Workbooks**.
3. Select the **DevOps Security (Preview)** workbook.

The workbook loads and displays the **Overview** tab. On this tab, you can see the number of exposed secrets, the code security, and DevOps security. The findings are shown by total for each repository and by severity.

To view the count by secret type, select the **Secrets** tab.

[![Screenshot that shows the Secrets tab, which displays the count of findings by secret type.](media/custom-dashboards-azure-workbooks/count-secret-type.png)](media/custom-dashboards-azure-workbooks/count-secret-type.png#lightbox)

The **Code** tab displays the findings count by tool and repository. It shows the results of your code scanning by severity.

[![Screenshot that shows the Code tab and its findings by tool, repository, and severity.](media/custom-dashboards-azure-workbooks/code-findings.png)](media/custom-dashboards-azure-workbooks/code-findings.png#lightbox)

The **OSS Vulnerabilities** tab displays Open Source Security (OSS) vulnerabilities by severity and the count of findings by repository.

![Screenshot that shows the OSS Vulnerabilities tab, which displays severities and findings by repository.](media/custom-dashboards-azure-workbooks/oss-vulnerabilities.png)

The **Infrastructure as Code** tab displays your findings by tool and repository.

[![Screenshot that shows the Infrastructure as Code tab, which shows you your findings by tool and repository.](media/custom-dashboards-azure-workbooks/infrastructure-code.png)](media/custom-dashboards-azure-workbooks/infrastructure-code.png#lightbox)

The **Posture** tab displays security posture by severity and repository.

[![Screenshot that shows the Posture tab, which displays security posture by severity and repository.](media/custom-dashboards-azure-workbooks/posture-tab.png)](media/custom-dashboards-azure-workbooks/posture-tab.png#lightbox)

The **Threats & Tactics** tab displays the count of threats and tactics by repository and the total count.

[![Screenshot that shows the Threats &amp; Tactics tab, which displays the total count of threats and tactics and the count per repository.](media/custom-dashboards-azure-workbooks/threats-and-tactics.png)](media/custom-dashboards-azure-workbooks/threats-and-tactics.png#lightbox)

## Import workbooks from other workbook galleries

To move workbooks that you build in other Azure services into your Microsoft Defender for Cloud workbook gallery:

1. Open the workbook that you want to import.
2. On the toolbar, select **Edit**.

    ![Screenshot that shows how to edit a workbook.](media/custom-dashboards-azure-workbooks/editing-workbooks.png)
3. On the toolbar, select **&lt;/&gt;** to open the advanced editor.

    ![Screenshot that shows how to open the advanced editor to copy the gallery template JSON code.](media/custom-dashboards-azure-workbooks/editing-workbooks-advanced-editor.png)
4. In the workbook gallery template, select all the JSON in the file and copy it.
5. Open the workbook gallery in Defender for Cloud, and then select **New** on the menu bar.
6. Select **&lt;/&gt;** to open the Advanced Editor.
7. Paste the entire gallery template JSON code.
8. Select **Apply**.
9. On the toolbar, select **Save As**.

    ![Screenshot that shows saving the workbook to the gallery in Defender for Cloud.](media/custom-dashboards-azure-workbooks/editing-workbooks-save-as.png)
10. To save changes to the workbook, enter or select the following information:

    - A name for the workbook.
    - The Azure region to use.
    - Any relevant information about the subscription, resource group, and sharing.

To find the saved workbook, go to the **Recently modified workbooks** category.