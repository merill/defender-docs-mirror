---
layout: Conceptual
title: Use server-side filtering with export assessment APIs (preview) - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/export-assessment-server-side-filtering
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use the $filter query parameter to narrow Microsoft Defender Vulnerability Management JSON export assessments.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: reference
ms.subservice: reference
ms.custom: api
ms.date: 2026-11-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 8cffae53-3cae-f3c0-b6bc-8ac272fdbf82
document_version_independent_id: 8cffae53-3cae-f3c0-b6bc-8ac272fdbf82
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/export-assessment-server-side-filtering.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/export-assessment-server-side-filtering
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/export-assessment-server-side-filtering.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8b896464-3b7d-4e1f-84b0-9bb45aeb5f64
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1d2d671-9549-46e8-918c-24349120dbf5
platformId: 81619cd5-2fa2-241c-75fd-c4ceb97b48ed
---

# Use server-side filtering with export assessment APIs (preview) - Microsoft Defender for Endpoint | Microsoft Learn

Important

Server-side filtering with export assessment APIs is in preview. Some information relates to a prerelease product that might be substantially modified before it's released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Add the `$filter` query parameter to a supported JSON export method to narrow the eligible export records before they're returned. This reduces the data that you transfer and process. Existing permissions and device-group access still apply.

## Licensing and permissions

- Your license must cover the assessment that you export. Microsoft Defender for Endpoint Plan 2 includes core vulnerability management capabilities; some assessments require additional capabilities. Defender for Endpoint Plan 1 alone isn't sufficient for these vulnerability management capabilities. Plan 1 customers can use the appropriate Defender Vulnerability Management standalone subscription. See [Vulnerability Management prerequisites and licensing](/en-us/defender-vulnerability-management/tvm-prerequisites).
- Use the permissions and rate limits documented for each method. Filtering doesn't grant access to additional data.

Important

Use authorization, not `$filter`, as your access-control boundary. Filtering doesn't grant access to additional records.

## Supported methods

The following JSON response methods support server-side filtering, subject to the licensing and permission requirements above.

| Method | HTTP request |
| --- | --- |
| [Export software vulnerabilities assessment](get-assessment-software-vulnerabilities) | `GET /api/machines/SoftwareVulnerabilitiesByMachine` |
| [Delta export software vulnerabilities assessment](get-assessment-software-vulnerabilities) | `GET /api/machines/SoftwareVulnerabilityChangesByMachine` |
| [Export software inventory assessment](get-assessment-software-inventory) | `GET /api/machines/SoftwareInventoryByMachine` |
| [Export secure configuration assessment](get-assessment-secure-config) | `GET /api/machines/SecureConfigurationsAssessmentByMachine` |
| [Export security baselines assessment](export-security-baseline-assessment) | `GET /api/machines/BaselineComplianceAssessmentByMachine` |
| [Export non-product-code software inventory](get-assessment-non-cpe-software-inventory) | `GET /api/machines/SoftwareInventoryNoProductCodeByMachine` |
| [Export hardware and firmware assessment](export-firmware-hardware-assessment) | `GET /api/machines/HardwareFirmwareInventoryByMachine` |
| [Export browser extensions assessment](get-assessment-browser-extensions) | `GET /api/machines/BrowserExtensionsInventoryByMachine` |
| [Export certificate assessment](export-certificate-inventory-assessment) | `GET /api/machines/CertificateAssessmentByMachine` |

Server-side filtering is supported for JSON-response APIs only.

**File-export APIs are not supported.**

## Server-side filtering compared with client-side processing

Server-side filtering returns only the export records that match your conditions. It doesn't sort, group, join, count, aggregate, or add properties. Perform those operations in your application after retrieving the records.

| Task | Server-side row filtering (`$filter`) | Client-side processing |
| --- | --- | --- |
| Remove records that don't match your conditions | Yes | Yes, after retrieval |
| Reduce the records transferred in a JSON export | Yes | No |
| Sort records | No | Yes |
| Group, count, or aggregate records | No | Yes |
| Join records with other data | No | Yes |
| Filter rows inside downloaded export files | No | Yes |

## Syntax

```http
GET https://api.security.microsoft.com/api/machines/SoftwareVulnerabilitiesByMachine?$filter=osPlatform eq 'Windows11' and cvssScore ge 7
```

Each comparison has the form `<property> <operator> <constant>`. Combine comparisons with `and` or `or`, and use parentheses to control grouping. Write operators in lowercase.

