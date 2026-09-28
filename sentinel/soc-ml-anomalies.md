---
layout: Conceptual
title: Use customizable anomalies to detect threats in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/soc-ml-anomalies
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: This article explains how to use the new customizable anomaly detection capabilities in Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: feature-guide
ms.date: 2024-03-17T00:00:00.0000000Z
locale: en-us
document_id: b116d095-6a15-0d46-d3f0-ade23c0c430e
document_version_independent_id: d4979509-1979-e74d-e1db-1204e2fe7d35
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/soc-ml-anomalies.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/soc-ml-anomalies
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/soc-ml-anomalies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 82515dba-849e-ad6e-ea12-a0e1d6b60c75
---

# Use customizable anomalies to detect threats in Microsoft Sentinel | Microsoft Learn

Important

[**Custom detections**](/en-us/defender-xdr/custom-detections-overview?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) is now the best way to create new rules across Microsoft Sentinel SIEM Microsoft Defender XDR. With custom detections, you can reduce ingestion costs, get unlimited real-time detections, and benefit from seamless integration with Defender XDR data, functions, and remediation actions with automatic entity mapping. For more information, read [this blog](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/custom-detections-are-now-the-unified-experience-for-creating-detections-in-micr/4463875).

## What are customizable anomalies?

With attackers and defenders constantly fighting for advantage in the cybersecurity arms race, attackers are always finding ways to evade detection. Inevitably, though, attacks still result in unusual behavior in the systems being attacked. Microsoft Sentinel's customizable, machine learning-based anomalies can identify this behavior with analytics rule templates that can be put to work right out of the box. While anomalies don't necessarily indicate malicious or even suspicious behavior by themselves, they can be used to improve detections, investigations, and threat hunting:

- **Additional signals to improve detection**: Security analysts can use anomalies to detect new threats and make existing detections more effective. A single anomaly is not a strong signal of malicious behavior, but a combination of several anomalies at different points on the kill chain sends a clear message. Security analysts can make existing detection alerts more accurate by conditioning them on the identification of anomalous behavior.
- **Evidence during investigations**: Security analysts also can use anomalies during investigations to help confirm a breach, find new paths for investigating it, and assess its potential impact. These efficiencies reduce the time security analysts spend on investigations.
- **The start of proactive threat hunts**: Threat hunters can use anomalies as context to help determine whether their queries uncovered suspicious behavior. When the behavior is suspicious, the anomalies also point toward potential paths for further hunting. These clues provided by anomalies reduce both the time to detect a threat and its chance to cause harm.

Anomalies can be powerful tools, but they are notoriously noisy. They typically require a lot of tedious tuning for specific environments, or complex post-processing. Customizable anomaly templates are tuned by Microsoft Sentinel's data science team to provide out-of-the-box value. If you need to tune them further, the process is simple and requires no knowledge of machine learning. The thresholds and parameters for many of the anomalies can be configured and fine-tuned through the already familiar analytics rule user interface. The performance of the original threshold and parameters can be compared to the new ones within the interface and further tuned as necessary during a testing, or flighting, phase. Once the anomaly meets the performance objectives, the anomaly with the new threshold or parameters can be promoted to production with the click of a button. Microsoft Sentinel customizable anomalies enable you to get the benefit of anomaly detection without the hard work.

## UEBA anomalies

Some of Microsoft Sentinel's anomaly detections come from its [User and Entity Behavior Analytics (UEBA) engine](identify-threats-with-entity-behavior-analytics), which detects anomalies based on each entity's baseline historical behavior across various environments. Each entity's baseline behavior is set according to its own historical activities, those of its peers, and those of the organization as a whole. Anomalies can be triggered by the correlation of different attributes such as action type, geo-location, device, resource, ISP, and more.