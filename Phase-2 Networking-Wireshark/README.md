# Phase 2 — Network Traffic Analysis with Wireshark

## Overview
Phase 2 focuses on network packet capture and analysis. Using port mirroring on the TP-Link TL-SG108E managed switch and Wireshark on the HP ZBook workstation, all network traffic was captured and analyzed at the packet level. This phase builds foundational skills in network security monitoring, protocol analysis, and understanding how data moves across a network.

## Hardware Used
- TP-Link TL-SG108E 8-Port Gigabit Easy Smart Switch
- HP ZBook 16 G11 — packet capture workstation
- Alienware Aurora R12 — Proxmox server running Windows Server 2022 VM
- QGeeM USB-C to Gigabit Ethernet adapter

## Software Used
- Wireshark 4.x
- TP-Link Easy Smart Configuration Utility

## Theory

### What is Port Mirroring?
Port mirroring is a feature on managed switches that copies all traffic from selected source ports to a designated destination port. Without port mirroring, a device only sees traffic addressed directly to itself. With port mirroring enabled, the destination port receives a copy of every packet flowing through the network — making full traffic analysis possible.

This is the same technique used by security teams in real enterprise environments to feed traffic into IDS systems and packet analyzers without disrupting network operations.

### What is a Packet?
A packet is a unit of data transmitted over a network. Every communication — whether a website request, a login, a file transfer, or a ping — is broken into packets. Each packet contains a header with source address, destination address, and protocol information, plus a payload containing the actual data. Wireshark captures and decodes these packets in real time, allowing you to read network conversations at the lowest level.

### The OSI Model in Practice
This phase provided hands-on experience with multiple OSI layers simultaneously:
- **Layer 2 (Data Link):** Ethernet frames, MAC addresses, ARP
- **Layer 3 (Network):** IP addresses, ICMP
- **Layer 4 (Transport):** TCP, UDP
- **Layer 7 (Application):** DNS, HTTP, SMB, TLS

### Why Encryption Matters
One of the most important demonstrations in this phase was comparing HTTP and HTTPS traffic. Unencrypted HTTP traffic is completely readable in Wireshark — headers, user agents, URLs, and potentially credentials are all visible in plain text to anyone on the same network segment. TLS encrypted traffic shows only that a connection occurred and how much data was transferred — the actual content is completely unreadable without the private key.

## Steps Completed

### 1. Switch Access and Configuration
- Downloaded and installed TP-Link Easy Smart Configuration Utility
- Utility automatically discovered switch on network at 10.0.0.184
- Logged in and accessed switch management interface
- Navigated to Monitoring tab and selected Port Mirror

### 2. Port Mirroring Setup
- Set Port Mirror Status to Enable
- Set Mirroring Port to Port 3 (ZBook destination)
- Enabled Ingress and Egress on Port 1 (router) and Port 2 (Alienware)
- Port 3 left as destination only — cannot mirror to itself
- Clicked Apply to save configuration

### 3. Wireshark Installation and First Capture
- Launched Wireshark on ZBook
- Selected Ethernet 3 interface (USB-C adapter connected to switch)
- Started live capture — immediately saw network traffic from all devices
- Observed MDNS, UDP, IGMPv3 background traffic

### 4. Protocol Analysis

#### ICMP — Ping Traffic
- Applied filter: icmp
- Generated ping traffic using Command Prompt: ping 10.0.0.1
- Captured ICMP Request and Reply packets
- Expanded Internet Protocol layer to read source and destination IPs
- Confirmed source and destination addresses flip between request and reply
- Source: 10.0.0.80 (ZBook) → Destination: 10.0.0.1 (router) on request
- Source: 10.0.0.1 (router) → Destination: 10.0.0.80 (ZBook) on reply

#### DNS — Domain Name Resolution
- Applied filter: dns
- Browsed to multiple websites to generate DNS queries
- Captured Standard Query and Standard Query Response packets
- Read domain names in Info column — login.microsoftonline.com, manage.microsoft.com, google.com
- Confirmed every website visit begins with a DNS lookup before any connection is made

#### SMB — Windows File Sharing
- Applied filter: smb
- Browsed network resources inside Windows Server 2022 VM
- Captured SMB Host Announcement packets
- Identified YOUNES workstation and WIN-6K5I2BSEKE2 domain controller announcements
- Noted security relevance — WannaCry, NotPetya, and EternalBlue all exploited SMB vulnerabilities

#### ARP — Address Resolution Protocol
- Applied filter: arp
- Observed ARP broadcast traffic: "Who has 10.0.0.80? Tell 10.0.0.1"
- Understood ARP has no authentication mechanism
- Identified ARP spoofing as the foundation of man-in-the-middle attacks
- This attack will be demonstrated in Phase 6 using Kali Linux

#### HTTP vs TLS — Encryption Demonstration
- Applied filter: http
- Visited neverssl.com (deliberately unencrypted site)
- Read full HTTP headers, GET requests, user agent, and browser information in plain text
- Applied filter: tls
- Visited google.com and observed TLS 1.3 handshake
- Confirmed Client Hello, Server Hello, Change Cipher Spec, and Application Data
- Payload completely unreadable — encryption working as intended

## Key Security Findings

| Protocol | Security Risk | Real World Mitigation |
|---|---|---|
| ARP | No authentication — spoofing and MITM attacks possible | Dynamic ARP Inspection, VLANs, network segmentation |
| HTTP | Traffic readable in plain text by anyone on network | Always use HTTPS, enforce HSTS |
| SMB | Historical exploit target — major ransomware vector | Keep patched, disable SMBv1, segment network |
| DNS | Queries visible — privacy concern, DNS spoofing possible | DNS over HTTPS, DNSSEC |
| ICMP | Can be used for reconnaissance and data exfiltration | Rate limiting, firewall rules |

## Troubleshooting

| Problem | Cause | Fix |
|---|---|---|
| Could not access switch web interface | Switch got DHCP IP, not default 192.168.0.1 | Used TP-Link Easy Smart Configuration Utility to discover switch |
| Ethernet adapter not recognized | Wrong adapter selected in ncpa.cpl | Identified correct adapter as Ethernet 3 — Realtek USB GbE |
| Switch login failed after IP change | Session lost when IP changed | Reset switch, re-logged in with admin credentials |

## Screenshots
(screenshots coming)

## Skills Demonstrated
- Managed switch configuration and port mirroring
- Live network packet capture with Wireshark
- Protocol analysis — ICMP, DNS, ARP, SMB, HTTP, TLS
- OSI model practical application across multiple layers
- Network security concepts — encryption, ARP spoofing, protocol vulnerabilities
- Identifying sensitive data exposure in unencrypted traffic
- Network troubleshooting and device discovery