| Operator | Meaning | Comparison categories |
| --- | --- | --- |
| `eq`, `ne` | Equal to, not equal to | String, number, Boolean, date, null |
| `gt`, `ge`, `lt`, `le` | Greater than, greater than or equal to, less than, less than or equal to | Number, date, or string ordering |
| `in` | Select device groups | Only the special `rbacGroups` expression |

String ordering is ordinal and case-insensitive, not numeric or semantic-version ordering. For example, don't use a string ordering comparison to determine whether a software version is newer. Use `eq` and `ne` for Boolean values; don't rely on textual Boolean ordering.

| Value | Recommended format | Example |
| --- | --- | --- |
| String | Single quotes | `softwareName eq 'chrome'` |
| Number | An unquoted finite number | `cvssScore ge 7` |
| Boolean | Unquoted `true` or `false` | `securityUpdateAvailable eq true` |
| Date | A quoted ISO-8601 UTC timestamp; a quoted date-only value is also accepted | `lastSeenTimestamp ge '2026-10-01T00:00:00Z'` |
| Null | Unquoted `null` | `lastSeenTimestamp ne null` |

- Property names and ordinary string comparisons aren't case-sensitive.
- Use actual response values, such as `Windows11` for `osPlatform`.
- Escape a single quote inside a string by doubling it, for example `'O''Brien'`.
- To match several values of an ordinary property, use `or`, such as `(osPlatform eq 'Windows11' or osPlatform eq 'Windows10')`.
- Compare a property with a fixed value, such as `cvssScore ge 7`. You can't compare two properties, such as `firstSeenTimestamp lt lastSeenTimestamp`.
- You can't use functions such as `contains(softwareName,'chrome')` or `startswith(softwareName,'ch')`. Use supported comparisons such as `softwareName eq 'chrome'` instead.
- You can't use `not` to negate a condition or `any`/`all` to search items in a list.
- URL-encode the filter expression when sending the request. Examples in this article are shown without encoding for readability.
- Use valid numeric and date literals. Not every mistyped property or value is rejected with `400 Bad Request`.

## Query parameters and pagination

| Parameter | Scope and guidance |
| --- | --- |
| `pageSize` | Available on the JSON methods listed above. The default is 50,000; the maximum is 200,000. Use it for paged retrieval. A selective filter can produce fewer records than the requested page size. |
| `$top` | Requests a limited response. Prefer `pageSize` and continuation links when you need a complete export; don't use `$top` as a substitute for full pagination. See the individual method's reference for its public paging contract. |
| `sinceTime` | Used only by the delta vulnerability method. The initial delta request requires a UTC timestamp within the last 14 days. |
| `$skiptoken` | An opaque continuation cursor supplied by the service. Prefer following the returned `@odata.nextLink` rather than constructing one yourself. |

For a complete paged JSON export:

1. Send the initial request with `pageSize` and your filter.
2. If `@odata.nextLink` is present, follow that URL without changing the selection criteria.
3. Continue until `@odata.nextLink` is absent.

The returned `@odata.nextLink` includes the query parameters needed to continue the export, including your filter and applicable `sinceTime`. Follow that URL unchanged rather than reconstructing it.

## Timeouts and partial pages

### Server-side scan limit

The service uses a **100-second search budget** to find matching records for each request. It can return the matches found so far with an `@odata.nextLink` if more data remains. Follow that link to continue retrieving results.

The total request can take longer than 100 seconds. Don't assume that every request completes within 100 seconds or copy that number directly into your client's timeout setting. Allow additional time to receive the complete response when configuring your client's timeout.

A complete `200 OK` JSON response can contain fewer records than `pageSize`, or an empty `value` array, while still including `@odata.nextLink`. That is a successful page, not a failed request.

| What you receive | What to do |
| --- | --- |
| Complete successful JSON with `@odata.nextLink`, including an empty page | Process the completed page and follow the next link. Don't restart the same page merely because it is short or empty. |
| Complete successful JSON without `@odata.nextLink` | There is no further page for this request. A result requested with `$top` must not be assumed to be a full export. |
| A request timeout, disconnect, or incomplete response body | Treat the page as unsuccessful. Don't advance the saved continuation position from a partial response. |

### If a request actually times out

- For a transient failure, retry the **same page URL** that failed, with the same filter, applicable `sinceTime`, and continuation token. Don't skip ahead or restart the export from the beginning unless that is an intentional recovery decision.
- Use bounded retries with backoff and honor `Retry-After` when it is provided. Follow the method's rate limits. Don't repeatedly retry validation or permission errors as though they were timeouts.
- Only advance your checkpoint after receiving and validating the complete page. If records can be processed before a page finishes, use rollback or duplicate-safe processing because a retry can replay them.
- Allow enough time to receive the complete response, within your application's timeout limits. A retry can return different data if the assessment has changed.

