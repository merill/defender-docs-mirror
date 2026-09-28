---
layout: Conceptual
title: 'Tutorial: Gather threat intelligence and perform infrastructure chaining in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/gathering-threat-intelligence-and-infrastructure-chaining
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to gather threat intelligence and chain together indicators of compromise using Microsoft Threat Intelligence in the Microsoft Defender portal. Walk through a historical investigation of the MyPillow Magecart breach.
ms.service: defender-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.custom:
- cx-ti
ms.topic: tutorial
ms.date: 2026-07-30T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 686f0f6f-a37c-999d-cd41-e0c9e6207921
document_version_independent_id: 686f0f6f-a37c-999d-cd41-e0c9e6207921
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/gathering-threat-intelligence-and-infrastructure-chaining.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: gathering-threat-intelligence-and-infrastructure-chaining
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/gathering-threat-intelligence-and-infrastructure-chaining.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 9a3eb140-517f-a57e-85fe-46cebf7185f7
---

# Tutorial: Gather threat intelligence and perform infrastructure chaining in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

This tutorial walks you through how to perform several types of indicator searches and gather threat and adversary intelligence using Microsoft Threat Intelligence in the Microsoft Defender portal.

## Prerequisites

- Access to the [Microsoft Defender portal](https://security.microsoft.com/). [Learn more about the Defender portal](/en-us/defender-xdr/microsoft-365-defender-portal)

## Disclaimer

Microsoft Threat Intelligence might include live, real-time observations and threat indicators, including malicious infrastructure and adversary-threat tooling. Any IP address and domain searches in the Defender portal are safe to search. Microsoft shares online resources (for example, IP addresses and domain names) that are considered real threats posing a clear and present danger. Use your best judgment and minimize unnecessary risk while interacting with malicious systems when performing this tutorial. Microsoft minimizes risks by defanging malicious IP addresses, hosts, and domains.

## Before you begin

As the disclaimer states previously, suspicious and malicious indicators are defanged for your safety. Remove any brackets from IP addresses, domains, and hosts when searching. Don't search these indicators directly in your browser.

## Perform indicator searches and gather threat and adversary intelligence

This tutorial walks you through how to perform infrastructure chaining with indicators of compromise (IOCs) related to a Magecart breach and gather threat and adversary intelligence along the way.

Infrastructure chaining uses the highly connected nature of the internet to expand one IOC into many based on overlapping details or shared characteristics. Building infrastructure chains lets threat hunters or incident responders profile an adversary's digital presence and quickly pivot across these sets of data to create context around an incident or investigation. Infrastructure chains also allow for more effective incident triaging, alerting, and actioning within an organization.

**Relevant personas:** Threat intelligence analyst, threat hunter, incident responder, security operations analyst

### Background on the Magecart breach

Microsoft has been profiling and following the activities of Magecart, a syndicate of cybercriminal groups behind hundreds of breaches of online retail platforms. Magecart injects scripts, which steal the sensitive data consumers enter into online payment forms, on e-commerce websites directly or through their compromised suppliers.

Back in October 2018, Magecart infiltrated MyPillow's online website, *mypillow[.]com*, to steal payment information by injecting a script into their web store. The script was hosted on a typosquatted domain *mypiltow[.]com*.

The MyPillow breach was a two-stage attack, with the first skimmer only active for a brief time before being identified as illicit and removed. However, the attackers still had access to MyPillow's network and on October 26, 2018, Microsoft observed that they registered a new domain, *livechatinc[.]org*.

Magecart actors typically register a domain that looks as similar as possible to the legitimate one. Thus, if an analyst looks at the JavaScript code, they might miss Magecart's injected script that's capturing the credit card payment information and pushing it to Magecart's own infrastructure. However, Microsoft's virtual users capture the document object model (DOM) and find all the dynamic links and changes made by the JavaScript from the crawls on the backend. We can detect that activity and pinpoint that fake domain that was hosting the injected script into the MyPillow web store.

### Gather Magecart breach threat intelligence

Perform the following steps in the **Intel explorer** page in the Defender portal to do infrastructure chaining on *mypillow[.]com*.

1. Access the [Defender portal](https://security.microsoft.com/) and complete the Microsoft authentication process. [Learn more about the Defender portal](/en-us/defender-xdr/microsoft-365-defender-portal)
2. Navigate to **Threat intelligence** &gt; **Intel explorer**.
3. Search *mypillow[.]com* on the **Intel explorer** search bar. You should see the article *Consumers May Lose Sleep Over These Two Magecart Breaches* associated with this domain.
4. Select the article. The following information should be available about this related campaign:

    - This article was published on March 20, 2019.
    - It provides insights as to how the Magecart threat actor group breached MyPillow in October 2018.
5. Select the **Public indicators** tab in the article. It should list the following IOCs:

    - *amerisleep.github[.]io*
    - *cmytuok[.]top*
    - *livechatinc[.]org*
    - *mypiltow[.]com*
6. Go back to the **Intel explorer** search bar, select **All** in the dropdown, and query *mypillow[.]com* again.
7. Select the **Host pairs** tab of the search results. Host pairs reveal connections between websites that traditional data sources, such as passive domain name system (pDNS) and WHOIS, wouldn't surface. They also let you see where your resources are being used and vice-versa.
8. Sort the host pairs by **First seen**, and filter by *script.src* as the **Cause**. Page over until you find host pair relationships that took place in October 2018. Notice that *mypillow[.]com* is pulling content from the typosquatted domain, *mypiltow[.]com* on October 3-5, 2018 through a script.
9. Select the **Resolutions** tab and pivot off the IP address that *mypiltow[.]com* resolved to in October 2018.

    Repeat this step for *mypillow[.]com*. You should notice the following differences between the two domains' IP addresses in October 2018:

    - The IP address *mypiltow[.]com* resolved to, 195.161.41[.]65, was hosted in Russia.
    - The two IP addresses used different autonomous system numbers (ASNs).
10. Select the **Summary** tab and scroll down to the **Articles** section. You should see the following published articles related to *mypiltow[.]com*:

    - *RiskIQ: Magecart Injected URLs and C2 Domains, June 3-14, 2022*
    - *RiskIQ: Magecart injected URLs and C2 Domains, May 20-27, 2022*
    - *Commodity Skimming & Magecart Trends in First Quarter of 2022*
    - *RiskIQ: Magecart Group 8 Activity in Early 2022*
    - *Magecart Group 8 Real Estate: Hosting Patterns Associated with the Skimming Group*
    - *Inter Skimming Kit Used in Homoglyph Attacks*
    - *Magecart Group 8 Blends into NutriBullet.com Adding To Their Growing List of Victims*

    Review each of these articles and take note of additional information—such as targets; tactics, techniques, and procedures (TTPs); and other IOCs—you can find about the Magecart threat actor group.
11. Select the **WHOIS** tab and compare the WHOIS information between *mypillow[.]com* and *mypiltow[.]com*. Take note of the following details:

    - The WHOIS record of *mypillow[.]com* from October 2011 indicates that My Pillow Inc. clearly owns the domain.
    - The WHOIS record of *mypiltow[.]com* from October 2018 indicates that the domain was registered in Hong Kong SAR and is privacy protected by Domain ID Shield Service CO.
    - The registrar of *mypiltow[.]com* is OnlineNIC, Inc.

    Given the address records and WHOIS details analyzed so far, an analyst should find it odd that a Chinese privacy service primarily guards a Russian IP address for a US-based company.
12. Navigate back to the **Intel explorer** search bar and search *livechatinc[.]org*. The article *Magecart Group 8 Blends into NutriBullet.com Adding To Their Growing List of Victims* should now appear in the search results.
13. Select the article. The following information should be available about this related campaign:

    - The article was published on March 18, 2020.
    - The article indicates that Nutribullet, Amerisleep, and ABS-CBN were also victims of the Magecart threat actor group.
14. Select the **Public indicators** tab. It should list the following IOCs:

    - **URLs:** hxxps://coffemokko[.]com/tr/, hxxps://freshdepor[.]com/tr/, hxxps://prodealscenter[.]c4m/tr/, hxxps://scriptoscript[.]com/tr/, hxxps://swappastore[.]com/tr/
    - **Domains:** 3lift[.]org, abtasty[.]net, adaptivecss[.]org, adorebeauty[.]org, all-about-sneakers[.]org, amerisleep.github[.]io, ar500arnor[.]com, authorizecdn[.]com, bannerbuzz[.]info, battery-force[.]org, batterynart[.]com, blackriverimaging[.]org, braincdn[.]org, btosports[.]net, cdnassels[.]com, cdnmage[.]com, chicksaddlery[.]net, childsplayclothing[.]org, christohperward[.]org, citywlnery[.]org, closetlondon[.]org, cmytuok[.]top, coffemokko[.]com, coffetea[.]org, configsysrc[.]info, dahlie[.]org, davidsfootwear[.]org, dobell[.]su, elegrina[.]com, energycoffe[.]org, energytea[.]org, etradesupply[.]org, exrpesso[.]org, foodandcot[.]com, freshchat[.]info, freshdepor[.]com, greatfurnituretradingco[.]org, info-js[.]link, jewsondirect[.]com, js-cloud[.]com, kandypens[.]net, kikvape[.]org, labbe[.]biz, lamoodbighats[.]net, link js[.]link, livechatinc[.]org, londontea[.]net, mage-checkout[.]org, magejavascripts[.]com, magescripts[.]pw, magesecuritys[.]com, majsurplus[.]com, map-js[.]link, mcloudjs[.]com, mechat[.]info, melbounestorm[.]com, misshaus[.]org, mylrendyphone[.]com, mypiltow[.]com, nililotan[.]org, oakandfort[.]org, ottocap[.]org, parks[.]su, paypaypay[.]org, pmtonline[.]su, prodealscenter[.]com, replacemyremote[.]org, sagecdn[.]org, scriptoscript[.]com, security-payment[.]su, shop-rnib[.]org, slickjs[.]org, slickmin[.]com, smart-js[.]link, swappastore[.]com, teacoffe[.]net, top5value[.]com, track-js[.]link, ukcoffe[.]com, verywellfitnesse[.]com, walletgear[.]org, webanalyzer[.]net, zapaljs[.]com, zoplm[.]com
15. Navigate back to the **Intel explorer** search bar and search *mypillow[.]com*. Then, go to the **Host pairs** tab, sort the host pairs by **First seen**, and look for host pair relationships that occurred in October 2018.

    Notice how *www.mypillow[.]com* was first observed reaching out to *secure.livechatinc[.]org* on October 26, 2018, because a script GET request was observed from *www.mypillow[.]com* to *secure.livechatinc[.]org*. That relationship lasted until November 19, 2018.

    In addition, *secure.livechatinc[.]org* reached out to *www.mypillow[.]com* to access the latter's server (*xmlhttprequest*).
16. Review *mypillow[.]com*'s host pair relationships further. Notice how *mypillow[.]com* has host pair relationships with the following domains, which is similar to the domain name *secure.livechatinc[.]org*:

    - *cdn.livechatinc[.]com*
    - *secure.livechatinc[.]com*
    - *api.livechatinc[.]com*

    The relationship causes include:

    - script.src
    - iframe.src
    - unknown
    - topLevelRedirect
    - img.src
    - xmlhttprequest

    Livechat is a live support chat service that online retailers can add to their websites as a partner resource. Several e-commerce platforms, including MyPillow, use it. This fake domain is interesting because the Livechat's official site is actually *livechatinc[.]com*. Therefore, in this case, the threat actor used a top-level-domain typosquat to hide the fact they placed a second skimmer on the MyPillow website.
17. Go back and find a host pair relationship with *secure.livechatinc[.]org* and pivot off that hostname. The **Resolutions** tab should indicate that this host resolved to 212.109.222[.]230 in October 2018.

    Notice that this IP address is also hosted in Russia and the ASN organization is JSC IOT.
18. Navigate back to the **Intel explorer** search bar and search *secure.livechatinc[.]org*. Then, go to the **WHOIS** tab and select the record from December 25, 2018.

    The registrar used for this record is OnlineNIC Inc., which is the same one used to register *mypiltow[.]com* during the same campaign. Based on the record from December 25, 2018, notice that the domain also used the same Chinese privacy guarding service, Domain ID Shield Service, as *mypiltow[.]com*.

    The December record used the following name servers, which were the same one used in the October 1, 2018 record for *mypiltow[.]com*.

    - ns1.jino.ru
    - ns2.jino.ru
    - ns3.jino.ru
    - ns4.jino.ru
19. Select the **Host pairs** tab. You should see the following host pair relationships from October to November 2018:

    - *secure.livechatinc[.]org* redirected users to *secure.livechatinc.com* on November 19, 2022. This redirection is more than likely an obfuscation technique to evade detection.
    - *www.mypillow[.]com* was pulling a script hosted on *secure.livechatinc[.]org* (the fake LiveChat site) from October 26, 2018 through November 19, 2022. During this timeframe, *www.mypillow[.]com*'s user purchases were potentially compromised.
    - *secure.livechatinc[.]org* was requesting data (*xmlhttprequest*) from the server *www.mypillow[.]com*, which hosts the real MyPillow website, from October 27 to 29, 2018.

## Clean up resources

There are no resources to clean up in this section.