---
layout: Conceptual
title: Monitor Zero Trust (TIC 3.0) Security Architectures with Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sentinel-solution
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Install and learn how to use the Microsoft Sentinel Zero Trust (TIC3.0) solution for an automated visualization of Zero Trust principles, cross-walked to the Trusted Internet Connections framework.
ms.date: 2026-07-01T00:00:00.0000000Z
ms.author: monaberdugo
author: mberdugo
ms.reviewer: tbeerthuis
ms.topic: how-to
ms.collection:
- zerotrust-services
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 3b028bc5-97d2-3d33-a023-01edbed55809
document_version_independent_id: 64c1d3e6-00c9-b301-6fa8-2704bc9f2ac1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sentinel-solution.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/sentinel-solution
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sentinel-solution.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 6b4f8abc-b72b-6cc0-2333-6704a2b43a48
---

# Monitor Zero Trust (TIC 3.0) Security Architectures with Microsoft Sentinel | Microsoft Learn

[Zero Trust](/en-us/security/zero-trust/zero-trust-overview) is a security strategy for designing and implementing the following sets of security principles:

| Verify explicitly | Use least privilege access | Assume breach |
| --- | --- | --- |
| Always authenticate and authorize based on all available data points. | Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection. | Minimize blast radius and segment access. Verify end-to-end encryption and use analytics to get visibility, drive threat detection, and improve defenses. |