### Reduce repeated long-running requests

Device-group selection with `rbacGroups in (...)` limits which groups are included in the request. It is separate from filtering individual records by properties such as `cvssScore`. Selecting only the groups you need can reduce the data searched.

A smaller `pageSize` can reduce response size, but it doesn't necessarily make a filtered request faster. Follow continuation links rather than repeatedly requesting the first page.

## Filter by device group

Use `rbacGroups in ('Group A','Group B')` to select the device groups to include in the request. This selects groups, rather than comparing a property on each record. Combine it with record conditions through `and`, for example `rbacGroups in ('Group A') and cvssScore ge 7`.

Without `rbacGroups`, the request isn't narrowed to a requested group list; existing authorization still determines the available groups. Supplying a group name doesn't grant access to it.

- The clause is optional. Use at most one `rbacGroups` clause, and combine all requested names in its `in` list.
- Join the clause through `and`. It must not appear beneath any `or` expression, including an `or` outside a parenthesized group.
- Putting `rbacGroups` first is recommended for readability, but isn't required.
- Group-name matching is case-insensitive. Normal field-name casing and clause spacing are flexible.
- `rbacGroupName` and `rbacGroupId` aren't supported as per-row filter properties.

The examples below assume that the request otherwise passes authentication and authorization.

| Filter | Result |
| --- | --- |
| `rbacGroups in ('Group A','Group B') and (osPlatform eq 'Windows11' or osPlatform eq 'Windows10')` | Valid |
| `osPlatform eq 'Linux' and rbacGroups in ('Group A')` | Valid |
| `rbacGroupName eq 'Group A'` | `400 Bad Request` |
| `rbacGroupId eq 1` | `400 Bad Request` |
| `rbacGroups in ('Group A') or osPlatform eq 'Linux'` | `400 Bad Request` |
| `(rbacGroups in ('Group A') and osPlatform eq 'Linux') or cvssScore ge 7` | `400 Bad Request` |
| `rbacGroups in ('Group A') and rbacGroups in ('Group B')` | `400 Bad Request`. Combine names into `rbacGroups in ('Group A','Group B')`. |

## Filter by CVE publication date

Use `cvePublishedDate` to filter full and delta vulnerability exports by the CVE's publication date.

This property is available for filtering only and isn't included in the response. It represents when the CVE was published, not when the vulnerability was first seen on a device or when a delta event occurred.

```http
GET https://api.security.microsoft.com/api/machines/SoftwareVulnerabilitiesByMachine?$filter=cvePublishedDate ge '2026-10-01T00:00:00Z' and cvssScore ge 7
```

Use quoted ISO-8601 timestamps, preferably UTC with `Z`. Timestamps that represent the same moment compare equally, even if their time-zone offsets differ.

An unavailable publication date doesn't match a date-range condition such as `cvePublishedDate ge '2026-10-01'`. Use `cvePublishedDate eq null` to select records without an available publication date.

`cvePublishedDate` filtering is supported only for full and delta vulnerability exports.

## Missing values, unknown names, and complex properties

Use the actual property names from the export records. Filtering isn't restricted to the names in the tables below. An unknown or misspelled name is treated as a missing property and doesn't necessarily return `400 Bad Request`. Check property names carefully to avoid empty or unexpectedly broad results.

For a missing or null value:

| Comparison | Result of that comparison |
| --- | --- |
| `eq` a non-null constant | `false` |
| `ne` a non-null constant | `true` |
| `eq null` | `true` |
| `ne null` | `false` |
| `gt`, `ge`, `lt`, or `le` | `false` |

These results don't bypass other conditions or authorization.

**Filtering doesn't look inside arrays (lists) or objects.** For example, you can filter by `softwareName eq 'chrome'`, but you can't filter a record by whether its `diskPaths` list contains a particular file path.

**You can't filter individual items or nested fields in these properties:**

- Vulnerabilities and software inventory: `diskPaths` and `registryPaths`
- Software inventory: `softwareTags`
- Secure configurations: `context`
- Security baselines: `recommendedValue`, `currentValue`, `source`, and `rawValue`
- Browser extensions: `permissions`

Arrays and objects are treated as null in scalar comparisons. For example, `diskPaths eq null` does not tell you whether the list is empty.

Some properties store JSON-like text as a single string, such as hardware/firmware `additionalFields` and certificate `issuedTo`, `issuedBy`, `keyUsage`, and `extendedKeyUsage`. You can compare the whole string, but you can't filter a nested value within it.

## Filterable properties by method

