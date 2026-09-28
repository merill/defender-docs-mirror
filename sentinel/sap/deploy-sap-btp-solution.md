---
layout: Conceptual
title: Deploy Microsoft Sentinel solution for SAP BTP | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/deploy-sap-btp-solution
breadcrumb_path: ../breadcrumb/toc.json
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
ms.reviewer: mapankra
description: Learn how to deploy the Microsoft Sentinel solution for SAP Business Technology Platform (BTP) system.
ms.author: monaberdugo
author: mberdugo
ms.topic: how-to
ms.custom: devx-track-azurepowershell, msecd-doc-authoring-1016
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 79dae81d-051f-7109-31d7-c6bbd696105a
document_version_independent_id: 9ed4ec22-169d-2a93-f7b5-7b45c5042362
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/deploy-sap-btp-solution.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/deploy-sap-btp-solution
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/deploy-sap-btp-solution.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: becf73c8-2cb1-670b-64b7-f982321c80bc
---

# Deploy Microsoft Sentinel solution for SAP BTP | Microsoft Learn

This article describes how to deploy the Microsoft Sentinel solution for SAP Business Technology Platform (BTP) system. The Microsoft Sentinel solution for SAP BTP monitors and protects your SAP BTP system. It collects audit logs and activity logs from the BTP infrastructure and BTP-based apps, and then detects threats, suspicious activities, illegitimate activities, and more. [SAP BTP solution overview](sap-btp-solution-overview).

Important

An architectural shift in the data connector v3.0.11 to cater for delayed SAP BTP logs requires re-onboarding of SAP subaccounts added prior to that change. See the [SAP BTP solution release notes](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/SAP%20BTP/ReleaseNotes.md) for more details. Consider the [SAP BTP mass onboarding tools](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/SAP%20BTP/Tools) for convenience.

## Prerequisites

Before you begin, verify that:

