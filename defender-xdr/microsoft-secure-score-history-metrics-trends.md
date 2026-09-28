---
layout: Conceptual
title: Track your Microsoft Secure Score history and meet goals - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/microsoft-secure-score-history-metrics-trends
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Gain insights into activity that has affected your Microsoft Secure Score. Discover trends and set goals.
ms.service: defender-xdr
ms.mktglfcycl: deploy
ms.localizationpriority: medium
f1.keywords:
- NOCSH
ms.author: guywild
author: guywi-ms
audience: ITPro
ms.collection:
- m365-security
- tier2
ms.topic: concept-article
search.appverid:
- MOE150
- MET150
ms.date: 2025-04-28T00:00:00.0000000Z
locale: en-us
document_id: 9da1b490-e7fa-e8a0-79d0-3b173505640b
document_version_independent_id: 9da1b490-e7fa-e8a0-79d0-3b173505640b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/microsoft-secure-score-history-metrics-trends.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-secure-score-history-metrics-trends
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/microsoft-secure-score-history-metrics-trends.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: d4a1962e-8f30-7622-7a42-e8e6ab8ec7aa
---

# Track your Microsoft Secure Score history and meet goals - Microsoft Defender XDR | Microsoft Learn

[Microsoft Secure Score](microsoft-secure-score) is a measurement of an organization's security posture, with a higher number indicating more recommended actions taken. It can be found at https://security.microsoft.com/securescore in the [Microsoft Defender portal](microsoft-365-defender-portal).

## Gain insights into activity that has affected your score

View a graph of your organization's score over time in the **History** tab.

Below the graph is a list of all the actions taken in the selected time range and their attributes, such as resulting points and category. You can customize a date range and filter by category.

[![An example of the page that describes the activity history in the Microsoft Defender portal](/en-us/defender-xdr/media/microsoft-secure-score-history-metrics-trends/secure-score-history-activity.png)](/en-us/defender-xdr/media/microsoft-secure-score-history-metrics-trends/secure-score-history-activity.png#lightbox)

If you select the recommended action associated with an activity, the full recommended action flyout will appear.

To view all history for that specific recommended action, select the history link in the flyout.

[![The History pane regarding recommended action in the Microsoft Defender portal](/en-us/defender-xdr/media/microsoft-secure-score-history-metrics-trends/secure-score-history-flyout.png)](/en-us/defender-xdr/media/microsoft-secure-score-history-metrics-trends/secure-score-history-flyout.png#lightbox)

## Discover trends and set goals

In the **Metrics & trends** tab, there are several graphs and charts to give you more visibility into trends and set goals. You can set the date range for the whole page of visualizations. The visualizations include:

- **Your Secure Score zone** - Customized based on your organization's goals and definitions of good, okay, and bad score ranges.
- **Comparison trend** - How your organization's Secure Score compares to others' over time. This view can include lines representing the score average of organizations with similar seat count and a custom comparison view that you can set.
- **Score changes** - The number of points achieved, points regressed, and changes to your score in the specified date range.
- **Regression trend** - A timeline of points that have regressed because of configuration, user, or device changes.
- **Risk acceptance trend** - Timeline of recommended actions marked as "risk accepted."

### Compare your score to organizations like yours

There are two places to see how your score compares to organizations that are similar to yours.

#### Comparison bar chart

The comparison bar chart is available on the **Overview** tab. Hover over the chart to view the score and score opportunity.

[![An example of the bar graph of similar organization's scores in the Microsoft Defender portal](/en-us/defender-xdr/media/microsoft-secure-score-history-metrics-trends/secure-score-comparison-bar.png)](/en-us/defender-xdr/media/microsoft-secure-score-history-metrics-trends/secure-score-comparison-bar.png#lightbox)

The comparison data is anonymized so we don't know exactly which others tenants are in the mix.

![Bar graph of similar organization's scores.](/en-us/defender-xdr/media/microsoft-secure-score-history-metrics-trends/secure-score-comparison-screenshot.png)

#### Comparison trend

In the **Metrics & trends** tab, view how your organization's Secure Score compares to others' over time.

[![An example of a line graph of similar organization's scores over time in the Microsoft Defender portal](/en-us/defender-xdr/media/microsoft-secure-score-history-metrics-trends/secure-score-comparison-trend.png)](/en-us/defender-xdr/media/microsoft-secure-score-history-metrics-trends/secure-score-comparison-trend.png#lightbox)

## We want to hear from you

If you have any issues, let us know by posting in the [Defender XDR community](https://techcommunity.microsoft.com/category/microsoft-defender-xdr/discussions/microsoftthreatprotection). We're monitoring the community and will provide help.

## Related resources

- [Microsoft Secure Score overview](microsoft-secure-score)
- [Assess your security posture](microsoft-secure-score-improvement-actions)
- [What's coming](whats-new)
- [What's new](microsoft-secure-score-whats-new)

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).