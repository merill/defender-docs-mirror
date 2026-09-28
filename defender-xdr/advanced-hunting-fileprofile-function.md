---
layout: Conceptual
title: FileProfile() function in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-fileprofile-function
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use the FileProfile() to enrich information about files in your advanced hunting query results.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom:
- cx-ti
- cx-ah
ms.topic: reference
ms.date: 2025-08-05T00:00:00.0000000Z
locale: en-us
document_id: d6427e60-810a-00db-b798-52a0d977f343
document_version_independent_id: d6427e60-810a-00db-b798-52a0d977f343
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-fileprofile-function.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-fileprofile-function
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-fileprofile-function.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: d8000c0f-9dba-0128-d355-4bf3532cd0ba
---

# FileProfile() function in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

The `FileProfile()` function is an enrichment function in [advanced hunting](advanced-hunting-overview) that adds the following data to files found by the query.

| Column | Data type | Description |
| --- | --- | --- |
| `SHA1` | `string` | SHA-1 of the file that the recorded action was applied to |
| `SHA256` | `string` | SHA-256 of the file that the recorded action was applied to |
| `MD5` | `string` | MD5 hash of the file that the recorded action was applied to |
| `FileSize` | `int` | Size of the file in bytes |
| `GlobalPrevalence` | `int` | Number of instances of the entity observed by Microsoft globally |
| `GlobalFirstSeen` | `datetime` | Date and time when the entity was first observed by Microsoft globally |
| `GlobalLastSeen` | `datetime` | Date and time when the entity was last observed by Microsoft globally |
| `Signer` | `string` | Information about the signer of the file |
| `Issuer` | `string` | Information about the issuing certificate authority (CA) |
| `SignerHash` | `string` | Unique hash value identifying the signer |
| `IsCertificateValid` | `boolean` | Whether the certificate used to sign the file is valid |
| `IsRootSignerMicrosoft` | `boolean` | Indicates whether the signer of the root certificate is Microsoft and the file is built in to Windows OS |
| `SignatureState` | `string` | State of the file signature: SignedValid - the file is signed with a valid signature, SignedInvalid - the file is signed but the certificate is invalid, Unsigned - the file isn't signed, Unknown - information about the file can't be retrieved |
| `IsExecutable` | `boolean` | Whether the file is a Portable Executable (PE) file |
| `ThreatName` | `string` | Detection name for any malware or other threats found |
| `Publisher` | `string` | Name of the organization that published the file |
| `SoftwareName` | `string` | Name of the software product |
| `ProfileAvailability` | `string` | Indicates the availability status of the profile data for the file: Available - profile was successfully queried and file data returned, Missing - profile was successfully queried but no file info was found, Error - error in querying the file info or maximum allotted time was exceeded before query could be completed, or an empty value - if file ID is invalid or the maximum number of files was reachedIf this column's value is Missing or is empty, the value of the `GlobalPrevalance` column would be null. |

## Syntax

```kusto
invoke FileProfile(x,y)
```

## Arguments

- **x**—file ID column to use: `SHA1`, `SHA256`, `InitiatingProcessSHA1`, or `InitiatingProcessSHA256`; function uses `SHA1` if unspecified
- **y**—limit to the number of records to enrich, 1-1000; function uses 100 if unspecified

Tip

Enrichment functions will show supplemental information only when they're available. Availability of information is varied and depends on numerous factors. Make sure to consider this when using FileProfile() in your queries or in creating custom detections. For best results, we recommend using the FileProfile() function with SHA1.

## Examples

### Project only the SHA1 column and enrich it

```kusto
DeviceFileEvents
| where isnotempty(SHA1) and Timestamp > ago(1d)
| take 10
| project SHA1
| invoke FileProfile()
```

### Enrich the first 500 records and list low-prevalence files

```kusto
DeviceFileEvents
| where ActionType == "FileCreated" and Timestamp > ago(1d)
| project CreatedOn = Timestamp, FileName, FolderPath, SHA1
| invoke FileProfile("SHA1", 500) 
| where GlobalPrevalence < 15
```