This article describes how to use the Microsoft Sentinel **Zero Trust (TIC 3.0)** solution, which helps governance and compliance teams monitor and respond to Zero Trust requirements according to the [TRUSTED INTERNET CONNECTIONS (TIC) 3.0](https://www.cisa.gov/resources-tools/programs/trusted-internet-connections-tic) initiative.

[Microsoft Sentinel solutions](sentinel-solutions) are sets of bundled content, pre-configured for a specific set of data. The **Zero Trust (TIC 3.0)** solution includes a workbook, analytics rules, and a playbook, which provide an automated visualization of Zero Trust principles, cross-walked to the Trust Internet Connections framework, helping organizations to monitor configurations over time.

Note

Get a comprehensive view of your organization's Zero Trust status with the Zero Trust initiative in Microsoft Exposure Management. For more information, see [Rapidly modernize your security posture for Zero Trust | Microsoft Learn](/en-us/security/zero-trust/adopt/rapidly-modernize-security-posture#in-product-dashboards-and-reports).

## The Zero Trust solution and the TIC 3.0 framework

Zero Trust and TIC 3.0 aren't the same, but they share many common themes and together provide a common story. The Microsoft Sentinel solution for **Zero Trust (TIC 3.0)** offers detailed crosswalks between Microsoft Sentinel and the Zero Trust model with the TIC 3.0 framework. These crosswalks help users to better understand the overlaps between the Zero Trust model and the TIC 3.0 framework.

While the Microsoft Sentinel solution for **Zero Trust (TIC 3.0)** provides best practice guidance, Microsoft doesn't guarantee nor imply compliance. All Trusted Internet Connection (TIC) requirements, validations, and controls are governed by the [Cybersecurity & Infrastructure Security Agency](https://www.cisa.gov/resources-tools/programs/trusted-internet-connections-tic).

The **Zero Trust (TIC 3.0)** solution provides visibility and situational awareness for control requirements delivered with Microsoft technologies in predominantly cloud-based environments. Customer experience will vary by user, and some panes might require additional configurations and query modification for operation.

Recommendations don't imply coverage of respective controls, as they're often one of several courses of action for approaching requirements, which is unique to each customer. Recommendations should be considered a starting point for planning full or partial coverage of respective control requirements.

The Microsoft Sentinel solution for **Zero Trust (TIC 3.0)** is useful for any of the following users and use cases:

- **Security governance, risk, and compliance professionals**, for compliance posture assessment and reporting
- **Engineers and architects**, who need to design Zero Trust and TIC 3.0-aligned workloads
- **Security analysts**, for alert and automation building
- **Managed security service providers (MSSPs)** for consulting services
- **Security managers**, who need to review requirements, analyze reporting, evaluating capabilities

## Prerequisites

Before installing the **Zero Trust (TIC 3.0)** solution, make sure you have the following prerequisites:

- **Onboard Microsoft services**: Make sure that you have both [Microsoft Sentinel](quickstart-onboard) and [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/get-started) enabled in your Azure subscription.
- **Microsoft Defender for Cloud requirements**: In Microsoft Defender for Cloud:

    - Add required regulatory standards to your dashboard. Make sure to add both the *Microsoft Cloud security benchmark* and *NIST SP 800-53 R5 Assessments* to your Microsoft Defender for Cloud dashboard. For more information, see [add a regulatory standard to your dashboard](/en-us/azure/security-center/update-regulatory-compliance-packages?WT.mc_id=Portal-fx#add-a-regulatory-standard-to-your-dashboard) in the Microsoft Defender for Cloud documentation.
    - Continuously export Microsoft Defender for Cloud data to your Log Analytics workspace. For more information, see [Continuously export Microsoft Defender for Cloud data](/en-us/azure/defender-for-cloud/continuous-export?tabs=azure-portal).
- **Required user permissions**: To install the **Zero Trust (TIC 3.0)** solution, you must have access to your Microsoft Sentinel workspace with [Security Reader](/en-us/azure/active-directory/roles/permissions-reference#security-reader) permissions.

The **Zero Trust (TIC 3.0)** solution is also enhanced by integrations with other Microsoft Services, such as:

- [Microsoft Defender XDR](https://www.microsoft.com/microsoft-365/security/microsoft-365-defender)
- [Microsoft Information Protection](https://www.microsoft.com//security/business/solutions/information-protection/)
- [Microsoft Entra ID](https://www.microsoft.com/security/business/identity-access/microsoft-entra-id)
- [Microsoft Defender for Cloud](https://www.microsoft.com/security/business/cloud-security/microsoft-defender-cloud)
- [Microsoft Defender for Endpoint](https://www.microsoft.com/microsoft-365/security/endpoint-defender)
- [Microsoft Defender for Identity](https://www.microsoft.com/microsoft-365/security/identity-defender)
- [Microsoft Defender for Cloud Apps](https://www.microsoft.com/security/business/siem-and-xdr/microsoft-defender-cloud-apps)
- [Microsoft Defender for Office 365](https://www.microsoft.com/microsoft-365/security/office-365-defender)

## Install the Zero Trust (TIC 3.0) solution

To deploy the *Zero Trust (TIC 3.0)* solution from the Azure portal:

1. In Microsoft Sentinel, select **Content hub** and locate the **Zero Trust (TIC 3.0)** solution.
2. At the bottom-right, select **View details**, then select **Create**. Select the subscription, resource group, and workspace where you want to install the solution, and then review the related security content that will be deployed.

    When you're done, select **Review + Create** to install the solution.

For more information about deploying Microsoft Sentinel solutions, see [Deploy out-of-the-box content and solutions](sentinel-solutions-deploy).

## Sample usage scenario

This scenario shows how a security operations analyst could use the resources deployed with the **Zero Trust (TIC 3.0)** solution to visualize Zero Trust data, configure Zero Trust-related alerts, and respond with SOAR.

After you install the Zero Trust (TIC 3.0) solution, use the workbook, analytics rules, and playbook deployed to your Microsoft Sentinel workspace to manage Zero Trust in your network.

### Visualize Zero Trust data

Use the **Zero Trust (TIC 3.0)** workbook to view Zero Trust data and explore queries:

1. Navigate to the Microsoft Sentinel **Workbooks** &gt; **Zero Trust (TIC 3.0)** workbook, and select **View saved workbook**.

    In the **Zero Trust (TIC 3.0)** workbook page, select the TIC 3.0 capabilities you want to view. For this procedure, select **Intrusion Detection**.

    Tip

    Use the **Guide** toggle at the top of the page to display or hide recommendations and guide panes. Make sure that the correct details are selected in the **Subscription**, **Workspace**, and **TimeRange** options so that you can view the specific data you want to find.
2. Select the control cards you want to display. For this procedure, select **Adaptive Access Control**, then continue scrolling to view the displayed card.

    ![Screenshot of the Adaptive Access Control card.](media/sentinel-workbook/review-query-output-sample.png)

    Tip

    Use the **Guides** toggle at the top left to view or hide recommendations and guide panes. For example, these might be helpful when you first access the workbook, but unnecessary once you've understood the relevant concepts.
3. **Explore queries**. For example, at the top right of the **Adaptive Access Control** card, select the three dot **Options** menu, and then select **Open the last run query in the Logs view.**

    The query opens in the Microsoft Sentinel **Logs** page:

    ![Screenshot of the selected query in the Microsoft Sentinel Logs page.](media/sentinel-workbook/explore-query-logs.png)

### Configure Zero Trust-related alerts

In Microsoft Sentinel, navigate to the **Analytics** area. View out-of-the-box analytics rules deployed with the **Zero Trust (TIC 3.0)** solution by searching for **TIC3.0**.

By default, the **Zero Trust (TIC 3.0)** solution installs a set of analytics rules that are configured to monitor Zero Trust (TIC3.0) posture by control family, and you can customize thresholds for alerting compliance teams to changes in posture.

For example, if your workload's resiliency posture falls below a specified percentage in a week, Microsoft Sentinel will generate an alert to detail the respective policy status (pass/fail), the assets identified, the last assessment time, and provide deep links to Microsoft Defender for Cloud for remediation actions.

Update the rules as needed or configure a new one:

![Screenshot of the Analytics rule wizard.](media/sentinel-workbook/edit-rule.png)

For more information, see [Create custom analytics rules to detect threats](detect-threats-custom).

### Respond with SOAR

In Microsoft Sentinel, navigate to the **Automation** &gt; **Active playbooks** tab, and locate the **Notify-GovernanceComplianceTeam** playbook.

Use this playbook to automatically monitor CMMC alerts, and notify the governance compliance team with relevant details via both email and Microsoft Teams messages. Modify the playbook as needed:

![Screenshot of the Logic app designer showing a sample playbook.](media/sentinel-workbook/logic-app-sample.png)

For more information, see [Use triggers and actions in Microsoft Sentinel playbooks](playbook-triggers-actions).

## Frequently asked questions

The following questions address common scenarios and requirements for the **Zero Trust (TIC 3.0)** solution.

### Are custom views and reports supported?

Yes. You can customize your **Zero Trust (TIC 3.0)** workbook to view data by subscription, workspace, time, control family, or maturity level parameters, and you can export and print your workbook.

For more information, see [Use Azure Monitor workbooks to visualize and monitor your data](monitor-your-data).

### Are additional products required?

Both Microsoft Sentinel and Microsoft Defender for Cloud are required prerequisites for this solution. For details, see the Prerequisites section.

Aside from these services, each control card is based on data from multiple services, depending on the types of data and visualizations being shown in the card. Over 25 Microsoft services provide enrichment for the **Zero Trust (TIC 3.0)** solution.

### What should I do with panels with no data?

Panels with no data provide a starting point for addressing Zero Trust and TIC 3.0 control requirements, including recommendations for addressing respective controls.

### Are multiple subscriptions, clouds, and tenants supported?

Yes. You can use workbook parameters, Azure Lighthouse, and Azure Arc to leverage the **Zero Trust (TIC 3.0)** solution across all of your subscriptions, clouds, and tenants.

For more information, see [Use Azure Monitor workbooks to visualize and monitor your data](monitor-your-data) and [Manage multiple tenants in Microsoft Sentinel as an MSSP](multiple-tenants-service-providers).

### Is partner integration supported?

Yes. Both workbooks and analytics rules are customizable for integrations with partner services.

For more information, see [Use Azure Monitor workbooks to visualize and monitor your data](monitor-your-data) and [Surface custom event details in alerts](surface-custom-details-in-alerts).

### Is this available in government regions?

Yes. The **Zero Trust (TIC 3.0)** solution is in Public Preview and deployable to Commercial/Government regions. For more information, see [Cloud feature availability for commercial and US Government customers](/en-us/azure/security/fundamentals/feature-availability).

### Which permissions are required to use this content?

The following Microsoft Sentinel roles determine what users can do with this content:

- [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) users can create and edit workbooks, analytics rules, and other Microsoft Sentinel resources.
- [Microsoft Sentinel Reader](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-reader) users can view data, incidents, workbooks, and other Microsoft Sentinel resources.

For more information, see [Permissions in Microsoft Sentinel](roles).