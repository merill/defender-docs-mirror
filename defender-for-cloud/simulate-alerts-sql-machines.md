---
layout: Conceptual
title: Simulate Alerts for SQL Servers on Machines - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/simulate-alerts-sql-machines
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: TimShererWithAquent
ms.author: v-tishe
manager: orspodek
ms.service: defender-for-cloud
description: Simulate alerts for SQL servers on machines to safely validate your Defender for Cloud detection and response workflows. Learn how to run and verify test alerts.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 94d92be4-8294-e427-f617-4f05e9174b52
document_version_independent_id: 214862ba-39bc-8e92-5222-88aabea460a5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/simulate-alerts-sql-machines.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/simulate-alerts-sql-machines
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/simulate-alerts-sql-machines.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 6e0267be-ffbe-fecd-2e13-4adff4d31e1b
---

# Simulate Alerts for SQL Servers on Machines - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud provides a SQL alert simulation feature that helps organizations and security teams validate deployments and test detection, response, and automation workflows without creating actual security risks.

The simulation uses a custom script extension named `Sql-SimulateAlert` to inject telemetry records on target machines. Target machines include Azure Virtual Machines (VMs) or Arc-connected machines. Each simulated alert includes runtime context such as host, SQL instance, database, and process information. You can use these alerts to validate your end-to-end security response flows. This process is safe and doesn't affect your resources.

You can simulate the following security scenarios:

- Brute force authentication
- Authentication from suspicious application
- SQL injection
- Principal anomaly
- Shell external source anomaly
- Shell obfuscation

The simulation runs locally on the machine through the Custom Script Extension without executing external malicious payloads. All generated alerts contain complete machine and resource identifiers, SQL instance names, database information, process details, and telemetry data required by playbooks and security automation workflows.

## Prerequisites

- [Enable SQL Servers on Machines plan for Defender for Databases](defender-for-sql-usage).
- [Ensure that the target machine, whether a SQL VM or Arc‑connected machine, is successfully protected](verify-machine-protection).
- The following roles and permissions:

    - **Create an ARM deployment and write VM extensions**: Security Admin or Contributor in the target subscription.
    - Contributor permission and Resource Policy contributor to the resources `Microsoft.Compute/virtualMachines/write` and `Microsoft.Resources/deployments/*`.
- Configure the SQL Server instance to allow SQL Authentication for simulation scenarios that require a username and password. Some simulation types accept user credentials.

    Note

    Use an appropriate test SQL username and password rather than a production account.

## Simulate alerts

The `SqlAlertSimulationClient` reads details from the target resource, such as subscription, resource group, machine name, and location.

It then builds an Azure Resource Manager (ARM) template that deploys a custom script extension on the machine. The extension runs a PowerShell command that starts the Defender for SQL simulate helper with the chosen attack settings. The helper creates alert data and sends it to Defender for Cloud. These alerts can then trigger your automation and response connectors.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Azure SQL**.
3. Select **SQL Server on Azure VMS** or **SQL Server instances (Azure Arc)**.

    [![Screenshot that shows how to navigate to your SQL virtual machine.](media/simulate-alerts-sql-machines/select-sql-database.png)](media/simulate-alerts-sql-machines/select-sql-database.png#lightbox)
4. Select the relevant database.
5. Select **Security** &gt; **Microsoft Defender for Cloud**.
6. Select the **Security Alerts** tab, and then select **Simulate Alerts**.

    [![Screenshot of the Microsoft Defender for SQL page with the Security Alerts tab and Simulate Alerts button highlighted.](media/simulate-alerts-sql-machines/simulate-sql-alert.png)](media/simulate-alerts-sql-machines/simulate-sql-alert.png#lightbox)
7. Select an alert type.

    [![Screenshot that shows the different types of alerts that can be selected.](media/simulate-alerts-sql-machines/select-alert-type.png)](media/simulate-alerts-sql-machines/select-alert-type.png#lightbox)
8. Enter the required information for the selected alert type. For example, username and password for authentication attacks.
9. Select **Simulate Alerts**.

The alert appears after a few minutes. You can use the alert to validate your security monitoring setup.

## Verify that the alert is generated

After you simulate an alert, verify that the alert is generated.

1. In the Azure portal, search for and select **Azure SQL**.
2. Select **SQL Server on Azure VMS** or **SQL Server instances (Azure Arc)**.
3. Select the relevant database.
4. Select **Security** &gt; **Microsoft Defender for Cloud**.
5. Select the **Security Alerts** tab.
6. Select **Check for alerts on this resource in Microsoft Defender for Cloud**.

    [![Screenshot of the Microsoft Defender for SQL page with the Security Alerts tab and the link to check the resource's alerts in Defender for Cloud highlighted.](media/simulate-alerts-sql-machines/check-resource-alerts-in-defender-for-cloud.png)](media/simulate-alerts-sql-machines/check-resource-alerts-in-defender-for-cloud.png#lightbox)

Verify that the simulated alert appears in the list of alerts for the resource and [manage and respond to the security alert](manage-respond-alerts).