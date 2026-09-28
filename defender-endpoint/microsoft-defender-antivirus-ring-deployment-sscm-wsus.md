---
layout: Conceptual
title: Ring deployment using System Center Configuration Manager and Windows Server Update Services - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-antivirus-ring-deployment-sscm-wsus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Microsoft Defender Antivirus is an enterprise endpoint security platform that helps defend against advanced persistent threats. This article provides information about how to use a ring deployment method to update your Microsoft Defender Antivirus clients using System Center Configuration Manager (SCCM) and Windows Server Update Services (WSUS).
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.reviewer: yongrhee
ms.localizationpriority: high
ms.collection:
- m365-security
- tier1
- mde-ngp
ms.custom:
- intro-overview
- sfi-image-nochange
ms.topic: install-set-up-deploy
ms.subservice: ngp
ms.date: 2025-10-20T00:00:00.0000000Z
locale: en-us
document_id: 551f8d2b-1983-3bbf-fc9d-037a71f07d99
document_version_independent_id: 551f8d2b-1983-3bbf-fc9d-037a71f07d99
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/microsoft-defender-antivirus-ring-deployment-sscm-wsus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-defender-antivirus-ring-deployment-sscm-wsus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/microsoft-defender-antivirus-ring-deployment-sscm-wsus.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: dd9e97cf-7df5-3fc2-55ba-3258ece94d45
---

# Ring deployment using System Center Configuration Manager and Windows Server Update Services - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint is an enterprise endpoint security platform designed to help enterprise networks prevent, detect, investigate, and respond to advanced threats.

Tip

Microsoft Defender for Endpoint is available in two plans, Defender for Endpoint Plan 1 and Plan 2. A new Microsoft Defender Vulnerability Management add-on is now available for Plan 2.

## Prerequisites

### Supported operating systems

- Windows
- Windows Server

## Setting up the pilot environment

This section describes the process for setting up the pilot UAT / Test / QA environment.