**For a supported JSON export, you can filter on the top-level scalar properties of its returned records—not just the names listed in these tables.**

The exceptions and qualifications are:

- Array elements and object children aren't supported by the scalar row filter.
- For device groups, use `rbacGroups in (...)`, not per-row comparisons on `rbacGroupName` or `rbacGroupId`.

The tables list filterable properties and their comparison categories. Values can be missing or null, and filtering doesn't change which properties are returned. Dates can be represented as strings in the response. Full and delta vulnerability exports also support `cvePublishedDate` as a filter-only property.

`rbacGroups` is separate group scoping and isn't counted or repeated as an ordinary row property.

### Software vulnerabilities (JSON response)

| Comparison category | Properties |
| --- | --- |
| String | `id`, `deviceId`, `deviceName`, `osPlatform`, `osVersion`, `osArchitecture`, `softwareVendor`, `softwareName`, `softwareVersion`, `cveId`, `vulnerabilitySeverityLevel`, `exploitabilityLevel`, `recommendationReference`, `recommendedSecurityUpdate`, `recommendedSecurityUpdateId`, `recommendedSecurityUpdateUrl`, `cveBatchUrl`, `cveBatchTitle`, `cveMitigationStatus` |
| Number | `cvssScore` |
| Boolean | `isOnboarded`, `securityUpdateAvailable` |
| Date | `firstSeenTimestamp`, `lastSeenTimestamp` |
| Date (filter only) | `cvePublishedDate` |

For publication-date filtering and missing-date behavior, see Filter by CVE publication date.

### Delta export software vulnerabilities (JSON response)

To select delta events by status, use `New`, `Updated`, or `Fixed`, for example `status eq 'New'`.

| Comparison category | Properties |
| --- | --- |
| String | `id`, `deviceId`, `deviceName`, `osPlatform`, `osVersion`, `osArchitecture`, `softwareVendor`, `softwareName`, `softwareVersion`, `cveId`, `vulnerabilitySeverityLevel`, `exploitabilityLevel`, `recommendationReference`, `recommendedSecurityUpdate`, `recommendedSecurityUpdateId`, `recommendedSecurityUpdateUrl`, `status` |
| Number | `cvssScore` |
| Boolean | `isOnboarded`, `securityUpdateAvailable` |
| Date | `eventTimestamp`, `firstSeenTimestamp`, `lastSeenTimestamp` |
| Date (filter only) | `cvePublishedDate` |

### Software inventory (JSON response)

| Comparison category | Properties |
| --- | --- |
| String | `deviceId`, `deviceName`, `osPlatform`, `softwareVendor`, `softwareName`, `softwareVersion`, `endOfSupportStatus` |
| Number | `numberOfWeaknesses` |
| Boolean | `isOnboarded` |
| Date | `endOfSupportDate`, `softwareFirstSeenTimestamp`, `softwareLastSeenTimestamp` |

### Secure configuration (JSON response)

| Comparison category | Properties |
| --- | --- |
| String | `configurationCategory`, `configurationId`, `configurationName`, `configurationSubcategory`, `deviceId`, `deviceName`, `osPlatform`, `osVersion`, `recommendationReference` |
| Number | `configurationImpact` |
| Boolean | `isApplicable`, `isCompliant`, `isExpectedUserImpact` |
| Date | `timestamp` |

### Security baselines (JSON response)

| Comparison category | Properties |
| --- | --- |
| String | `id`, `configurationId`, `deviceId`, `deviceName`, `osPlatform`, `osVersion`, `profileId`, `complianceEvaluationDetails`, `assessmentMethod`, `complianceCalculationTimeOffset`, `dataCollectionTimeOffset` |
| Boolean | `isApplicable`, `isCompliant`, `isExempt` |

To select noncompliant baseline assessments, use `isCompliant eq false`. The quoted form, `isCompliant eq 'false'`, is also accepted.

Compare `complianceCalculationTimeOffset` and `dataCollectionTimeOffset` as text, not as dates.

Use `profileId` to filter by a baseline profile.

### Non-product-code software inventory (JSON response)

| Comparison category | Properties |
| --- | --- |
| String | `deviceId`, `deviceName`, `osPlatform`, `softwareVendor`, `softwareName`, `softwareVersion`, `registryPath` |
| Date | `softwareLastSeenTimestamp` |

`registryPath` is a scalar string on this method, unlike the `registryPaths` arrays on vulnerability and software-inventory methods.

### Hardware and firmware assessment (JSON response)

| Comparison category | Properties |
| --- | --- |
| String | `deviceId`, `deviceName`, `componentType`, `manufacturer`, `componentName`, `componentVersion`, `additionalFields` |

