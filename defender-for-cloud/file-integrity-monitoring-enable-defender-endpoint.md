---
layout: Conceptual
title: Enable File Integrity Monitoring - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/file-integrity-monitoring-enable-defender-endpoint
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
description: Configure File Integrity Monitoring in Microsoft Defender for Cloud. Use the Defender for Endpoint scanning to collect monitoring data.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 435e1a40-0037-f9fa-2c63-24b0e267705b
document_version_independent_id: 10426ecb-0886-4281-3828-8baa3cca8d2a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/file-integrity-monitoring-enable-defender-endpoint.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/file-integrity-monitoring-enable-defender-endpoint
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/file-integrity-monitoring-enable-defender-endpoint.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: f28dd0a5-001f-794c-3876-c565c5a78058
---

# Enable File Integrity Monitoring - Microsoft Defender for Cloud | Microsoft Learn

In Defender for Servers Plan 2 in Microsoft Defender for Cloud, the [File Integrity Monitoring](file-integrity-monitoring-overview) feature helps to keep enterprise assets and resources secure. It scans and analyzes operating system files, Windows registries, application software, and Linux system files for changes that might indicate an attack.

After you enable Defender for Servers Plan 2, follow the steps in this article to configure File Integrity Monitoring by using the Microsoft Defender for Endpoint agent and agentless machine scanning to collect data.

Note

- If you use a previous version of File Integrity Monitoring with the Log Analytics agent (Microsoft Monitoring agent (MMA)) or the Azure Monitor agent (AMA), you can [migrate to the new File Integrity Monitoring experience](migrate-file-integrity-monitoring).
- File Integrity Monitoring powered by Microsoft Defender for Endpoint requires a minimum agent version. Update the agent as needed.

    - **Windows (legacy machines/downlevel clients)**: Defender for Servers Windows client (MDE agent) version 10.8799 or later.
    - **Linux**: 30.124082 or later. For known Linux sensor behavior limitations, see Considerations and limitations.

## Prerequisites

- Enable [Defender for Servers Plan 2](tutorial-enable-servers-plan) on your subscription.
- Install the [Defender for Endpoint](/en-us/defender-endpoint/microsoft-defender-endpoint) agent through the [Defender for Servers extensions](faq-defender-for-servers) on machines you want to monitor.
- Connect non-Azure machines with [Azure Arc](/en-us/azure/azure-arc/servers/learn/quick-enable-hybrid-vm).
- Enable [agentless machine scanning](concept-agentless-data-collection) on your subscription to gain extra coverage and the ability to monitor custom paths.
- Have **Workspace owner** and **Security admin** permissions to enable and disable File Integrity Monitoring. **Security reader** permissions can view results.

## Verify Defender for Endpoint client version

Before you begin, verify that the Defender for Endpoint client version on your machines is at least the minimum version required for File Integrity Monitoring.

- **Windows Server 2019 or later**: The Defender for Endpoint agent is updated as part of continuous operating system updates. Ensure Windows machines have the latest update installed.

    Learn more about using the [Windows Servers Update Service to install machines at scale](/en-us/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus).
