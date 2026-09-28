---
layout: Conceptual
title: Gain Application and End-user Context for AI Alerts - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/gain-end-user-context-ai
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
description: Learn how to improve AI alert triage in Microsoft Defender for Cloud by adding end-user and application context to Azure AI API calls.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: ecc3fdbb-b398-2237-352c-9f5c1fb1ff74
document_version_independent_id: cf712a8b-23ad-2603-0377-33610de79510
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/gain-end-user-context-ai.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/gain-end-user-context-ai
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/gain-end-user-context-ai.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8a6e4dad-7050-4ce7-83f9-eb4123577a54
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/0a5fc323-00ce-4c20-9095-41948f54c83f
platformId: 1c97be9c-4bf0-49f1-6e3f-c7c1efaf3d6a
---

# Gain Application and End-user Context for AI Alerts - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud's threat protection for AI services lets you enhance the actionability and security value of generated AI alerts by providing both end-user and application context.

Most AI service scenarios are built as part of an application, so API calls to the AI service originate from a web application, compute instance, or AI gateway. This application-mediated architecture introduces complexity because investigators lack context when they review AI requests to determine the business application or end-user involved.

Together, Microsoft Defender for Cloud and Azure AI let you add parameters to Azure AI API calls so Defender for Cloud can capture critical end-user or application context in AI alerts. Capturing end-user and application context in AI alerts leads to more effective triage and results. For example, when you add end-user IP or identity, you can block that user or correlate incidents and alerts by that user. When you add application context, you can prioritize or determine whether suspicious behavior is standard for that application in the organization.

[![Screenshot of the Defender XDR portal showing benefits from adding the code.](media/gain-end-user-context-ai/after-code.png)](media/gain-end-user-context-ai/after-code.png#lightbox)

## Prerequisites

- Read up on [AI threat protection](ai-threat-protection).
- [Enable threat protection for AI services](ai-onboarding) on an AI application, with Azure OpenAI underlying model, directly through the Azure OpenAI Service. This feature is currently not supported when applying models consumed through the [Azure AI model inference API](/en-us/azure/ai-studio/ai-services/model-inference).

## Add security parameters to your Azure OpenAI call

To receive AI security alerts with more context, add any or all of the following sample `UserSecurityContext` parameters to your [Azure OpenAI API](/en-us/azure/ai-services/openai/reference) calls.

- All of the fields in the `UserSecurityContext` are optional.
- For end-user context, pass the `EndUserId` and `SourceIP` fields at a minimum. The `EndUserId` and `SourceIP` fields give Security Operations Center (SOC) analysts the ability to investigate security incidents that involve AI resources and generative AI applications.
- For application context, pass the `applicationName` field as a simple string.

If you misspell the name of any `UserSecurityContext` field, the Azure OpenAI API call still succeeds.

Note

The `EndUserId` is the Microsoft Entra ID user object ID used to authenticate end-users in the generative AI application. Don't include sensitive personal information in this field.

## UserSecurityContext schema

You can find the exact schema in Azure OpenAI [REST API reference documentation](/en-us/azure/ai-services/openai/reference-preview).

The [user security context object](/en-us/azure/ai-services/openai/reference-preview#usersecuritycontext) is part of the [request body](/en-us/azure/ai-services/openai/reference-preview#createchatcompletionrequest) of the chat completion API.

Currently, the API doesn't support adding `UserSecurityContext` parameters for Defender for Cloud alert enrichment when you apply models deployed through the [Azure AI model inference API](/en-us/azure/ai-studio/ai-services/model-inference).

## Supported APIs and SDK versions

The following table lists the supported APIs and SDK versions for `UserSecurityContext`.

| Source | Version support | Code Example | Comments |
| --- | --- | --- | --- |
| Azure OpenAI REST API | [2025-01-01 version](/en-us/azure/ai-services/openai/reference-preview) | - | - |
| Azure .NET SDK | [v2.2.0-beta.1 (2025-02-07) or higher](https://github.com/Azure/azure-sdk-for-net/blob/Azure.AI.OpenAI_2.2.0-beta.1/sdk/openai/Azure.AI.OpenAI/CHANGELOG.md) | [GitHub code example](https://github.com/Azure-Samples/signalr-ai-streaming/blob/main/src/AIStreaming/MsDefenderExtension.cs) | - |
| Azure Python SDK | [v1.61.1 or higher](https://github.com/openai/openai-python/releases/tag/v1.61.1) | [GitHub code example](https://github.com/microsoft/sample-app-aoai-chatGPT/blob/main/backend/security/ms_defender_utils.py) | The support is provided by appending to the `extra_body` object. |
| Azure JS/Node SDK | [v4.83.0 or higher](https://github.com/openai/openai-node/releases/tag/v4.83.0) | [GitHub code example](https://github.com/Azure-Samples/openai-secure-ui-js/blob/main/packages/api/src/functions/security/ms-defender-utils.ts) | The support is provided by appending to the `extra_body` object. |
| Azure Go SDK | [v0.7.2 or higher](https://pkg.go.dev/github.com/Azure/azure-sdk-for-go/sdk/ai/azopenai@v0.7.2#UserSecurityContext) | - | - |