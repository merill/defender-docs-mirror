---
layout: Conceptual
title: Protect Managed Security Service Provider (MSSPs) Intellectual Property in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/mssp-protect-intellectual-property
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
description: Protect Microsoft Sentinel intellectual property such as analytics rules, hunting queries, playbooks, and workbooks. Compare protection approaches for CSP and EA/PAYG customer purchasing models.
author: EdB-MSFT
ms.topic: how-to
ms.date: 2026-06-15T00:00:00.0000000Z
ms.author: edbaynash
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 90bcabfd-e99e-f1dd-2fd7-7e2cd41fd0bc
document_version_independent_id: 4ffd7d46-8216-ae8b-37c3-d0040918cb09
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/mssp-protect-intellectual-property.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/mssp-protect-intellectual-property
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/mssp-protect-intellectual-property.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/d0989e16-62ed-4db0-8dd8-b1c704683638
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/677796fe-69f7-4468-8f9b-540e903c4f4e
platformId: 87454396-ec58-6b2d-5b55-a6018c82ee78
---

# Protect Managed Security Service Provider (MSSPs) Intellectual Property in Microsoft Sentinel | Microsoft Learn

This article describes the methods that managed security service providers (MSSPs) can use to protect intellectual property they've developed in Microsoft Sentinel, such as Microsoft Sentinel analytics rules, hunting queries, playbooks, and workbooks.

The method you choose depends on how each of your customers buys Azure; whether you act as a Cloud Solutions Provider (CSP), or the customer has an Enterprise Agreement (EA)/Pay-as-you-go (PAYG) account. The Cloud Solutions Providers (CSP) and Enterprise Agreements (EA) / Pay-as-you-go (PAYG) sections describe each of these methods separately.

## Protect MSSP intellectual property in Cloud Solutions Provider (CSP) environments

If you're reselling Azure as a Cloud Solutions Provider (CSP), you're managing the customer's Azure subscription. Thanks to [Admin-On-Behalf-Of (AOBO)](/en-us/partner-center/azure-plan-manage), which lets partner admin agents manage a customer's subscription, users in the Admin Agents group (the Partner Center role whose members administer customer subscriptions) from your MSSP tenant are granted Owner access to the customer's Azure subscription, and the customer has no access by default.

If other users from the MSSP tenant, outside of the Admin Agents group, need to access the customer environment, we recommend that you use [Azure Lighthouse](multiple-tenants-service-providers). Azure Lighthouse allows you to grant users or groups with access to a specific scope, such as a resource group or subscription, using one of the built-in roles.

If you need to provide customer users with access to the Azure environment, we recommend that you grant them access at *resource group* level rather than the entire subscription, so that you can show/hide parts of the environment as needed.

For example:

- You might grant the customer with access to several resource groups where their applications are located, but still keep the Microsoft Sentinel workspace in a separate resource group, where the customer has no access.
- Use this method to enable customers to view selected workbooks and playbooks, which are separate resources that can reside in their own resource group.

Even with granting access at the resource group level, customers have access to log data for the resources they can access, such as logs from a VM, even without access to Microsoft Sentinel. For more information, see [Manage access to Microsoft Sentinel data by resource](resource-context-rbac).

Tip

If you need to provide your customers with access to the entire subscription, see the guidance in Protect MSSP intellectual property in Enterprise Agreement and Pay-as-you-go environments.

### Sample Microsoft Sentinel CSP architecture

The following image describes how the CSP permissions described in the Cloud Solutions Providers (CSP) section might work when providing access to CSP customers:

![Diagram showing how to protect your Microsoft Sentinel intellectual property with CSP customers.](media/mssp-protect-intellectual-property/csp-customers.png)

In this image:

- The users granted with **Owner** access to the CSP subscription are the users in the Admin Agents group, in the MSSP Microsoft Entra tenant.
- Other groups from the MSSP get access to the customer environment via Azure Lighthouse.
- Customer access to Azure resources is managed by Azure RBAC at the resource group level.

    Managing customer access at the resource group level allows MSSPs to hide Microsoft Sentinel components as needed, such as analytics rules and hunting queries.

For more information, also see the [Azure Lighthouse documentation](/en-us/azure/lighthouse/concepts/cloud-solution-provider).

## Protect MSSP intellectual property in Enterprise Agreement and Pay-as-you-go environments

If your customer is buying directly from Microsoft, the customer already has full access to the Azure environment, and you can't hide anything that's in the customer's Azure subscription.

Instead, protect your intellectual property that you've developed in Microsoft Sentinel as follows, depending on the type of resource you need to protect:

### Analytics rules and hunting queries

Analytics rules and hunting queries are both contained within Microsoft Sentinel, and therefore can't be separated from the Microsoft Sentinel workspace.

