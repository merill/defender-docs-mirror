---
layout: Conceptual
title: Prepare for Retirement of the Log Analytics Agent - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/prepare-deprecation-log-analytics-mma-agent
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
description: Understand the retirement of the Log Analytics (MMA) agent in Microsoft Defender for Cloud and review the planned changes to Defender plans and features.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 8e27a83d-42d1-3ea4-374e-8a5f210681b2
document_version_independent_id: 2a7c6c85-2ab1-5d1a-45ca-fd94087e116e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/prepare-deprecation-log-analytics-mma-agent.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/prepare-deprecation-log-analytics-mma-agent
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/prepare-deprecation-log-analytics-mma-agent.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 196064bc-1f8a-9b36-d901-098bf8666f0c
---

# Prepare for Retirement of the Log Analytics Agent - Microsoft Defender for Cloud | Microsoft Learn

The Log Analytics agent, also known as the Microsoft Monitoring Agent (MMA), [retired in November 2024 as described in the Defender for Cloud Log Analytics agent retirement plan](https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/microsoft-defender-for-cloud-strategy-and-plan-towards-log/ba-p/3883341). Because of this retirement, the Defender for Servers and Defender for SQL on machines plans in Microsoft Defender for Cloud will be updated, and features that rely on the Log Analytics agent will be redesigned.

This article summarizes plans for the Log Analytics agent (MMA) retirement.

## Prepare Defender for Servers

The Defender for Servers plan uses the Log Analytics agent in general availability (GA) and in AMA for [Defender for Servers agent and feature support](plan-defender-for-servers-agents) (in preview). Here's what's happening with these features going forward:

To simplify onboarding, you get all Defender for Servers security features and capabilities with a single agent ([Microsoft Defender for Endpoint](integration-defender-for-endpoint)), complemented by [agentless machine scanning](concept-agentless-data-collection), without any dependency on Log Analytics agent or Azure Monitor agent (AMA).

- Defender for Servers features, which are based on AMA, are currently in preview and won't be released in GA.
- Features in preview that rely on AMA remain supported until an alternate version of the feature is provided, which relies on the Defender for Endpoint integration or the agentless machine scanning feature.
- By enabling the Defender for Endpoint integration and agentless machine scanning feature before the deprecation takes place, your Defender for Servers deployment will be up to date and supported.

### Feature functionality

The following table summarizes how Defender for Servers features are provided. Most features are already generally available using Defender for Endpoint integration or agentless machine scanning. The remaining Defender for Servers features listed in the following table will either be available in GA by the time the MMA is retired, or will be deprecated.

