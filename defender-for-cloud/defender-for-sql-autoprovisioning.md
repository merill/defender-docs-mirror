---
layout: Conceptual
title: Migrate to Defender for SQL on machines using AMA - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-sql-autoprovisioning
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
description: Learn how to enable SQL server-targeted Azure Monitoring Agent's autoprovisioning process for Defender for SQL.
ms.topic: install-set-up-deploy
ms.date: 2025-05-05T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 3969b018-5481-3637-4546-f5970bc8c5ab
document_version_independent_id: c8d7db45-6acb-9ce4-7adc-bd4ad6b280b9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-sql-autoprovisioning.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-sql-autoprovisioning
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-sql-autoprovisioning.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 6b11aff2-2108-0c3c-93e2-427bd7a630ef
---

# Migrate to Defender for SQL on machines using AMA - Microsoft Defender for Cloud | Microsoft Learn

Important

This article applies to government clouds only.

Microsoft Monitoring Agent (MMA) was deprecated in August 2024. As a result, a new SQL server-targeted Azure Monitoring Agent (AMA) autoprovisioning process was released. You can learn more about the [Defender for SQL Server on machines Log Analytics Agent's deprecation plan](upcoming-changes#defender-for-sql-server-on-machines).

Customers who are using the current **Log Analytics agent/Azure Monitor agent** autoprovisioning process, should migrate to the new **Azure Monitoring Agent for SQL server on machines** autoprovisioning process. The migration process is seamless and provides continuous protection for all machines.

## Migrate to the SQL server-targeted AMA autoprovisioning process

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. In the Defender for Cloud menu, select **Environment settings**.
4. Select the relevant subscription.
5. Under the Databases plan, select **Action required**. [![Screenshot that shows where the option to select action required is on the Defender plans page.](media/defender-sql-autoprovisioning/action-required.png)](media/defender-sql-autoprovisioning/action-required.png#lightbox)

    Note

    If you don't see the action required button, under the Databases plan select **Settings** and then toggle the **Azure Monitoring Agent for SQL server on machines** option to **On**. Then select **Continue** &gt; **Save**.
6. In the pop-up window, select **Enable**.

    [![Screenshot that shows you where to select the Azure Monitor Agent on the screen.](media/defender-sql-autoprovisioning/update-sql.png)](media/defender-sql-autoprovisioning/update-sql.png#lightbox)
7. Select **Save**.

Once the SQL server-targeted AMA autoprovisioning process has been enabled, you should disable the **Log Analytics agent/Azure Monitor agent** autoprovisioning process.

Note

If you have the Defender for Server plan enabled, you need to [review the Defender for Servers Log Analytics deprecation plan](upcoming-changes#defender-for-servers) for Log Analytics agent/Azure Monitor agent dependency before disabling the process.

## Disable the Log Analytics agent/Azure Monitor agent

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. In the Defender for Cloud menu, select **Environment settings**.
4. Select the relevant subscription.
5. Under the Database plan, select **Settings**.
6. Toggle the Log Analytics agent/Azure Monitor agent to **Off**.

    [![Screenshot that shows where the toggle is for the log analytics agent and the Azure monitor agent toggled to off.](media/defender-sql-autoprovisioning/toggle-to-off.png)](media/defender-sql-autoprovisioning/toggle-to-off.png#lightbox)
7. Select **Continue**.
8. Select **Save**.