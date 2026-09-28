---
layout: Conceptual
title: Protocols supported by Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/concept-supported-protocols
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
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
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
description: Learn about protocols that Microsoft Defender for IoT supports.
ms.date: 2023-12-04T00:00:00.0000000Z
ms.topic: concept-article
ms.custom: enterprise-iot
locale: en-us
document_id: 29e3a1ad-0c7d-e379-2307-0c6bd10d1979
document_version_independent_id: 17ad225f-d941-9713-d9d7-260375ad0689
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/concept-supported-protocols.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/concept-supported-protocols
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/concept-supported-protocols.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 6badba64-f134-7aa7-7d60-1df0eac57300
---

# Protocols supported by Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

This article lists the protocols that are supported by default in Microsoft Defender for IoT.

## Supported protocols for OT device discovery

OT network sensors can detect the following protocols when identifying assets and devices in your network:

| Brand / Vendor | Protocols |
| --- | --- |
| **ABB** | ABB 800xA DCS (IEC61850 MMS including ABB extension) CNCP RNRP ABB IAC ABB Totalflow  ABB NetConfig |
| **ASHRAE** | BACnet BACnet BACapp BACnet BVLC |
| **Beckhoff** | AMS (ADS) Twincat |
| **Cisco** | CAPWAP Control CAPWAP Data CDP LWAPP |
| **DICOM** | Dicom |
| **Desoutter Protocol** | Open |
| **DNP. org** | DNP3 |
| **Emerson** | DeltaV DeltaV - Discovery Emerson OpenBSI/BSAP Ovation DCS ADMDOvation DCS DPUSTAT Ovation DCS SSRPC |
| **Emerson Fischer** | ROC |
| **EVRoaming Foundation** | OCPI |
| **FANUC** | FANUC FOCUS |
| **FieldComm Group** | HART-IP |
| **GE** | ADL (MarkVIe) Bentley Nevada (System 1 / BN3500)ClassicSDI (MarkVle)  EGD GSM (GE MarkVI and MarkVIe) InterSite SDI (MarkVle)  SRTP (GE) GE\_CMP |
| **Generic Applications** | Active Directory RDP Teamviewer VNC |
| **Honeywell** | ENAP Experion DCS CDA Experion DCS FDA Honeywell EUCN  Honeywell Discovery |
| **IEC** | Codesys V3IEC 60870-5-7 (IEC 62351-3 + IEC 62351-5) IEC 60870-5-104 IEC 60870-5-104 ASDU\_APCI IEC 60870 ICCP TASE.2 IEC 61850 GOOSE IEC 61850 MMS IEC 61850 SMV (SAMPLED-VALUES) LonTalk (LonWorks) |
| **IEEE** | LLC STP VLAN |
| **IETF** | ARP DHCP DCE RPC DNS FTP (FTP\_ADAT FTP\_DATA) GSSAPI (RFC2743) HTTP ICMP IPv4 LLDP MDNS NBNS NTLM (NTLMSSP Auth Protocol) RPC SMB / Browse / NBDGM SMB / CIFS SNMP SPNEGO (RFC4178) SSH Syslog TCP Telnet TFTP TPKT UDP |
| **ISO** | CLNP (ISO 8473) COTP (ISO 8073) ISO Industrial Protocol MQTT (IEC 20922) |
| **Jenesys** | FOX Niagara |
| **Medical** | ASTM HL7  DICOM  POCT1 |
| **Mitsubishi** | Melsoft / Melsec (Mitsubishi Electric) |
| **Omron** | FINS HTTP |
| **OPC** | AE Common  DA HDA  UA |
| **Oracle** | TDS TNS |
| **Rockwell Automation** | CSP2 ENIP EtherNet/IP CIP (including Rockwell extension) EtherNet/IP CIP FW version 27 and above Rockwell AADvance Discover  Rockwell AADvance SNCP/IXL |
| **Samsung** | Samsung TV |
| **Schneider Electric** | Modbus/TCP Modbus TCP–Schneider Unity Extensions OASYS (Schneider Electric Telvant) Schneider TSAA  Schneider NetManage |
| **Schneider Electric / Invensys** | Foxboro Evo Foxboro I/A Trident TriGP TriStation |
| **Schneider Electric / Modicon** | Modbus RTU |
| **Schneider Electric / Wonderware** | Wonderware Suitelink |
| **SEL** | FTP  Telnet |
| **Siemens** | CAMP PCS7 PCS7 WinCC – Historian Profinet DCP Profinet I/O Profinet Realtime Siemens PHD Siemens S7 Siemens S7 - Firmware and model extraction Siemens S7 – key state Siemens S7-Plus Siemens SICAM Siemens WinCC |
| **Toshiba** | Toshiba Computer Link |
| **Yokogawa** | Centum ODEQ (Centum / ProSafe DCS) HIS Equalize FA-M3 Vnet/IP |

## Supported OT protocols for active monitoring

OT sensors support active monitoring for the following protocols:

| Scan type | Supported protocols | Method |
| --- | --- | --- |
| **Windows event scans** | - WMI | [Configure Windows Endpoint Monitoring](configure-windows-endpoint-monitoring) |
| **DNS lookup scans** | - DNS | [Configure reverse DNS lookup](configure-reverse-dns-lookup) |

## Supported protocols for Enterprise IoT device discovery

Enterprise IoT network sensors can detect the following protocols when identifying assets and devices in your network:

| Brand / Vendor | Protocols |
| --- | --- |
| **ALARIS** | BAXTER |
| **ASHRAE** | BACnet BACapp |
| **Cisco** | CDP |
| **IANA** | SIP |
| **IETF** | BROWSE  DHCP  DNS  HTTP  LLDP  MDNS  SNMP SSDP |
| **Medical** | DICOM HL7 POCT1 |
| **SWARM** | swarm |