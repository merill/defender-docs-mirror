---
layout: Conceptual
title: Enable threat protection for AI services - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/ai-onboarding
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
description: Learn how to enable threat protection for AI services on your Azure subscription for Microsoft Defender for Cloud.
ms.topic: install-set-up-deploy
ms.date: 2026-07-29T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d25370c0-1c01-504b-db49-9e200caa8d6a
document_version_independent_id: 47f1c74d-e7ba-a064-cb01-32d2466aa1d4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/ai-onboarding.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/ai-onboarding
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/ai-onboarding.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
platformId: ca55e12f-3398-9e37-b751-c97c51bca088
---

# Enable threat protection for AI services - Microsoft Defender for Cloud | Microsoft Learn

Threat protection for AI services in Microsoft Defender for Cloud protects Microsoft Foundry workloads on an Azure subscription by providing insights to threats that might affect your generative AI applications and agents.

## Prerequisites

- Read the [Overview - AI threat protection](ai-threat-protection).
- You need a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Enable Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.
- Required permissions: To enable the plan, you need **Owner** or **Contributor** level.

## Enable threat protection for AI services

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. In the Defender for Cloud menu, select **Environment settings**.
4. Select the relevant Azure subscription.
5. On the Defender plans page, toggle the AI services to **On**.

    [![Screenshot that shows you how to toggle threat protection for AI services to on.](media/ai-onboarding/enable-ai-workloads-plan.png)](media/ai-onboarding/enable-ai-workloads-plan.png#lightbox)

## Enable the components of the plan

With the AI services threat protection plan enabled, you can control whether the different components of the plan are enabled. This includes:

- **Suspicious prompt evidence**: receive alerts for suspicious portions of user prompts and model responses to help analyze AI-related security alerts, with sensitive data automatically redacted. These prompt snippets appear in the Defender portal as part of each alert’s evidence.
- **Data security for AI interactions**: allows Microsoft Purview to access and analyze prompts, responses, and related metadata to provide data security and compliance capabilities such as SIT classification, auditing, insider risk, communication compliance, and eDiscovery. It is a paid Purview feature and is not included in the Defender for AI Services plan.
- **AI model security**: AI model scanning gives you a clear, unified view of all your models registered in Azure Machine Learning Registries. It helps teams stay ahead of security risks by automatically checking for issues like serialization vulnerabilities, malware, and missing scans. By surfacing misconfigurations and integrating seamlessly with Defender for Cloud and developer workflows, it ensures your AI models are continuously protected and ready for production.

### Enable suspicious prompt evidence

With the AI services threat protection plan enabled, you can control whether alerts include suspicious segments directly from your user's prompts, or the model responses from your AI applications or agents. Enabling user prompt evidence helps you triage, classify alerts and your user's intentions.

User prompt evidence consists of prompts and model responses. Both are considered your data. Evidence is available through the Azure portal, Defender portal, and any attached partner integrations.

If User prompt evidence is disabled, Microsoft Defender for Cloud continues analyzing prompts and responses for threat detection, but the prompt content is masked in alerts.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. In the Defender for Cloud menu, select **Environment settings**.
4. Select the relevant Azure subscription.
5. Locate AI services and select **Settings**.

    [![Screenshot that shows where the settings button is located on the Plans screen.](media/ai-onboarding/select-settings.png)](media/ai-onboarding/select-settings.png#lightbox)
6. Toggle Enable user prompt evidence to **On**.

    [![Screenshot that shows you how to toggle user prompt evidence to on.](media/ai-onboarding/enable-user-prompt-evidence.png)](media/ai-onboarding/enable-user-prompt-evidence.png#lightbox)
7. Select **Continue**.

### Enable Data Security for Microsoft with Microsoft Purview

Important

The current Microsoft Purview configuration method for Microsoft Foundry is being deprecated. A new configuration method is now available. For more information, see [Manage compliance and security in Microsoft Foundry](/en-us/azure/foundry/control-plane/how-to-manage-compliance-security).

Note

This feature requires a Microsoft Purview license, which isn't included with Microsoft Defender for Cloud's Defender for AI Services plan.

To get started with Microsoft Purview DSPM for AI, see [Set up Microsoft Purview DSPM for AI](/en-us/purview/ai-microsoft-purview).

Enable Microsoft Purview to access, process, and store prompt and response data—including associated metadata—from Microsoft Foundry. This integration supports key data security and compliance scenarios such as:

- Sensitive information type (SIT) classification
- Analytics and Reporting through Microsoft Purview DSPM for AI
- Insider Risk Management
- Communication Compliance
- Microsoft Purview Audit
- Data Lifecycle Management
- eDiscovery

This capability helps your organization manage and monitor AI-generated data in alignment with enterprise policies and regulatory requirements.

Note

Microsoft Purview integration does **not** include data or context from Foundry agents. Support for Foundry agent integration is not available at this time and will be communicated in future updates if planned.

Note

Data Security Policies for Microsoft Foundry interactions are supported only for API calls that use Microsoft Entra ID authentication with a user-context token, or for API calls that explicitly include user context. To learn more, see [Gain end-user context for Azure AI API calls](gain-end-user-context-ai). For all other authentication scenarios, user interactions captured in Purview show up only in Purview Audit and DSPM for AI Activity Explorer.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Microsoft Defender for Cloud**.
3. In the Defender for Cloud menu, select **Environment settings**.
4. Select the relevant Azure subscription.
5. Locate AI services and select **Settings**.
6. Toggle Enable data security for AI interactions to **On**. 

    [![Screenshot that shows where the toggle is located for AI interactions is located.](media/ai-onboarding/ai-interactions-on.png)](media/ai-onboarding/ai-interactions-on.png#lightbox)
7. Select **Continue**.

#### **Troubleshooting**

If you don't see user interactions for Entra ID authenticated users in Microsoft Purview Activity Explorer after turning on the toggle, follow these steps to troubleshoot:

Run the following commands in Azure PowerShell

1. Install the following Az modules (if needed): 

    ```PowerShell
    Install-Module -Name Az -AllowClobber
    Import-Module Az.Accounts
    ```
2. Connect to Azure PowerShell as a tenant admin : 

    ```PowerShell
    Connect-AzAccount -Tenant $yourTenantIdHere
    ```
3. On the web page that opens, sign in using your tenant admin credentials.
4. Verify that the Microsoft Purview service principal is in your tenant: 

    ```PowerShell
    Get-AzADServicePrincipal -ApplicationId "9ec59623-ce40-4dc8-a635-ed0275b5d58a"
    ```
5. If the service principal doesn't exist, add the Microsoft Purview app service principal to the tenant: 

    ```PowerShell
    New-AzADServicePrincipal -ApplicationId "9ec59623-ce40-4dc8-a635-ed0275b5d58a"
    ```

### Enable AI model security

AI model security in Defender for Cloud, provides organizations proactive protection for Machine Learning (ML) models. The service scans models for security risks, such as embedded malware, unsafe operators, and exposed secrets, before models reach production.

By integrating directly with Azure Machine Learning workspaces, registries, and continuous integration and continuous delivery (CI/CD) pipelines, Ai model security provides security teams visibility into the safety and compliance status of AI models that exist in their environments.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Microsoft Defender for Cloud**.
3. In the Defender for Cloud menu, select **Environment settings**.
4. Select the relevant Azure subscription.
5. Locate AI services and select **Settings**.
6. Toggle AI model security to **On**.

    [![Screenshot that shows where the toggle for AI model security is located.](media/ai-onboarding/model-security.png)](media/ai-onboarding/model-security.png#lightbox)
7. Select **Continue**.

Learn more about [AI model security](ai-model-security).