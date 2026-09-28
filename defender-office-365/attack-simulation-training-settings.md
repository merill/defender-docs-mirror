---
layout: Conceptual
title: Global settings in Attack simulation training - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/attack-simulation-training-settings
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.service: defender-office-365
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
description: Admins can learn how to configure global settings in Attack simulation training in Microsoft Defender for Office 365 Plan 2.
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 43c97462-457f-e827-00fd-fb2364aea1fd
document_version_independent_id: 43c97462-457f-e827-00fd-fb2364aea1fd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/attack-simulation-training-settings.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: attack-simulation-training-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/attack-simulation-training-settings.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 06a4eea6-73d8-f6d6-4560-0991f7a99ab2
---

# Global settings in Attack simulation training - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In Attack simulation training in Microsoft 365 E5 or Microsoft Defender for Office 365 Plan 2, the **Settings** tab contains settings that affect all simulations:

- **Repeat offender threshold**: A *repeat offender* is someone who gives up their credentials in multiple consecutive simulations. How many simulations in a row constitute a repeat offender is determined by the repeat offender threshold. Information about repeat offenders appears in the following locations:

    - The [Repeat offenders card on the Overview tab](attack-simulation-training-insights#repeat-offenders-card) and the [Repeat offenders tab in the Attack simulation report](attack-simulation-training-insights#repeat-offenders-tab-for-the-attack-simulation-report).
    - When you select users in [target users for simulations](attack-simulation-training-simulation-automations#target-users), [target users for simulation automations](attack-simulation-training-simulation-automations#target-users), and [target users for training campaigns](attack-simulation-training-training-campaigns#target-users), you can find and filter repeat offenders.
- **Training threshold**: In [Training campaigns](attack-simulation-training-training-campaigns), the *training threshold* specifies a time period in days to prevent users from having the same training modules assigned to them. Specifically, a training module isn't reassigned to users who completed the module during the training threshold, nor is a training module assigned to users who haven't completed modules assigned during the training threshold. For more information, see [Set the training threshold time period](attack-simulation-training-training-campaigns#set-the-training-threshold).
- **View exclude simulations from reporting**: After a simulation has completed, you can exclude the results of the simulation from reporting. For instructions, see [Exclude completed simulations from reporting](attack-simulation-training-simulations#exclude-completed-simulations-from-reporting). You can use the **View all** link in the **Simulations excluded from reporting** section to see excluded simulations on the **Simulations** tab.

To get to the **Settings** tab, do the following steps:

1. Open the Microsoft Defender portal at https://security.microsoft.com.
2. Go to **Email & collaboration** &gt; **Attack simulation training**.
3. Select the **Settings** tab.

To go directly to the **Settings** tab, use https://security.microsoft.com/attacksimulator?viewid=setting.

For getting started information about Attack simulation training, see [Get started using Attack simulation training](attack-simulation-training-get-started).

## Configure the repeat offender threshold

To configure the repeat offender threshold, use the box in the **Repeat offender threshold** section on the **Settings** tab. The default value is 2.

## Configure the training threshold

To configure the training threshold, use the box in the **Training threshold** section on the **Settings** tab. The default value is 90 days.

The training threshold starts from the time that modules are assigned to users.

We recommend that the training threshold is greater than the number of days users have to complete a training module.

To remove the training threshold and always assign training, regardless of whether a user has already completed or been assigned a training, set value to 0.

## View simulations excluded from reporting

To view completed simulations that have been excluded from reporting on the **Settings** tab, select the **View all** link in the **Simulations excluded from reporting** section. This link takes you to the **Simulations** tab at https://security.microsoft.com/attacksimulator?viewid=simulations where **Show excluded simulations** is automatically toggled on ![](media/scc-toggle-on.png) .

On the **Simulations** tab, both excluded *and* included completed simulations are shown on the **Simulations** tab together. You can tell the difference by the **Status** values (**Excluded** vs. **Completed**).

If you go directly to the **Simulations** tab and manually toggle **Show excluded simulations** on ![](media/scc-toggle-on.png) , *only* excluded simulations are shown.

To exclude completed simulations from reporting, see [Exclude completed simulations from reporting](attack-simulation-training-simulations#exclude-completed-simulations-from-reporting).