[![Shows an example Microsoft Defender for Endpoint ring deployment schedule using System Center Configuration Manager and Windows Server Update Services.](media/microsoft-defender-antivirus-deploy-ring-sccm-wsus-schedule.png)](media/microsoft-defender-antivirus-deploy-ring-sccm-wsus-schedule.png#lightbox)

Note

Security intelligence update (SIU) is equivalent to signature updates, which is the same as definition updates.

On about 10-500 Windows and/or Windows Server systems, depending on how many total systems that you all have.

Note

If you have a Citrix environment, include at least 1 Citrix VM (non-persistent) and/or (persistent)

1. In **System Center Configuration Manager** &gt; **Create Automatic Deployment Rule Wizard** &gt; **General** page, in **Specify the setting for this automatic deployment rule**, make the following settings:

    | In: | Change: |
    | --- | --- |
    | **Name** | Type a name for your deployment rule. For example, type *MDE-MDAV\_Security\_Intelligence\_Update\_Pilot* |
    | **Description** | Type a brief description for your pilot |
    | **Template** | Select **SCEP and Windows Defender Antivirus Updates** |
    | **Collection** | Type **Windows\_Security\_Intelligence\_Pilot** |
    | **Each time the rule runs and finds new updates**. | Select **Create a new Software Update Group** |
    | **Each time the rule runs and finds new updates** | Select **Enable the deployment after this rule is run** |
2. Select **Next**. On the **Deployment Settings** page, under **Specify the settings for this Automatic Deployment Rule**, then do the following:

    | In: | Change: |
    | --- | --- |
    | **Type of deployment** | Select **Required** |
    | **Detail level** | Select **Only error messages** |
    | **Some software updates include a license agreement** | Select **Automatically deploy all software updates found by this rule, and approve any license agreements**. |
3. Select **Next**. On the **Software Updates** page, under **Select the property filters and search criteria**, make the following settings:

    | In: | Change: |
    | --- | --- |
    | **Property filters** | Select **Article ID** and **Date Released or Revised** |
    | **Search Criteria** | Enter the following **Article ID** = **2267602** **Date Released or Revised** = **Last 1 month** **Product** = **Windows Defender** **Superseded** = **No** **Update Classification** = **"Critical Updates" OR "Definition Updates"** |

    These settings are shown in the following image:

    [![Shows recommended Intune Microsoft Defender Antivirus pilot policy settings for the Software Updates page.](media/microsoft-defender-antivirus-deploy-ring-sccm-wizard-software-updates.png)](media/microsoft-defender-antivirus-deploy-ring-sccm-wizard-software-updates.png#lightbox)

    Tip

    Click **Preview** - to make sure "Security Intelligence Update for Windows Defender Antivirus" is listed. You should see **KB2267602**.

    Note

    **Date Released or Revised: Last 1 month** - If your WSUS/SUP have been healthy, you may want to set this to "Last 1 week".

    **Product: "Windows Defender"** - We are removing "System Center Endpoint Protection", because we want to target this to only the operating systems that have Microsoft Defender Antivirus.

    **Update Classification**: "Critical Updates" and "Definition Updates"
4. Select **Next**. On the **Evaluation Schedule** page, under **Specify the recurring schedule for this rule**, select **Run the rule on a schedule**, and then select **Customize**.
5. On the **Deployment Schedule** page, under **Configure schedule details for this deployment**, do the following:

    | In: | Change: |
    | --- | --- |
    | **Schedule evaluation** &gt; **Time based on** | Select **UTC** |
    | **Software available time** | Select **As soon as possible** |
    | **Installation deadline** | Select **As soon as possible** |
6. Select **Next**. On the **User Experience** page, under **Specify the user experience for this deployment**, ensure the following are selected:

    | In: | Change: |
    | --- | --- |
    | **User visual experience** &gt; **User notifications** | Select **Hide in Software center and all notifications** |
    | **Deadline behavior** | Select **Software Update Installation** |
    | **Device restart behavior** | Select **Servers** |
    | **Write filter handling for Windows Embedded devices** | Select **Commit changes at deadline or during a maintenance windows (requires restarts)** |
7. Select **Next**. On the **Alerts** page, under **Specify software update alert options for this deployment**, select **Generate an alert when this Rule fails**, and then select **Next**.
8. On the top-level **Deployment Package** page, under **Select deployment package for this automatic deployment rule**, select **Create a new deployment package**, and then do the following:

    | In: | Change: |
    | --- | --- |
    | **Name** | Type a name for your new deployment package. For example, type *MDE-MDAV Security Intelligence Update*. |
    | **Description** | Type a brief description for your new deployment package |
    | **Package Source (Example): \*server\_name*\_folder path\_** | Type the path to your package source. For example, type *\sccm\deployment\MDE-MDAV\_Security\_Intelligence\_Updates\_Pilot* or select **Browse** to navigate to - and select - your package source. |
    | **Sending priority:** | Select **High** and select **Enable binary differential replication** |
9. Select **Next**. On the **Distribution point** page, under **Specify the distribution points or distribution point groups to host the content**, select **Add** and then specify your distribution point or distribution point groups.
10. Select **Next**. On the **Distribution location** page, under **Specify download location for this Automatic Deployment Rule**, select **Download software updates from the Internet**, and then select **Next**.
11. On the **Distribution location** page, under **Specify the update languages for product**, under **product**, select **Windows Update**.
12. Select **Next**. On the **Download Settings** page, under **Specify the software updates download behavior for clients on slow site boundaries**, select the following:

    | In: | Change: |
    | --- | --- |
    | **Name** | In **Deployment options** select **Download software updates from distribution point and install** |
    | **Deployment options** | Select **Download and install software updates from the distribution points in site default boundary group** |
    | **Deployment options** | Select **"Prefer cloud based sources over on-premises sources" is configures in the boundary group settings, Microsoft update will be the preferred source.** |
13. Select **Next**. On the **Summary** page, under **Confirm the settings**, review the settings. Example settings are shown in the following figure.

    [![Shows the configuration details for the newly configured Automatic Deployment Rule.](media/microsoft-defender-antivirus-deploy-ring-sccm-wizard-confirm-settings.png)](media/microsoft-defender-antivirus-deploy-ring-sccm-wizard-confirm-settings.png#lightbox)
14. Select **Next**. Wait until the process completes and the **Completion** page opens. Select **Close** to finish the process. Automatic Deployment rules are saved, and can be managed from the location shown in the following figure:

    [![Shows the Configuration Manager Software library and configured Automatic Deployment Rules.](media/microsoft-defender-antivirus-deploy-ring-sccm-manage-pilot-policys.png)](media/microsoft-defender-antivirus-deploy-ring-sccm-manage-pilot-policys.png#lightbox)

## Setting up the production environment

1. In the System Center Configuration Manager &gt; **Create Automatic Deployment Rule Wizard** &gt; **General** page, in **Specify the setting for this automatic deployment rule**, make the following settings:

    | In: | Change: |
    | --- | --- |
    | **Name** | Type a name for your deployment rule. For example, type *MDE-MDAV\_Security\_Intelligence\_Update\_Production* |
    | **Description** | Type a brief description for your pilot |
    | **Template** | Select **SCEP and Windows Defender Antivirus Updates** |
    | **Collection** | Type **Windows\_Security\_Intelligence\_Production** |
    | **Each time the rule runs and finds new updates**. | Select **Add to an existing Software Update Group** |
    | **Each time the rule runs and finds new updates** | Select **Enable the deployment after this rule is run** |
2. Select **Next**. On the **Deployment Settings** page, under **Specify the settings for this Automatic Deployment Rule**, then do the following:

    | In: | Change: |
    | --- | --- |
    | **Type of deployment** | Select **Required** |
    | **Detail level** | Select **Only error messages** |
    | **Some software updates include a license agreement** | Select **Automatically deploy all software updates found by this rule, and approve any license agreements**. |
3. Select **Next**. On the **Software Updates** page, under **Select the property filters and search criteria**, enter the following:

    | In: | Change: |
    | --- | --- |
    | **Property filters** | Select **Product** and **Update Classification** |
    | **Search Criteria** | Enter the following product and update classifications: **Article ID** = *2267602***Date Released or Revised** = *Last 1 month***Product** = *Windows Defender***Superseded** = *No***Update Classification** = *Critical Updates* OR *Definition Updates* |

    Tip

    Click **Preview** - to make sure "Security Intelligence Update for Windows Defender Antivirus" is listed. You should see **KB2267602**.

    Note

    **Date Released or Revised: Last 1 month** - If your WSUS/SUP have been healthy, you may want to set this to **Last 1 week**.

    **Product: "Windows Defender"** - We are removing "System Center Endpoint Protection", because we want to target this to only the operating systems that have Microsoft Defender Antivirus.

    **Update Classification**: "Critical Updates" and "Definition Updates"
4. Select **Next**. On the **Evaluation Schedule** page, under **Specify the recurring schedule for this rule**, select **Run the rule on a schedule**, and then select **Customize**.
5. On the **Deployment Schedule** page, under \*\*Configure schedule details for this deployment, do the following:

    | In: | Change: |
    | --- | --- |
    | **Schedule evaluation** &gt; **Time based on** | Select **UTC** |
    | **Software available time** | Select **As soon as possible** |
    | **Installation deadline** | Select **As soon as possible** |
6. Select **Next**. On the **User Experience** page, under **Specify the user experience for this deployment**, ensure the following are selected:

    | In: | Change: |
    | --- | --- |
    | **User visual experience** &gt; **User notifications** | Select **Hide in Software center and all notifications** |
    | **Deadline behavior** | Select **Software Update Installation** |
    | **Device restart behavior** | Select **Servers** |
    | **Write filter handling for Windows Embedded devices** | Select **Commit changes at deadline or during a maintenance windows (requires restarts)** |
7. Select **Next**. On the **Alerts** page, under **Specify software update alert options for this deployment**, select **Generate an alert when this Rule fails**, select **Browse**, navigate to, and select the deployment package and then select **Next**.
8. On the top-level **Deployment Package** page, under **Select deployment package for this automatic deployment rule**, select **Select a deployment package**.
9. On the **Download Location page**, under **Specify download location for this Automatic Deployment Rule**, select **Download software updates from the Internet**, and then select **Next**.
10. On the **Language Selection** page, under **Specify the update languages for product**, under **Product**, specify the necessary Product and Update languages.
11. Select **Next**. On the **Download Settings** page, under **Specify the software updates download behavior for clients on slow site boundaries**, select the following:

    | In: | Change: |
    | --- | --- |
    | **Deployment options** | Select **Download and install software updates from the distribution points and install** |
    | **Deployment options** | Select **Download and install software updates from the distribution points site default boundary group** |
    | **Deployment options** | Select **"Prefer cloud based sources over on-premises sources" is configures in the boundary group settings, Microsoft update will be the preferred source.** |
12. Select **Next**. On the **Summary** page, under **Confirm the settings**, review the settings. Example settings are shown in the following figure:

    [![Shows as screen capture of the configuration details for the newly configured Automatic Deployment Rule for a production environment.](media/microsoft-defender-antivirus-deploy-ring-sccm-wizard-confirm-production-settings.png)](media/microsoft-defender-antivirus-deploy-ring-sccm-wizard-confirm-production-settings.png#lightbox)
13. Select **Next**. Wait until the process completes and the **Completion** page opens. Select **Close** to finish the process.

### If you encounter problems

1. Navigate to **Software Library**
2. Under **Software Updates**, select on **Automatic Deployment Rules**, right-click on **MDE-MDAV\_Security\_Intelligence\_Update\_Production**, and then select **Disable**. This setting is shown in the following figure:

    [![hows as screen capture of how to disable Automatic Deployment Rules if you encounter errors or problems.](media/microsoft-defender-antivirus-deploy-ring-sccm-disable-automatic-deployment-rules.png)](media/microsoft-defender-antivirus-deploy-ring-sccm-disable-automatic-deployment-rules.png#lightbox)