Even if a user only has Microsoft Sentinel Reader permissions, they can view the query. Because Reader permissions still expose queries, we recommend hosting your analytics rules and hunting queries in your own MSSP tenant, instead of the customer tenant.

To do this, you need a workspace in your own tenant with Microsoft Sentinel enabled, and you also need to see the customer workspace via [Azure Lighthouse](multiple-tenants-service-providers).

To create an analytic rule or hunting query in the MSSP tenant that references data in the customer tenant, you must use the `workspace` statement as follows:

```kusto
workspace('<customer-workspace-explicit-identifier>').SecurityEvent
| where EventID == ‘4625’
```

When adding a `workspace` statement to your analytics rules, consider the following:

- **Use the customer's explicit workspace identifier**: Use the customer workplace identifier in the cross workspace query for best performance. For more information, see [Identifier formats for cross workspace queries](/en-us/azure/azure-monitor/logs/cross-workspace-query#arguments).
- **No alerts in the customer workspace**: Rules created in this manner don't create alerts or incidents in the customer workspace. Both alerts and incidents exist in your MSSP workspace only.
- **Create separate alerts for each customer**: When you create cross-workspace analytics rules, we also recommend that you use separate alert rules for each customer and detection, because the workspace statement is different in each case.

    You can add the customer name to the alert rule name to easily identify the customer where the alert is triggered. Separate alerts may result in a large number of rules, which you might want to manage using scripting, or [Microsoft Sentinel as Code](https://techcommunity.microsoft.com/t5/azure-sentinel/deploying-and-managing-azure-sentinel-as-code/ba-p/1131928).

    For example:

    ![Create separate rules in your MSSP workspace for each customer.](media/mssp-protect-intellectual-property/mssp-rules-per-customer.png)
- **Create separate MSSP workspaces for each customer**: Creating separate rules for each customer and detection may cause you to reach the maximum number of analytics rules for your workspace (512). If you have many customers and expect to reach this limit, you may want to create a separate MSSP workspace for each customer.

    For example:

    ![Create a workspace and rules in your MSSP tenant for each customer.](media/mssp-protect-intellectual-property/mssp-rules-and-workspace-per-customer.png)

Important

The key to using cross-workspace analytics rules successfully is using automation to manage a large set of rules across your workspaces.

For more information, see [Cross-workspace analytics rules](https://techcommunity.microsoft.com/t5/azure-sentinel/what-s-new-cross-workspace-analytics-rules/ba-p/1664211)

### Workbooks

If you developed a Microsoft Sentinel workbook that you don't want your customer to copy, first make sure that you have access to your customer workspaces via Azure Lighthouse. Then host the workbook in your MSSP tenant and modify it to use those customer workspaces.

For example:

![Cross-workspace workbooks](media/mssp-protect-intellectual-property/cross-workspace-workbook.png)

For more information, see [Cross-workspace workbooks](extend-sentinel-across-workspaces-tenants#use-cross-workspace-workbooks).

If you want the customer to be able to view the workbook visualizations, while still keeping the code secret, we recommend that you export the workbook to Power BI.

Exporting your workbook to Power BI:

- **Makes the workbook visualizations easier to share**: You can send the customer a link to the Power BI dashboard, where they can view the reported data, without requiring Azure access permissions.
- **Enables scheduling**: Configure Power BI to send emails periodically that contain a snapshot of the dashboard for that time.

For more information, see [Import Azure Monitor log data into Power BI](/en-us/azure/azure-monitor/logs/log-powerbi).

### Playbooks

You can protect your playbooks as follows, depending on where the analytic rules that trigger the playbook have been created:

- **Analytics rules created in the MSSP workspace**: Make sure to create your playbooks in the MSSP tenant, and that you get all incident and alert data from the MSSP workspace. You can attach the playbooks whenever you create a new rule in your workspace.

    For example:

    ![Rules created in the MSSP workspace.](media/mssp-protect-intellectual-property/rules-in-mssp-workspace.png)
- **Analytics rules created in the customer workspace**: Use Azure Lighthouse to attach analytics rules from the customer's workspace to a playbook hosted in your MSSP workspace. In this case, the playbook gets the alert and incident data, and any other customer information, from the customer workspace.

    For example:

    ![Rules created in the customer workspace.](media/mssp-protect-intellectual-property/rules-in-customer-workspace.png)

In both cases, if the playbook needs to access the customer’s Azure environment, use a user or service principal that has that access via Lighthouse.

However, if the playbook needs to access non-Azure resources in the customer’s tenant, such as Microsoft Entra ID, Office 365, or Microsoft Defender XDR, create a service principal with appropriate permissions in the customer tenant, and then add that identity in the playbook.

Note

If you use automation rules together with your playbooks, you must set the automation rule permissions on the resource group where the playbooks live. For more information, see [Permissions for automation rules to run playbooks](automate-incident-handling-with-automation-rules#permissions-for-automation-rules-to-run-playbooks).