| Feature | Current support | New support | New experience status |
| --- | --- | --- | --- |
| Defender for Endpoint integration for down-level Windows machines (Windows Server 2016/2012 R2) | Legacy Defender for Endpoint sensor, based on the Log Analytics agent | [Unified agent integration](/en-us/microsoft-365/security/defender-endpoint/configure-server-endpoints) | - Functionality with the MDE unified agent is GA.- Functionality with the legacy Defender for Endpoint sensor using the Log Analytics agent will be deprecated in August 2024. |
| Operating system-level (OS-level) threat detection | Log Analytics agent | Defender for Endpoint agent integration | Functionality with the Defender for Endpoint agent is GA. |
| Adaptive application controls | Log Analytics agent (GA), AMA (Preview) | --- | The adaptive application control feature is set to be deprecated in August 2024. |
| Endpoint protection discovery recommendations | Recommendations that are available through the Foundational Cloud Security Posture Management (CSPM) plan and Defender for Servers, using the Log Analytics agent (GA), AMA (Preview) | Agentless machine scanning | - Functionality with agentless machine scanning has been released to preview in early 2024 as part of Defender for Servers Plan 2 and the Defender CSPM plan.- Azure VMs, Google Cloud Platform (GCP) instances, and Amazon Web Services (AWS) instances are supported. On-premises machines are not supported. |
| Missing OS update recommendation | Recommendations available in the Foundational CSPM and Defender for Servers plans using the Log Analytics agent. | Integration with Update Manager, Microsoft | New recommendations based on Azure Update Manager integration [reached general availability (see OS update recommendations release notes)](release-notes-archive#two-recommendations-related-to-missing-operating-system-os-updates-were-released-to-ga), with no agent dependencies. |
| OS misconfigurations (Microsoft Cloud Security Benchmark) | Recommendations that are available through the Foundational CSPM and Defender for Servers plans using the Log Analytics agent, Guest Configuration extension (Preview). | Guest Configuration extension, as part of Defender for Servers Plan 2. | - Functionality based on Guest Configuration extension will be released to GA in September 2024- For Defender for Cloud customers only: functionality with the Log Analytics agent will be deprecated in November 2024.- Support of this feature for Docker-hub and Azure Virtual Machine Scale Sets will be deprecated in Aug 2024. |
| File integrity monitoring | Log Analytics agent, AMA (Preview) | Defender for Endpoint agent integration | Functionality with the Defender for Endpoint agent will be available in August 2024.- For Defender for Cloud customers only: functionality with the Log Analytics agent will be deprecated in November 2024.- Functionality with AMA will deprecate when the Defender for Endpoint integration is released. |

### Log analytics agent autoprovisioning experience - deprecation plan

As part of the MMA agent retirement, the auto provisioning capability that provides the installation and configuration of the agent for Defender for Cloud customers, will be deprecated as well in 2 stages:

1. **By the end of September 2024** - auto provisioning of MMA will be disabled for customers that are no longer using the capability, as well as for newly created subscriptions:

    - **Existing subscriptions** that switch off MMA auto provisioning after end of September will no longer be able to enable the capability afterwards.
    - On **newly created subscriptions**, auto provisioning can no longer be enabled and is automatically turned off.
2. **End of November 2024** - MMA auto provisioning will be disabled on subscriptions that have not yet switched it off. From that point forward, it is no longer possible to enable MMA auto provisioning on existing subscriptions.

### The 500-MB benefit for data ingestion

To preserve the 500 MB of free data ingestion allowance for the [supported data types](data-ingestion-benefit), you need to migrate from MMA to AMA.

Note

- The benefit is granted to every AMA machine that is part of a subscription with Defender for Servers plan 2 enabled.
- The benefit is granted to the workspace the machine is reporting to.
- The security solution should be installed on the related Workspace. Learn more about [how to configure security events collection with Azure Monitor](https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/how-to-configure-security-events-collection-with-azure-monitor/ba-p/3770719).
- If the machine is reporting to more than one workspace, the benefit will be granted to only one of them.

Learn more about how to [deploy AMA](/en-us/azure/azure-monitor/vm/monitor-virtual-machine-agent).

For SQL servers on machines, we recommend to [migrate to SQL server-targeted Azure Monitoring Agent's (AMA) autoprovisioning process](defender-for-sql-autoprovisioning).

### Changes to legacy Defender for Servers Plan 2 onboarding by using Log Analytics agent

Microsoft is retiring the legacy approach to onboard servers to Defender for Servers Plan 2 that uses the Log Analytics agent and Log Analytics workspaces. The retirement includes the following changes:

- The onboarding experience for [onboarding new non-Azure machines](quickstart-onboard-machines) to Defender for Servers using Log Analytics agents and workspaces is removed from the **Inventory** and **Getting started** pages in the Defender for Cloud portal.
- To avoid losing security coverage on the affected machines that connect to a Log Analytics Workspace, take the following actions for the Agent retirement:

    - If you onboarded non-Azure servers (both on-premises and multicloud) by using the [legacy Log Analytics agent onboarding for non-Azure machines](quickstart-onboard-machines), connect these machines by using Azure Arc-enabled servers to Defender for Servers Plan 2 Azure subscriptions and connectors. For more information about deploying machines at scale, see [Azure Arc server deployment options](/en-us/azure/azure-arc/servers/deployment-options).
    - If you used the legacy approach to enable Defender for Servers Plan 2 on selected Azure VMs, enable Defender for Servers Plan 2 on the Azure subscriptions for these machines. You can then exclude individual machines from the Defender for Servers coverage by using the Defender for Servers [per-resource configuration](tutorial-enable-servers-plan).

The following table summarizes the required action for each server onboarded to Defender for Servers Plan 2 through the legacy approach:

| Machine type | Action required to preserve security coverage |
| --- | --- |
| On-premises servers | [Onboarded to Azure Arc](/en-us/azure/azure-arc/servers/deployment-options) and connected to a subscription with Defender for Servers Plan 2 |
| Azure Virtual Machines | Connect to subscription with Defender for Servers Plan 2 |
| Multicloud Servers | Connect to [multicloud connector](quickstart-onboard-aws) with Azure Arc provisioning and Defender for Servers Plan 2 |

### System update and patch recommendations experience - changes and migration guidance

System updates and patches are crucial for keeping the security and health of your machines. Updates often contain security patches for vulnerabilities that, if left unfixed, are exploitable by bad actors.

Defender for Cloud Foundational CSPM and the Defender for Servers plans previously provided system update recommendations by using the Log Analytics agent. The previous Log Analytics agent-based system updates recommendation experience has been replaced by security recommendations that are gathered by using [Azure Update Manager](/en-us/azure/update-manager/overview?branch=main) and constructed out of two new recommendations:

- [Machines should be configured to periodically check for missing system updates](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/2Fbd876905-5b84-4f73-ab2d-2e7a7c4568d9)
- [System updates should be installed on your machines (powered by Azure Update Manager)](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/e1145ab1-eb4f-43d8-911b-36ddf771d13f)

Learn how to [Remediate system updates and patch recommendations on your machines](enable-periodic-system-updates).

#### Which recommendations are being replaced?

The following table summarizes the timetable for recommendations being deprecated and replaced.

| Recommendation | Agent | Supported resources | Deprecation date | Replacement recommendation |
| --- | --- | --- | --- | --- |
| [System updates should be installed on your machines](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/SystemUpdatesRecommendationDetailsWithRulesBlade/assessmentKey/4ab6e3c5-74dd-8b35-9ab9-f61b30875b27) | MMA | Azure and non-Azure (Windows and Linux) | August 2024 | [System updates should be installed on your machines (powered by Azure Update Manager)](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/e1145ab1-eb4f-43d8-911b-36ddf771d13f) |
| [System updates on virtual machine scale sets should be installed](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/GenericRecommendationDetailsBlade/assessmentKey/bd20bd91-aaf1-7f14-b6e4-866de2f43146) | MMA | Azure Virtual Machine Scale Sets | August 2024 | No replacement |

#### How do I prepare for the new recommendations?

- Connect your non-Azure machines to Arc.
- Ensure that [periodic assessment](/en-us/azure/update-manager/assessment-options) update setting is enabled on your machines. You can enable it in two ways:

    - Fix the recommendation: Machines should be configured to periodically check for missing system updates, by using Azure Update Manager.
    - Enable periodic assessment [at scale with Azure Policy](/en-us/azure/update-manager/periodic-assessment-at-scale?branch=main).
- When you complete these steps, Update Manager can fetch the latest updates to the machines, and you can view the latest machine compliance status.

Note

Enabling periodic assessments for Arc-enabled machines that aren't in a subscription or connector with Defender for Servers Plan 2 enabled is subject to [Azure Update Manager pricing](https://azure.microsoft.com/pricing/details/azure-update-management-center/). **Arc-enabled machines in a subscription or connector with Defender for Servers Plan 2 enabled, and any Azure VM, are eligible for this capability at no additional cost.**

### Endpoint protection recommendations experience - changes and migration guidance

Endpoint discovery and recommendations were previously provided by the Defender for Cloud Foundational CSPM and the Defender for Servers plans using the Log Analytics agent in GA, or in preview via the AMA. The previous MMA and AMA-based endpoint discovery and recommendation experiences have been replaced by security recommendations that are gathered using agentless machine scanning.

Endpoint protection recommendations are constructed in two stages. The first stage is endpoint detection and response solution discovery. The second stage is assessment of the solution's configuration. The following tables provide details of the current and new experiences for each stage.

Learn how to [manage the new endpoint detection and response recommendations (agentless)](endpoint-detection-response).

#### Endpoint detection and response solution - discovery

The following table compares the current and new discovery experiences for endpoint detection and response solutions.

| Area | Current experience (based on AMA/MMA) | New experience (based on agentless machine scanning) |
| --- | --- | --- |
| **What's needed to classify a resource as healthy?** | An antivirus is in place. | An endpoint detection and response solution is in place. |
| **What's needed to get the recommendation?** | Log Analytics agent | Agentless machine scanning |
| **What plans are supported?** | - Foundational CSPM (free)- Defender for Servers Plan 1 and Plan 2 | - Defender CSPM- Defender for Servers Plan 2 |
| **What fix is available?** | Install Microsoft anti-malware. | Install Defender for Endpoint on selected machines/subscriptions. |

#### Endpoint detection and response solution - configuration assessment

The following table compares the current and new configuration assessment experiences for endpoint detection and response solutions.

| Area | Current experience (based on AMA/MMA) | New experience (based on agentless machine scanning) |
| --- | --- | --- |
| Resources are classified as unhealthy if one or more of the security checks aren't healthy. | Three security checks:- Real time protection is off- Signatures are out of date.- Both quick scan and full scan aren't run for seven days. | Three security checks:- Antivirus is off or partially configured- Signatures are out of date- Both quick scan and full scan aren't run for seven days. |
| Prerequisites to get the recommendation | An anti-malware solution in place | An endpoint detection and response solution in place. |

#### Which recommendations are being deprecated?

The following table summarizes the timetable for recommendations being deprecated and replaced.

| Recommendation | Agent | Supported resources | Deprecation date | Replacement recommendation |
| --- | --- | --- | --- | --- |
| [Endpoint protection should be installed on your machines](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/GenericRecommendationDetailsBlade/assessmentKey/4fb67663-9ab9-475d-b026-8c544cced439) (public) | MMA/AMA | Azure & non-Azure (Windows & Linux) | July 2024 | [New agentless endpoint protection recommendation](upcoming-changes#changes-in-endpoint-protection-recommendations) |
| [Endpoint protection health issues should be resolved on your machines](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/GenericRecommendationDetailsBlade/assessmentKey/37a3689a-818e-4a0e-82ac-b1392b9bb000) (public) | MMA/AMA | Azure (Windows) | July 2024 | [New agentless endpoint protection recommendation](upcoming-changes#changes-in-endpoint-protection-recommendations) |
| [Endpoint protection health failures on virtual machine scale sets should be resolved](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/GenericRecommendationDetailsBlade/assessmentKey/e71020c2-860c-3235-cd39-04f3f8c936d2) | MMA | Azure Virtual Machine Scale Sets | August 2024 | No replacement |
| [Endpoint protection solution should be installed on virtual machine scale sets](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/GenericRecommendationDetailsBlade/assessmentKey/21300918-b2e3-0346-785f-c77ff57d243b) | MMA | Azure Virtual Machine Scale Sets | August 2024 | No replacement |
| [Endpoint protection solution should be on machines](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/GenericRecommendationDetailsBlade/assessmentKey/383cf3bc-fdf9-4a02-120a-3e7e36c6bfee) | MMA | Non-Azure resources (Windows) | August 2024 | No replacement |
| [Install endpoint protection solution on your machines](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/GenericRecommendationDetailsBlade/assessmentKey/83f577bd-a1b6-b7e1-0891-12ca19d1e6df) | MMA | Azure and non-Azure (Windows) | August 2024 | [New agentless recommendation](upcoming-changes#changes-in-endpoint-protection-recommendations) |
| [Endpoint protection health issues on machines should be resolved](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/GenericRecommendationDetailsBlade/assessmentKey/3bcd234d-c9c7-c2a2-89e0-c01f419c1a8a) | MMA | Azure and non-Azure (Windows and Linux) | August 2024 | [New agentless recommendation](upcoming-changes#changes-in-endpoint-protection-recommendations). |

The [new agentless endpoint protection recommendations](upcoming-changes#changes-in-endpoint-protection-recommendations) experience based on agentless machine scanning support both Windows and Linux OS for multicloud machines.

#### How will the replacement work?

- Current recommendations provided by the Log Analytics Agent or the AMA will be deprecated over time.
- Some of these existing recommendations will be replaced by new recommendations based on agentless machine scanning.
- Recommendations currently in GA remain in place until the Log Analytics agent retires.
- Recommendations that are currently in preview will be replaced when the new recommendation is available in preview.

#### What's happening with secure score?

The following points explain how secure score is affected during the transition from MMA-based to agentless endpoint protection recommendations.

- Recommendations that are currently in GA will continue to affect secure score.
- Current and upcoming new recommendations are located under the same Microsoft Cloud Security Benchmark control, ensuring that there's no duplicate impact on secure score.

#### How do I prepare for the new recommendations?

To prepare for the new agentless endpoint protection recommendations, take the following actions:

- Ensure that [agentless machine scanning is enabled](enable-agentless-scanning-vms) as part of Defender for Servers Plan 2 or Defender Cloud Security Posture Management.
- If suitable for your environment, remove deprecated recommendations when the replacement GA recommendation becomes available. To do that, disable the recommendation in the [built-in Defender for Cloud initiative in Azure Policy](policy-reference).

### File Integrity Monitoring experience - changes and migration guidance

Defender for Servers Plan 2 now offers a new File Integrity Monitoring (FIM) solution powered by Defender for Endpoint (MDE) integration. After FIM powered by MDE is generally available, the Defender for Cloud portal experience for FIM powered by AMA will be removed. In November, FIM powered by MMA will be deprecated.

#### Migration from FIM over AMA

If you currently use FIM over AMA:

- You can no longer onboard new subscriptions or servers to FIM based on AMA and the change tracking extension or view changes through the Defender for Cloud portal beginning May 30.
- If you want to continue consuming FIM events collected by AMA, you can manually connect to the relevant workspace and view changes in the Change Tracking table with the following query:

    ```kusto
    ConfigurationChange
    
    | where TimeGenerated > ago(14d)
    
    | where ConfigChangeType in ('Registry', 'Files') 
    
    | summarize count() by Computer, ConfigChangeType
    ```
- If you want to continue onboarding new scopes or configure monitoring rules, you can manually use [Data Connection Rules](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview) to configure or customize various aspects of data collection.
- Defender for Cloud recommends disabling FIM over AMA, and onboarding your environment to the new FIM version based on Defender for Endpoint upon release.

#### Disable FIM over AMA

To disable FIM over AMA, remove the Azure Change Tracking solution. For more information, see [Remove ChangeTracking solution](/en-us/azure/automation/change-tracking/remove-feature#remove-changetracking-solution).

Alternatively, you can remove the related file change tracking Data collection rules (DCR). For more information, see [Remove-AzDataCollectionRuleAssociation](/en-us/powershell/module/az.monitor/remove-azdatacollectionruleassociation) or [Remove-AzDataCollectionRule](/en-us/powershell/module/az.monitor/remove-azdatacollectionrule).

After you disable the file events collection by using one of the methods above:

- New events stop being collected on the selected scope.
- The historical events that already were collected remain stored in the relevant workspace under the *ConfigurationChange* table in the **Change Tracking** section. These events remain available in the relevant workspace according to the retention period defined in this workspace. For more information, see [How retention and archiving work](/en-us/azure/azure-monitor/logs/data-retention-archive#how-retention-and-archiving-work).

#### Migrate from FIM over Log Analytics Agent (MMA)

If you currently use FIM over the Log Analytics Agent (MMA):

- File Integrity Monitoring based on Log Analytics Agent (MMA) will be deprecated at the end of November 2024.
- Defender for Cloud recommends disabling FIM over MMA, and onboarding your environment to the new FIM version based on Defender for Endpoint upon release.

#### Disable FIM over MMA

To disable FIM over MMA, remove the Azure Change Tracking solution. For more information, see [Remove ChangeTracking solution](/en-us/azure/automation/change-tracking/remove-feature#remove-changetracking-solution).

After you disable the file events collection:

- New events stop being collected on the selected scope.
- The historical events that already were collected remain stored in the relevant workspace under the *ConfigurationChange* table in the **Change Tracking** section. These events remain available in the relevant workspace according to the retention period defined in this workspace. For more information, see [How retention and archiving work](/en-us/azure/azure-monitor/logs/data-retention-archive#how-retention-and-archiving-work).

## Baseline experience changes and migration guidance

The baselines misconfiguration feature on VMs helps ensure that your VMs follow security best practices and organizational policies. Baselines misconfiguration checks your VMs against predefined security baselines and identifies any deviations or misconfigurations that could pose a risk to your environment.

The Log Analytics agent (also known as the Microsoft Monitoring agent or MMA) retired in November 2024, and the following changes apply:

- Machine information is collected by using the [Azure Policy guest configuration](/en-us/azure/virtual-machines/extensions/guest-configuration).
- The following Azure policies are enabled with Azure Policy guest configuration:

    - "Windows machines should meet requirements of the Azure compute security baseline"
    - "Linux machines should meet requirements for the Azure compute security baseline"

    Note

    If you remove these policies, you lose access to the benefits of the Azure Policy guest configuration extension.
- Defender for Cloud foundational CSPM no longer includes OS recommendations based on compute security baselines. These recommendations are available when you [enable the Defender for Servers Plan 2](tutorial-enable-servers-plan).

To learn about Defender for Servers Plan 2 pricing, review the [Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

Important

Be aware that Azure Policy guest configuration provides features outside of the Defender for Cloud portal that aren't included with Defender for Cloud. These features are subject to Azure Policy guest configurations pricing policies. For example, [remediation](/en-us/azure/governance/machine-configuration/concepts/remediation-options) and [custom policies](/en-us/azure/governance/machine-configuration/how-to/create-policy-definition). For more information, see the [Azure Policy guest configuration pricing page](https://azure.microsoft.com/pricing/details/azure-policy/?msockid=06fc23a2aac2601229353214abbf61f1).

Recommendations that the MCSB provides and that aren't part of Windows and Linux compute security baselines continue to be part of free foundational CSPM.

### Install Azure Policy guest configuration

To continue receiving the baseline experience, you need to enable the Defender for Servers Plan 2 and install the Azure Policy guest configuration. When you enable Defender for Servers Plan 2 and install the Azure Policy guest configuration, you ensure that you continue to receive the same recommendations and hardening guidance that you received through the baseline experience.

Depending on your environment, you might need to take the following steps:

1. Review the [support matrix for the Azure Policy guest configuration](/en-us/azure/governance/machine-configuration/overview).
2. Install the Azure Policy guest configuration on your machines.

    - **Azure machines**: In the Defender for Cloud portal, on the recommendations page, search for and select [Guest Configuration extension should be installed on machines](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/6c99f570-2ce7-46bc-8175-cde013df43bc), and [remediate the recommendation](implement-security-recommendations).
    - (**Azure VMs only**) You must assign a managed identity.

        - In the Defender for Cloud portal, on the recommendations page, search for and select [Virtual machines' Guest Configuration extension should be deployed with system-assigned managed identity](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/69133b6b-695a-43eb-a763-221e19556755), and [remediate the recommendation](implement-security-recommendations).
    - (**Azure VMs only**) Optional: To autoprovision the Azure Policy guest configuration for your entire subscription, you can enable the Guest Configuration agent (preview).

        - To enable the Guest Configuration agent:

            1. Sign in to the [Azure portal](https://portal.azure.com/).
            2. Navigate to **Environment settings** &gt; **Your subscription** &gt; **Settings & Monitoring**.
            3. Select **Guest Configuration**.

                [![Screenshot that shows the location of the settings and monitoring button.](media/prepare-deprecation-log-analytics-mma-agent/setting-and-monitoring.png)](media/prepare-deprecation-log-analytics-mma-agent/setting-and-monitoring.png#lightbox)
            4. Toggle the Guest Configuration agent (preview) to **On**.

                [![Screenshot that shows the location of the toggle button to enable the Guest Configuration agent.](media/prepare-deprecation-log-analytics-mma-agent/toggle-guest.png)](media/prepare-deprecation-log-analytics-mma-agent/toggle-guest.png#lightbox)
            5. Select **Continue**.
    - **GCP and AWS**: Azure Policy guest configuration is automatically installed when you [connect your GCP project](quickstart-onboard-gcp), or you [connect your AWS accounts](quickstart-onboard-aws) with Azure Arc autoprovisioning enabled, to Defender for Cloud.
    - **On-premises machines**: The Azure Policy guest configuration is enabled by default when you [onboard on-premises machines as Azure Arc enabled machine or VMs](/en-us/azure/azure-arc/servers/learn/quick-enable-hybrid-vm?branch=main).

After you complete the necessary steps to install the Azure Policy guest configuration, you automatically gain access to the baseline features based on the Azure Policy guest configuration. When you install the Azure Policy guest configuration, you ensure that you continue to receive the same recommendations and hardening guidance that you received through the baseline experience.

### Changes to recommendations

With the deprecation of the MMA, the following MMA-based recommendations are set to be deprecated:

- [Machines should be configured securely](recommendations-reference-compute)
- [Auto provisioning of the Log Analytics agent should be enabled on subscriptions](recommendations-reference-data)

The deprecated recommendations are replaced by the following Azure Policy guest configuration-based recommendations:

- [Vulnerabilities in security configuration on your Windows machines should be remediated (powered by Guest Configuration)](recommendations-reference-compute)
- [Vulnerabilities in security configuration on your Linux machines should be remediated (powered by Guest Configuration)](recommendations-reference-compute)
- [Guest Configuration extension should be installed on machines](recommendations-reference-compute)

### Duplicate recommendations

When you enable Defender for Cloud on an Azure subscription, the [Microsoft cloud security benchmark (MCSB)](/en-us/security/benchmark/azure/introduction), including compute security baselines that assess machine OS compliance, is enabled as a default compliance standard. Free foundational cloud security posture management (CSPM) in Defender for Cloud makes security recommendations based on the MCSB.

If a machine is running both the MMA and the Azure Policy guest configuration, you see duplicate recommendations. The duplication of recommendations occurs because both methods run at the same time and produce the same recommendations. These duplicates affect your Compliance and Secure Score.

To avoid duplicate recommendations while both the MMA and Azure Policy guest configuration are running, you can disable the MMA recommendations `Machines should be configured securely` and `Auto provisioning of the Log Analytics agent should be enabled on subscriptions` by going to the Regulatory compliance page in Defender for Cloud.

[![Screenshot of the regulatory compliance dashboard that shows where one of the MMA recommendations exist.](media/prepare-deprecation-log-analytics-mma-agent/exempt-recommendation.png)](media/prepare-deprecation-log-analytics-mma-agent/exempt-recommendation.png#lightbox)

After you locate the recommendation, select the relevant machines and exempt them.

[![Screenshot that shows you how to select machines and exempt them.](media/prepare-deprecation-log-analytics-mma-agent/exempt-regulatory.png)](media/prepare-deprecation-log-analytics-mma-agent/exempt-regulatory.png#lightbox)

Some of the baseline configuration rules powered by the Azure Policy guest configuration tool are more current and offer broader coverage. As a result, transition to the Baselines feature powered by Azure Policy guest configuration can affect your compliance status since they include checks that might not have been performed previously.

### Query recommendations

With the retirement of the MMA, Defender for Cloud no longer queries recommendations through the Log Analytics workspace information. Instead, Defender for Cloud now uses Azure Resource Graph for API and portal queries to query recommendation information.

Here are two sample queries you can use:

- **Query all unhealthy rules for a specific resource**

    ```rest
    Securityresources 
    | where type == "microsoft.security/assessments/subassessments" 
    | extend assessmentKey=extract(@"(?i)providers/Microsoft.Security/assessments/([^/]*)", 1, id) 
    | where assessmentKey == '1f655fb7-63ca-4980-91a3-56dbc2b715c6' or assessmentKey ==  '8c3d9ad0-3639-4686-9cd2-2b2ab2609bda' 
    | parse-where id with machineId:string '/providers/Microsoft.Security/' * 
    | where machineId  == '{machineId}'
    ```
- **All Unhealthy Rules and the amount if Unhealthy machines for each**

    ```rest
    securityresources 
    | where type == "microsoft.security/assessments/subassessments" 
    | extend assessmentKey=extract(@"(?i)providers/Microsoft.Security/assessments/([^/]*)", 1, id) 
    | where assessmentKey == '1f655fb7-63ca-4980-91a3-56dbc2b715c6' or assessmentKey ==  '8c3d9ad0-3639-4686-9cd2-2b2ab2609bda' 
    | parse-where id with * '/subassessments/' subAssessmentId:string 
    | parse-where id with machineId:string '/providers/Microsoft.Security/' * 
    | extend status = tostring(properties.status.code) 
    | summarize count() by subAssessmentId, status
    ```

## Plan your Log Analytics agent migration

### Migration planning matrix

Plan agent migration according to your business requirements. The following migration-planning table summarizes the guidance.

| Are you using Defender for Servers? | Are these Defender for Servers features required in GA: file integrity monitoring, endpoint protection recommendations, security baseline recommendations? | Are you using Defender for SQL servers on machines or AMA log collection? | Migration plan |
| --- | --- | --- | --- |
| Yes | Yes | No | 1. Enable [Defender for Endpoint integration](enable-defender-for-endpoint) and [agentless machine scanning](enable-agentless-scanning-vms).2. Wait for GA of all features with the alternative's platform (you can use preview version earlier).3. Once features are GA, disable the [Log Analytics agent](defender-for-sql-autoprovisioning#disable-the-log-analytics-agentazure-monitor-agent). |
| No | --- | No | You can remove the Log Analytics agent now. |
| No | --- | Yes | 1. You can [migrate to SQL autoprovisioning for AMA](defender-for-sql-autoprovisioning) now.2. [Disable](defender-for-sql-autoprovisioning#disable-the-log-analytics-agentazure-monitor-agent) Log Analytics/Azure Monitor Agent. |
| Yes | Yes | Yes | 1. Enable [Defender for Endpoint integration](enable-defender-for-endpoint) and [agentless machine scanning](enable-agentless-scanning-vms).2. You can use the Log Analytics agent and AMA side-by-side to get all features in GA. See [auto-deploy the Azure Monitor Agent](auto-deploy-azure-monitoring-agent) for details about running agents side-by-side.3. Migrate to [SQL autoprovisioning for AMA](defender-for-sql-autoprovisioning) in Defender for SQL on machines. Alternatively, start the migration from Log Analytics agent to AMA in April 2024.4. Once the migration is finished, [disable](defender-for-sql-autoprovisioning#disable-the-log-analytics-agentazure-monitor-agent) the Log Analytics agent. |
| Yes | No | Yes | 1. Enable [Defender for Endpoint integration](enable-defender-for-endpoint) and [agentless machine scanning](enable-agentless-scanning-vms).2. You can migrate to [SQL autoprovisioning for AMA](defender-for-sql-autoprovisioning) in Defender for SQL on machines now.3. [Disable](defender-for-sql-autoprovisioning#disable-the-log-analytics-agentazure-monitor-agent) the Log Analytics agent. |

### Use the MMA migration experience

The MMA migration experience is a tool that helps you migrate from the MMA to the AMA. The experience provides a step-by-step guide to help you migrate your machines from the MMA to the AMA.

By using the MMA migration experience, you can:

- Migrate servers from the legacy onboarding through the Log Analytics workspace.
- Ensure subscriptions meet all of the prerequisites to receive all of Defender for Servers Plan 2's benefits.
- Migrate to FIM's new version over MDE.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Defender for Cloud** &gt; **Environment settings**.
3. Select **MMA migration**.

    [![Screenshot that shows where the MMA migration button is located.](media/prepare-deprecation-log-analytics-mma-agent/mma-migration.png)](media/prepare-deprecation-log-analytics-mma-agent/mma-migration.png#lightbox)
4. Select **Take action** for one of the available actions:

    [![Screenshot that shows where the take action button is located for all of the options.](media/prepare-deprecation-log-analytics-mma-agent/take-action.png)](media/prepare-deprecation-log-analytics-mma-agent/take-action.png#lightbox)

Allow the experience to load and follow the steps to complete the migration.