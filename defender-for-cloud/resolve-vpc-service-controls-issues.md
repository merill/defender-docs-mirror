---
layout: Conceptual
title: Resolve VPC Service Controls Issues - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/resolve-vpc-service-controls-issues
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
description: Troubleshoot VPC service controls issues in Microsoft Defender for Cloud to ensure your resources are connected and protected.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 97a7508a-31bd-3a3f-9553-874ac82ccdf1
document_version_independent_id: 84464e17-e41e-8e7d-d5e2-5176d4372895
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/resolve-vpc-service-controls-issues.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/resolve-vpc-service-controls-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/resolve-vpc-service-controls-issues.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: bfa555ec-5c9f-31c7-437b-b8f65d8e77c0
---

# Resolve VPC Service Controls Issues - Microsoft Defender for Cloud | Microsoft Learn

Google Cloud Platform (GCP) Virtual Private Cloud (VPC) Service Controls provide an extra layer of security by defining perimeters that isolate and protect sensitive resources. Each perimeter can include one or more projects, restricting access to Google services from outside the defined boundary.

To allow Microsoft Defender for Cloud to scan resources in these protected environments, you need to configure ingress and egress policies that allow Defender for Cloud service accounts to operate inside the perimeter. This configuration ensures that security scans can be performed without compromising the integrity of the perimeter's restrictions.

If you're unsure whether your Defender for Cloud account is experiencing issues with VPC Service Controls, check your [GCP Logs Explorer](troubleshoot-connectors#defender-api-calls-to-gcp) to determine whether VPC Service Controls are blocking Defender for Cloud API calls.

## Prerequisites

Before you configure VPC Service Controls for Defender for Cloud, make sure you have the following prerequisites:

- A Microsoft Azure subscription. If you don't have one, you can [sign up for a free Azure subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) set up on your Azure subscription.
- [A connected GCP project](quickstart-onboard-gcp).
- Contributor level permission for the relevant Azure subscription.

## Add ingress and egress policies

Each VPC Service Controls perimeter in GCP protects one or more projects. Configure any perimeter that restricts Google Services so Defender for Cloud can scan the projects in that perimeter.

1. Sign in to your GCP project.
2. Go to **Security** &gt; **VPC Service Controls**.
3. Select **Edit**.
4. Under the Ingress policy, add the following service accounts:

    - `serviceAccount:mdc-agentless-scanning@guardians-prod-diskscanning.iam.gserviceaccount.com`
    - `serviceAccount:microsoft-defender-cspm@eu-secure-vm-project.iam.gserviceaccount.com`

    Note

    If the microsoft-defender-cspm service account name was changed when the GCP project was connected to MDC, make sure to edit the service account with the correct name. The name can be found by navigating to **IAM & Admin permissions** in your GCP project.
5. Under the Egress policy, add the following service accounts:

    - `serviceAccount:mdc-agentless-scanning@guardians-prod-diskscanning.iam.gserviceaccount.com`
6. Select **Save**.

Defender for Cloud triggers agentless disk scanning by using API calls. You know the ingress and egress policy configuration works after the next scheduled scan API call, which can take up to 24 hours.