### Browser extensions assessment (JSON response)

| Comparison category | Properties |
| --- | --- |
| String | `deviceId`, `deviceName`, `browserName`, `extensionId`, `extensionName`, `extensionDescription`, `extensionVersion`, `extensionRisk`, `extensionVendor` |
| Boolean | `isActivated` |
| Date | `installationTime` |

### Certificate assessment (JSON response)

| Comparison category | Properties |
| --- | --- |
| String | `deviceId`, `deviceName`, `thumbprint`, `path`, `signatureAlgorithm`, `friendlyName`, `subjectType`, `serialNumber`, `issuedTo`, `issuedBy`, `keyUsage`, `extendedKeyUsage` |
| Number | `keySize` |
| Date | `expirationDate`, `issueDate` |

## Examples

The filter expressions are shown unencoded for readability. Dates are illustrative. Whenever you run a delta request, replace `sinceTime` with a UTC timestamp within the last 14 days; an old example date eventually falls outside that window.

High-severity vulnerabilities with a security update, in one device group:

```http
GET https://api.security.microsoft.com/api/machines/SoftwareVulnerabilitiesByMachine?pageSize=50000&$filter=rbacGroups in ('Finance') and cvssScore ge 7 and securityUpdateAvailable eq true
```

New critical vulnerability events in a recent delta window:

```http
GET https://api.security.microsoft.com/api/machines/SoftwareVulnerabilityChangesByMachine?sinceTime=2026-10-19T00:00:00Z&pageSize=50000&$filter=status eq 'New' and vulnerabilitySeverityLevel eq 'Critical'
```

This is a selected event stream, not a complete synchronization feed.

Software versions that reached end of support:

```http
GET https://api.security.microsoft.com/api/machines/SoftwareInventoryByMachine?$filter=endOfSupportStatus eq 'EOS Version'
```

Applicable, noncompliant configurations with an impact of at least 7:

```http
GET https://api.security.microsoft.com/api/machines/SecureConfigurationsAssessmentByMachine?$filter=rbacGroups in ('Group A') and isApplicable eq true and isCompliant eq false and configurationImpact ge 7
```

Applicable, noncompliant baseline configurations on Windows 11:

```http
GET https://api.security.microsoft.com/api/machines/BaselineComplianceAssessmentByMachine?$filter=rbacGroups in ('Group A') and osPlatform eq 'Windows11' and isApplicable eq true and isCompliant eq false
```

Active browser extensions with a high risk classification:

```http
GET https://api.security.microsoft.com/api/machines/BrowserExtensionsInventoryByMachine?$filter=isActivated eq true and extensionRisk eq 'High'
```

Certificates expiring before an illustrative cutoff:

```http
GET https://api.security.microsoft.com/api/machines/CertificateAssessmentByMachine?$filter=expirationDate lt '2026-11-01T00:00:00Z'
```

## Delta integrations and reconciliation

A filtered delta can omit updates to records that you previously downloaded if those records no longer match the filter.

For example, you download a record with score 8 using `cvssScore ge 7`. If a later delta update has score 5, the filter excludes that update. Your local copy can still show the old score of 8 because you didn't receive the change.

A filter such as `status eq 'New'` also excludes updates and fixes.

If you use exports to keep a local copy up to date:

- Retrieve a full export and its delta updates without row-property filters, then apply your reporting filter locally. Keep the same authorized device-group scope.
- Refresh from a full export periodically and when your filter criteria change. See the [delta reference](get-assessment-software-vulnerabilities) for which changes the API reports.

## Limitations

- Row filtering is supported for the JSON-response APIs listed above, not file-export APIs.
- Filter top-level scalar properties or the filter-only `cvePublishedDate` property. You can't search items in arrays or fields inside objects.
- Compare each property with a fixed value, not another property. Expressions such as `contains(softwareName,'chrome')` and `firstSeenTimestamp lt lastSeenTimestamp` aren't supported. See Syntax for supported comparisons.
- Filtering isn't restricted to the field tables. Returned top-level scalar properties can be filtered, except `rbacGroupName` and `rbacGroupId`; use `rbacGroups` for device-group selection. Unknown or unavailable properties are treated as missing/null rather than necessarily returning an error.
- String ordering is lexical, not numeric or semantic-version ordering.
- Filtering doesn't sort, group, join, count, aggregate, or add response properties.
- Follow continuation links even after an empty page. Don't change filter criteria between pages. For partial pages and failed requests, see Timeouts and partial pages.
- A delta filter can hide updates to records that no longer match, leaving outdated records in your local copy. See the example in Delta integrations and reconciliation.