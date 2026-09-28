---
layout: Conceptual
title: Troubleshoot configuration issues for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-support-configuration
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot configuration issues in Microsoft Defender for Endpoint on macOS.
ms.service: defender-endpoint
author: paulinbar
ms.author: painbar
ms.reviewer: joshbregman
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.topic: troubleshooting-general
ms.subservice: macos
ms.date: 2025-04-16T00:00:00.0000000Z
locale: en-us
document_id: 7c558323-a8dc-134b-5738-0d22d9dcf171
document_version_independent_id: 7c558323-a8dc-134b-5738-0d22d9dcf171
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-support-configuration.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-support-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-support-configuration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 52934695-1ba2-abd4-d58a-1c5c633d169c
---

# Troubleshoot configuration issues for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn

## Configuration isn't applied as expected

You configured Microsoft Defender with settings that you need, and you don't see some (or all) of them applied. How to troubleshoot it?

### Sources of configuration

Microsoft Defender collects configuration from multiple sources.

In almost all cases you can change configuration dynamically, and it will be applied immediately, with no restart required.

Different sources have different priorities. When the same setting comes from more than one source, Microsoft Defender will merge values from different sources. In most cases it means that the value with the higher priority prevails, and sources from lower priorities are ignored. In some cases (for example, [Antivirus Exclusions](mac-preferences#exclusion-merge-policy)). Refer to configuration documentation for details.

Configuration sources in the order of priority ("1" is the highest priority):

1. MDE Attach, Defender configured in Intune portal
2. [MDM configuration profile](mac-jamfpro-policies), configured using your MDM software
3. [Local configuration](mac-resources#supported-output-types), that you made using `mdatp config ...` command as local administrator, or through Microsoft Defender's application
4. Default setting that is used when you provided no explicit setting

### MDE Attach and MDM Configuration profile

Caution

MDE Attach and MDM Configuration Profile are mutually excluded. If you provide *some* configuration for both, then only MDE Attach settings are used, and *all* MDM settings are ignored! Don't use them together.

Use `mdatp health --field managed_by` to find out if you use MDE Attach.

1. "MDE" indicates MDE Attach. Any configuration specified with an MDM configuration profile is ignored.
2. "MEM" indicates MDM Configuration Profile, or only local configuration

You can run `mdatp health` to get the configuration that Microsoft Defender is currently used. If you see "[managed]" next to a value, then it's currently configured through an MDM Configuration Profile. If there's no "[managed]", then it's configured locally or via MDE Attach.

### MDE Attach and MDM configurations troubleshooting

Check the following files:

1. `/Library/Preferences/com.microsoft.mdeattach.plist` - Microsoft Defender reads this file for settings delivered by MDE Attach. If you expect some setting and you don't see it configured, then check that it's there
2. `/Library/Managed Preferences/com.microsoft.wdav.plist` and `/Library/Managed Preferences/com.microsoft.wdav.ext.plist` - Microsoft Defender reads these files for settings delivered by MDM.

The file paths and names must be exactly like described! If you see a similar but a bit different file path, then it means that Microsoft Defender ignores it.

If you expect some MDM settings and don't see those files, it means that MDM hasn't delivered configuration profiles to your machine at all. To troubleshoot profiles delivery, consult your MDM software (JAMF, Intune, etc.) resources.

If you expect some settings and you see those files, then check their content:

```
> plutil -p '/Library/Managed Preferences/com.microsoft.wdav.plist
{
  "antivirusEngine" => {
    "enforcementLevel" => "real_time"
  }
}
```

Those settings must match those settings that you configured. Their names, level of indirection, type must be exactly as [documented](mac-preferences).

For example, if `plist` tells you that "antivirusEngine" is inside a different group, then you can be confident that Microsoft Defender *ignores* "enforcementLevel" setting altogether:

```
# Bad configuration!
> plutil -p '/Library/Managed Preferences/com.microsoft.wdav.plist
{
  "Forced" => {
    "mcx_preference_settings" => {
      "antivirusEngine" => {
        "enforcementLevel" => "real_time"
      }
    }
  }
}
```

### MDM Configuration - where does it come from?

macOS updates /Library/Managed Preferences/ files based on Profiles deployed over MDM.

If you don't see an expected managed preferences file, or its content is different from what you expect, then open  =&gt; System Settings =&gt; Profiles.

You can see all profiles deployed over MDM under "Device (Managed)." Find a profile that you configured in MDM for Microsoft Defender configuration. You can open it and inspect its content. It must match what is in /Library/Managed Preferences/com.microsoft.wdav.plist and what you configured in MDM.

If you don't see any managed profile for com.microsoft.wdav, then MDM didn't deliver it. Consult your MDM software documentation for troubleshooting, there can be multiple reasons why it happened, troubleshooting of MDM is out of scope for Microsoft Defender documentation.

If you see *more than one* configuration profile for the same com.microsoft.wdav, then it can be the reason of not expected configuration of Microsoft Defender. macOS performs some merging of those profiles into a single .plist, but it can properly merge only the top level of configuration. That is, you can't spread different "antivirusEngine" settings across two com.microsoft.wdav configuration profiles, MDM uses only one of them randomly, and ignore the rest. You can use extra com.microsoft.wdav.ext profile if you need to put settings to two profiles (again, there must be at most one configuration profile with com.microsoft.wdav.ext as well).

In other words, avoid having more than one configuration profile for the same identifier.

### MDE Attach Configuration - where does it come from?

It isn't delivered over MDM. Consult MDE Attach documentation for how to troubleshoot it.