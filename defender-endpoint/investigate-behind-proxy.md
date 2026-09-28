---
layout: Conceptual
title: Investigate connection events that occur behind forward proxies - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/investigate-behind-proxy
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use advanced HTTP level monitoring through network protection in Microsoft Defender for Endpoint, which surfaces a real target, instead of a proxy.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- mde-edr
ms.topic: how-to
ms.subservice: edr
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 7792d8ad-1d7a-e906-bc9f-467afb5adffe
document_version_independent_id: 7792d8ad-1d7a-e906-bc9f-467afb5adffe
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/investigate-behind-proxy.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: investigate-behind-proxy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/investigate-behind-proxy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 9e36c464-92db-2109-0adc-0bf82456a284
---

# Investigate connection events that occur behind forward proxies - Microsoft Defender for Endpoint | Microsoft Learn

Defender for Endpoint supports network connection monitoring from different levels of the network stack. A challenging case is when the network uses a forward proxy as a gateway to the Internet.

The proxy acts as if it was the target endpoint. When a forward proxy acts as the target endpoint, simple network connection monitors audit the connections with the proxy that is correct but has lower investigation value.

Defender for Endpoint supports advanced HTTP level monitoring through network protection. When network protection is turned on, a new type of event is surfaced that exposes the real target domain names.

## Use network protection to monitor connections behind a forward proxy or firewall

Monitoring network connection behind a forward proxy is possible due to other network events that originate from network protection. To see these network events on a device timeline, turn on network protection (at the minimum in audit mode).

Network protection can be controlled using the following modes:

- **Block**: Users or apps are blocked from connecting to dangerous domains. You'll be able to see this activity in the Defender portal.
- **Audit**: Users or apps won't be blocked from connecting to dangerous domains. However, you'll still see this activity in the Defender portal.

If you turn off network protection, users or apps won't be blocked from connecting to dangerous domains. You won't see any network activity in Microsoft Defender XDR.

If you don't configure it, network blocking is turned off by default.

For more information, see [Enable network protection](enable-network-protection).

## How network protection reveals real targets behind forward proxies

When network protection is turned on, a device's timeline shows the proxy IP address while also displaying the real target address.

[![The network events on device's timeline](media/atp-proxy-investigation.png)](media/atp-proxy-investigation.png#lightbox)

Additional network protection connection events are available to surface the real domain names even behind a proxy.

Event's information:

[![The URLs of a single network event](media/atp-proxy-investigation-event.png)](media/atp-proxy-investigation-event.png#lightbox)

## Hunt for connection events using advanced hunting

The network protection connection events are also available through advanced hunting. You can find them in the DeviceNetworkEvents table under the `ConnectionSuccess` action type.

The following query returns all relevant ConnectionSuccess events:

```console
DeviceNetworkEvents
| where ActionType == "ConnectionSuccess"
| take 10
```

[![The advanced hunting query](media/atp-proxy-investigation-ah.png)](media/atp-proxy-investigation-ah.png#lightbox)

You can also filter out events that are related to connection to the proxy itself.

Use the following query to filter out the connections to the proxy:

```console
DeviceNetworkEvents
| where ActionType == "ConnectionSuccess" and RemoteIP != "ProxyIP"
| take 10
```