- **Windows Servers 2016 and Windows Server 2012 R2**: You must [update machines manually to the latest agent version](https://support.microsoft.com/topic/microsoft-defender-for-endpoint-update-for-edr-sensor-f8f69773-f17f-420f-91f4-a8e5167284ac).

    You can install [KB 5005292 from the Microsoft Update Catalog](https://www.catalog.update.microsoft.com/Search.aspx?q=KB5005292). KB 5005292 is periodically updated with the latest agent version.
- **Linux machines**: If autoprovisioning is turned on for the machines in Defender for Cloud, the Defender for Endpoint agent is automatically updated. After the MDE.Linux extension is installed on a Linux machine, the machine attempts to update the agent version each time the virtual machine (VM) restarts. You can also [update the agent version manually](/en-us/defender-endpoint/linux-updates).

## Enable File Integrity Monitoring in the Azure portal

File Integrity Monitoring isn't enabled by default. You can enable it in the Microsoft Defender for Cloud portal.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings** and select the relevant subscription.
3. Find the Defenders for Servers plan and select **Settings**.
4. In the **File Integrity Monitoring** section, switch the toggle to **On**.

    [![Screenshot of how to enable File Integrity Monitoring.](media/file-integrity-monitoring-enable-defender-endpoint/defender-servers-file-integrity-monitoring.png)](media/file-integrity-monitoring-enable-defender-endpoint/defender-servers-file-integrity-monitoring.png#lightbox)
5. Select **Edit configuration**.
6. Select a workspace to store the File Integrity Monitoring data. (Optional) Or, select **Create new** to create a new workspace.

    [![Screenshot of the File Integrity Monitoring configuration pane.](media/file-integrity-monitoring-enable-defender-endpoint/file-integrity-monitoring-configuration.png)](media/file-integrity-monitoring-enable-defender-endpoint/file-integrity-monitoring-configuration.png#lightbox)
7. Under the **Recommended to monitor** rule section, select **Edit**.
8. Select the [files and registries](file-integrity-monitoring-overview#recommended-items-to-monitor) recommended for monitoring.

    Ensure the **Status** toggle is set to **Enabled** and select the **Change types** you want to monitor. By default, all entities recommended for monitoring are selected. You can remove entities from monitoring by selecting the three dot button next to the monitoring rule and then selecting **Delete**.

    [![Screenshot that shows the file registries that need to be corrected.](media/file-integrity-monitoring-enable-defender-endpoint/files-registries.png)](media/file-integrity-monitoring-enable-defender-endpoint/files-registries.png#lightbox)
9. Select **Apply** to save your changes.

    [![Screenshot that shows the edit rule screen.](media/file-integrity-monitoring-enable-defender-endpoint/edit-rule.png)](media/file-integrity-monitoring-enable-defender-endpoint/edit-rule.png#lightbox)
10. (Optional) Select **+ Add rule** to create a custom rule.

    [![Screenshot that shows the Add a rule window.](media/file-integrity-monitoring-enable-defender-endpoint/add-rule.png)](media/file-integrity-monitoring-enable-defender-endpoint/add-rule.png#lightbox)

    1. Under the **Add new custom rule** section, enter a **Rule name** and (Optional) a **Rule description**.
    2. Ensure **Status** toggle is set to **Enabled**.
    3. Select the **Change types** and define **Entity type** and **Entity path** for your custom rules.
    4. Select **Apply** to save your changes.
    5. (Optional) Select **Delete rule** to delete a rule configuration.
11. Select **Apply**.
12. Select **Continue**.

## Review enablement status for File Integrity Monitoring

Review the File Integrity Monitoring enablement to ensure the configuration is correct and all prerequisites are met.

1. Go to **Workload protection** &gt; **File Integrity Monitoring**.

    [![Screenshot of the File Integrity Monitoring status button.](media/file-integrity-monitoring-enable-defender-endpoint/file-integrity-monitoring-status.png)](media/file-integrity-monitoring-enable-defender-endpoint/file-integrity-monitoring-status.png#lightbox)
2. Select **Settings**.

    [![Screenshot of the File Integrity Monitoring page that shows where the settings button is located.](media/file-integrity-monitoring-enable-defender-endpoint/file-integrity-monitoring-settings.png)](media/file-integrity-monitoring-enable-defender-endpoint/file-integrity-monitoring-settings.png#lightbox)
3. Check for any missing prerequisites.
4. Select a subscription and review corrective actions for the necessary workspace.

    [![Screenshot of the File Integrity Monitoring page that shows the missing prerequisites.](media/file-integrity-monitoring-enable-defender-endpoint/corrective-actions.png)](media/file-integrity-monitoring-enable-defender-endpoint/corrective-actions.png#lightbox)
5. Select the checkbox for any required fixes.
6. Select **Apply**.

## Disable File Integrity Monitoring

If you disable File Integrity Monitoring, no new events are collected. The data collected before the disablement remains in the Log Analytics workspace, in accordance with the workspace retention policy.

To disable File Integrity Monitoring, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Environment settings** &gt; **relevant subscription**.
3. Locate the Defenders for Servers plan and select **Settings**.
4. In the **File Integrity Monitoring** section, switch the toggle to **Off**.

    [![Screenshot of how to disable File Integrity Monitoring.](media/file-integrity-monitoring-enable-defender-endpoint/disable-file-integrity-monitoring.png)](media/file-integrity-monitoring-enable-defender-endpoint/disable-file-integrity-monitoring.png#lightbox)
5. Select **Apply**.
6. Select **Continue**.
7. Select **Save**.

## Considerations and limitations

The current Linux sensor doesn't distinguish between *Create* and *Modify* actions. It identifies both as *Modify* actions. As a result, when a new file is created, the event is logged as a *Modify* event rather than a Create event.