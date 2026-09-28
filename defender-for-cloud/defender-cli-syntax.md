---
layout: Conceptual
title: Defender for Cloud CLI Syntax - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-cli-syntax
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
description: Discover how to scan container images for security risks using Microsoft Container Security Scanner. Includes syntax, parameters, and examples.
ms.date: 2026-02-12T00:00:00.0000000Z
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: 13c15094-c3da-49c4-c3a7-922012f56707
document_version_independent_id: e249ca2f-3a29-a2bc-5f64-cddc5fb48c7d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-cli-syntax.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-cli-syntax
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-cli-syntax.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 45c5e922-3313-b4b3-66b7-6a19bd1face1
---

# Defender for Cloud CLI Syntax - Microsoft Defender for Cloud | Microsoft Learn

The Defender for Cloud CLI provides commands to scan container images for security vulnerabilities and export results in standard formats. This article describes the syntax, parameters, and usage examples for the image and SBOM scan commands.

## CLI Options

| Option | Required | Type | Description |
| --- | --- | --- | --- |
| `--defender-debug` | No | Bool | Output debug information to the console. |
| `--output-formats` | No | String | Option: HTML |
| `--defender-output` | No | String | Sets the path to the output file [default: `pwd`] |
| `--defender-break` | No | Bool | Exit with a non-zero code if critical issues are found |

## Image Scan

Use the `defender scan image` command to scan container images for vulnerabilities using Microsoft Defender Vulnerability Management (MDVM).

### Usage

```bash
defender scan image <image-name> [--defender-output <path>]
```

### Options

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| &lt;image-name&gt; | Yes | String | The container image reference (for example, `my-image:latest`, `registry.azurecr.io/app:v1`). |

### Examples

#### Scan a local image

```bash
defender scan image my-image:latest
```

#### Scan and export SARIF results

```bash
defender scan image my-image:latest --defender-output results.sarif
```

## SBOM Scan

Use the `defender scan sbom` command to scan filesystem or container images to generate a Software Bill of Materials (SBOM). This command also identifies malicious packages.

### Usage

```bash
defender scan sbom <target> [--sbom-format <format>]
```

### Options

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| &lt;target&gt; | Yes | String | The container image reference or filesystem (for example, `my-image:latest`, `/home/src/`). |
| --sbom-format | No | String | SBOM output format. Default: `cyclonedx1.6-json` |
| --output | No | String | Output path for generated SBOM file (default: `sbom-finding-<timestamp>.json`) |

#### Valid format options:

- `cyclonedx1.4-json`, `cyclonedx1.4-xml`
- `cyclonedx1.5-json`, `cyclonedx1.5-xml`
- `cyclonedx1.6-json`, `cyclonedx1.6-xml`
- `spdx2.3-json`

### Examples

#### Create SBOM of a container image

```bash
defender scan sbom my-image:latest
```

#### Create SBOM from local filesystem

```bash
defender scan sbom /home/src --sbom-format cyclonedx1.6-xml
```

## AI Model Scan

Use the `defender scan model` command to scan AI models for security risks including malware, unsafe operators, and exposed secrets. This command supports models stored locally or in cloud registries such as Hugging Face, and common formats including Pickle (`.pkl`), ONNX (`.onnx`), TorchScript (`.pt`), TensorFlow, and SafeTensors.

### Usage

```bash
defender scan model <target> [--modelscanner-Output <path>]
```

### Options

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| &lt;target&gt; | Yes | String | The path to a local model file or directory, or a Hugging Face model URL (for example, `./models/my-model.pkl`, `https://huggingface.co/org/model`). |
| --modelscanner-Output | No | String | Output path for SARIF scan results. |

### Supported model formats

- Pickle (`.pkl`)
- ONNX (`.onnx`)
- TorchScript (`.pt`)
- TensorFlow (`.tf`, `.pb`)
- SafeTensors (`.safetensors`)

### Examples

#### Scan a local model

```bash
defender scan model ./models/my-model.pkl
```

#### Scan a Hugging Face model

```bash
defender scan model "https://huggingface.co/org/model-name"
```

#### Scan and export SARIF results

```bash
defender scan model ./models/my-model.onnx --modelscanner-Output results.sarif
```