- The Microsoft Sentinel solution is enabled.
- You have a defined Microsoft Sentinel workspace, and you have read and write permissions to the workspace.
- Your organization uses SAP BTP (in a Cloud Foundry environment) to streamline interactions with SAP applications and other business applications.
- You have an SAP BTP Subaccount (which supports BTP Subaccounts in the Cloud Foundry environment). You can also use a [SAP BTP trial account](https://cockpit.hanatrial.ondemand.com/).
- You have the SAP BTP auditlog-management service and service key (see Set up the BTP Subaccount and solution).
- You have the Microsoft Sentinel Contributor role on the target Microsoft Sentinel workspace.

## Set up the BTP subaccount and solution

To set up the BTP subaccount and the solution manually from the SAP BTP cockpit and Azure portal, follow these steps:

1. After you can sign in to your BTP Subaccount (see the deployment prerequisites), follow the [audit log retrieval steps](https://help.sap.com/docs/btp/sap-business-technology-platform/audit-log-retrieval-api-usage-for-subaccounts-in-cloud-foundry-environment) on the SAP BTP system.
2. In the SAP BTP cockpit, select the **Audit Log Management Service**.

    [![Screenshot that shows selecting the BTP Audit Log Management Service.](media/deploy-sap-btp-solution/btp-audit-log-management-service.png)](media/deploy-sap-btp-solution/btp-audit-log-management-service.png#lightbox)
3. Create an instance of the Audit Log Management Service in the BTP subaccount.

    [![Screenshot that shows creating an instance of the BTP subaccount.](media/deploy-sap-btp-solution/btp-audit-log-sub-account.png)](media/deploy-sap-btp-solution/btp-audit-log-sub-account.png#lightbox)
4. Create a service key and record the values for `url`, `uaa.clientid`, `uaa.clientsecret`, and `uaa.url`. These values are required to deploy the data connector.

    Here are examples of these field values:

    - **url**: `https://auditlog-management.cfapps.us10.hana.ondemand.com`
    - **uaa.clientid**: `00001111-aaaa-2222-bbbb-3333cccc4444|auditlog-management!b1237`
    - **uaa.clientsecret**: `aaaaaaaa-0b0b-1c1c-2d2d-333333333333`
    - **uaa.url**: `https://trial.authentication.us10.hana.ondemand.com`
5. Sign in to the [Azure portal](https://portal.azure.com).
6. Go to the Microsoft Sentinel service.
7. Select **Content hub**, and in the search bar, search for *BTP*.
8. Select **SAP BTP**.
9. Select **Install**.

    For more information about how to manage the solution components, see [Discover and deploy Microsoft Sentinel out-of-the-box content](../sentinel-solutions-deploy).
10. Select **Create**.

    [![Screenshot that shows how to create the Microsoft Sentinel solution  for SAP BTP.](media/deploy-sap-btp-solution/sap-btp-create-solution.png)](media/deploy-sap-btp-solution/sap-btp-create-solution.png#lightbox)
11. Select the resource group and the Microsoft Sentinel workspace in which to deploy the solution.
12. Select **Next** until you pass validation, and then select **Create**.
13. When the solution deployment is finished, return to your Microsoft Sentinel workspace and select **Data connectors**.
14. In the search bar, enter **BTP**, and then select **SAP BTP**.
15. Select **Open connector page**.
16. On the connector page, make sure that you meet the required prerequisites listed and complete the configuration steps. When you're ready, select **Add account**.
17. Specify the parameters that you defined earlier during the configuration. The subaccount name specified is projected as a column in the `SAPBTPAuditLog_CL` table and can be used to filter the logs when you have multiple subaccounts.

    Consider the advanced options, if needed:

    - **Polling Frequency**: The frequency at which the connector polls for new data. The default is 1 minute.
    - **Log Ingest Delay**: The estimated delay between the time the event is generated in SAP BTP and the time it's available on the SAP BTP audit log service for ingestion in Microsoft Sentinel. The default is 20 minutes.

    Note

    Retrieving audits for the global account doesn't automatically retrieve audits for the subaccount. Follow the connector configuration steps for each of the subaccounts you want to monitor, and also follow these steps for the global account. Review these SAP BTP account auditing configuration considerations.
18. Make sure that BTP logs are flowing into the Microsoft Sentinel workspace:

    1. Sign in to your BTP subaccount and run a few activities that generate logs, such as sign-ins, adding users, changing permissions, and changing settings.
    2. Allow 20 to 30 minutes for the logs to start flowing.
    3. On the **SAP BTP** connector page, confirm that Microsoft Sentinel receives the BTP data, or query the **SAPBTPAuditLog\_CL** table directly.
19. Enable the [SAP BTP workbook](sap-btp-security-content#sap-btp-workbook) and the [SAP BTP built-in analytics rules](sap-btp-security-content#built-in-analytics-rules) that are provided as part of the solution by following the [guidelines for deploying Microsoft Sentinel analytics rules](../sentinel-solutions-deploy#analytics-rule).

Note

To onboard SAP BTP subaccounts at scale, API and CLI based approaches are recommended. Get started with the [SAP BTP onboarding script library](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/SAP%20BTP/Tools/).

## Consider your account auditing configurations

As part of deployment, consider your global account and subaccount auditing configurations.

### Global account auditing configuration

When you enable audit log retrieval in the BTP cockpit for the global account: If the subaccount for which you want to entitle the Audit Log Management Service is under a directory, you must entitle the service at the directory level first. Only then can you entitle the service at the subaccount level.

### Subaccount auditing configuration

To enable auditing for a subaccount, complete the steps in the [SAP subaccounts audit retrieval API documentation](https://help.sap.com/docs/btp/sap-business-technology-platform/audit-log-retrieval-api-usage-for-subaccounts-in-cloud-foundry-environment).

The API documentation describes how to enable the audit log retrieval by using the Cloud Foundry command-line interface (CLI).

You also can retrieve the logs via the UI:

1. In your subaccount in SAP Service Marketplace, create an instance of **Audit Log Management Service**.
2. In the new instance, create a service key.
3. View the service key and retrieve the required parameters from step 4 of the configuration instructions in the data connector UI (**url**, **uaa.url**, **uaa.clientid**, and **uaa.clientsecret**).

## Mass-Onboard SAP BTP subaccounts at scale

To onboard SAP BTP subaccounts at scale, API and CLI based approaches are recommended. Get started with the [SAP BTP onboarding script library](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/SAP%20BTP/Tools/).

## Rotate the BTP client secret

We recommend that you periodically rotate the BTP subaccount client secrets. For an automated, platform-based approach, see our [Automatic SAP BTP trust store certificate renewal with Azure Key Vault – or how to stop thinking about expiry dates once and for all](https://community.sap.com/t5/technology-blogs-by-members/automatic-sap-btp-trust-store-certificate-renewal-with-azure-key-vault-or/ba-p/13565138) (SAP blog).

The [SAP BTP key rotation script library](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/SAP%20BTP/Tools#key-rotation) demonstrates the automatic process of updating an existing data connector with a new secret.