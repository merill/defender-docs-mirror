---
layout: Conceptual
title: Download assessment export files - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/download-assessment-export-files
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Retrieve assessment export URLs, check asynchronous blob copy status, and download assessment files from Microsoft Defender for Endpoint APIs.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: how-to
ms.subservice: reference
ms.custom: api
ms.date: 2026-11-19T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d85d2fc6-e316-7886-0bbb-af2eb75f9bc9
document_version_independent_id: d85d2fc6-e316-7886-0bbb-af2eb75f9bc9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/download-assessment-export-files.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/download-assessment-export-files
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/download-assessment-export-files.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/ea957f26-244e-4bd1-9b19-105f0a0a73d6
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/85dd85bb-c2e5-412e-96b2-f2765a3fe51c
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: b8e3dd71-b001-a9cb-b71c-e89dbbc4e47e
---

# Download assessment export files - Microsoft Defender for Endpoint | Microsoft Learn

Use the assessment export APIs to retrieve download URLs, then download the files from Azure Blob Storage. Each file contains part of the assessment snapshot. Download and process every file returned for that snapshot.

When an export file is prepared by an asynchronous Azure Blob Storage copy, the download URL can be available before the copy finishes. Check the destination blob's copy status before downloading it. You don't need to start a copy operation yourself.

## Before you begin

Use the licensing requirements, permissions, parameters, and rate limits documented for the assessment method you call. Checking blob properties doesn't grant access to additional assessment data.

| Assessment | File export request |
| --- | --- |
| [Secure configurations](get-assessment-secure-config#2-export-secure-configuration-assessment-via-files) | `GET /api/machines/SecureConfigurationsAssessmentExport` |
| [Software inventory](get-assessment-software-inventory#2-export-software-inventory-assessment-via-files) | `GET /api/machines/SoftwareInventoryExport` |
| [Non-product-code software inventory](get-assessment-non-cpe-software-inventory#2-export-non-product-code-software-inventory-assessment-via-files) | `GET /api/machines/SoftwareInventoryNonCpeExport` |
| [Software vulnerabilities](get-assessment-software-vulnerabilities#2-export-software-vulnerabilities-assessment-via-files) | `GET /api/machines/SoftwareVulnerabilitiesExport` |

## Request the export URLs

Call the file export method for the assessment you need. For example, request the software vulnerabilities export:

```http
GET https://api.security.microsoft.com/api/machines/SoftwareVulnerabilitiesExport
Authorization: Bearer <access-token>
```

The response contains an `exportFiles` array of download URLs and a `generatedTime` value that identifies when the snapshot was generated. Use the complete URLs returned by the service rather than constructing storage account names or file paths.

The download URLs contain shared access signature (SAS) query parameters. Keep those parameters unchanged when checking copy status and downloading files. See the individual method reference for URL validity and the supported `sasValidHours` parameter.

Important

Treat download URLs as credentials. Don't expose their SAS tokens in logs, screenshots, or shared examples. Use each signed storage URL to access its blob; don't send your Defender API bearer token to Blob Storage.

## Check whether each file is ready

For each URL in `exportFiles`, send a `HEAD` request to retrieve the destination blob's properties without downloading its content. Replace the placeholders below with the complete URL returned by the API, including its SAS query string.

```http
HEAD https://<storage-account>.blob.core.windows.net/<container>/<blob>?<sas-token>
```

After a successful `HEAD` response, check the `x-ms-copy-status` header.

| Value | Meaning | Action |
| --- | --- | --- |
| `pending` | The copy is in progress. | Wait, then repeat the `HEAD` request with backoff and a bounded retry period. Don't download yet. |
| `success` | The copy completed successfully. | Proceed to download the file. |
| `failed` | The copy failed. | Don't download. Check `x-ms-copy-status-description` for details and investigate the failure. |
| `aborted` | The copy was canceled. | Don't download. Investigate before requesting another export. |

A `200 OK` response to `HEAD` doesn't, by itself, confirm that an asynchronous copy completed. For a blob being copied asynchronously, wait until `x-ms-copy-status` is `success`.

The header can be absent if the blob wasn't created by Copy Blob or was modified after a completed copy. Absence alone doesn't indicate success or failure. If you expect an asynchronously copied file but the header is missing or unrecognized, stop processing that file and investigate rather than assuming it is ready.

Azure Storage can return `202 Accepted` when a Copy Blob operation starts. This acknowledges the copy request, not completion. It isn't the expected response to the `HEAD` request used here. For details, see [Copy Blob](/en-us/rest/api/storageservices/copy-blob) and [Get Blob Properties](/en-us/rest/api/storageservices/get-blob-properties).

## Download and process the files

After the copy succeeds, send a `GET` request to the same complete download URL.

```http
GET https://<storage-account>.blob.core.windows.net/<container>/<blob>?<sas-token>
```

1. Validate that the HTTP transfer completes before treating the file as downloaded. A successful copy doesn't guarantee that a later network transfer succeeds.
2. Decompress the GZIP file and parse its multiline JSON content.
3. Repeat the readiness check and download for every URL in the export response. Mark the snapshot complete only after every file is downloaded and processed successfully.

## Handle retries and expired URLs

Use bounded retries with backoff for pending copies and transient request failures. Honor `Retry-After` when provided. Don't repeatedly call the export API to poll an existing blob's copy status; use `HEAD` on the returned URL instead.

- If the polling deadline is reached while a copy is still pending, report the file as incomplete. Don't download it as though the copy succeeded.
- If an HTTP request fails, handle the failure separately from the copy-status value. Don't treat an error response or missing response body as a completed file.
- If a download is interrupted, retry that file while its URL is valid. Discard or isolate incomplete local downloads so they aren't processed as complete files.
- If a URL expires, request fresh URLs through the assessment export API, subject to its rate limits. The new response can describe a newer snapshot; don't silently combine files from different snapshots.
- For authorization failures, check the URL's expiry and preserve its complete SAS query string. Don't retry indefinitely or expose the token when reporting the error.