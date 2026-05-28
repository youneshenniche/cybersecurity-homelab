# Phase 1 — Proxmox Hypervisor and Active Directory

## Overview
Phase 1 covers building the foundation of the home lab. This includes installing a Type-1 hypervisor on bare metal hardware, configuring network connectivity, and deploying a Windows Server 2022 virtual machine with a fully functional Active Directory domain.

## Hardware Used
- Alienware Aurora R12 — dedicated Proxmox server
- HP ZBook 16 G11 — management workstation
- TP-Link TL-SG108E managed switch
- QGeeM USB-C to Gigabit Ethernet adapter

## Software Used
- Proxmox VE 9.1
- Windows Server 2022 Standard Evaluation
- VirtIO drivers
- Active Directory Domain Services
- Group Policy Management Console

## Theory

### What is a Type-1 Hypervisor?
A hypervisor is software that creates and manages virtual machines. Type-1 hypervisors run directly on bare metal hardware with no underlying operating system. This gives VMs direct access to CPU, RAM, and storage with maximum efficiency. Proxmox VE is a Type-1 hypervisor, the same architecture used by VMware ESXi and Microsoft Hyper-V in enterprise environments.

### What is Active Directory?
Active Directory Domain Services is Microsoft's directory service for managing users, computers, and resources across a network. Every organization with Windows infrastructure uses it. Key components include domains, organizational units, group policy, DNS, and user accounts.

### What are VLANs?
A VLAN (Virtual Local Area Network) segments a physical network into isolated logical networks. This means devices on different VLANs cannot communicate unless explicitly allowed. Used in this lab to separate management, server, and attack traffic.

## Steps Completed

### 1. Preparing the Proxmox Installer
- Downloaded Proxmox VE 9.1 ISO from proxmox.com
- Flashed ISO to 128GB USB drive using Rufus Portable in DD image mode

### 2. BIOS Configuration
Several BIOS settings required adjustment before Proxmox would install correctly:
- Disabled Secure Boot — prevented Proxmox from booting
- Added nomodeset kernel parameter — NVIDIA GPU caused display to freeze during boot
- Changed SATA mode from RAID to AHCI — Proxmox could not detect the internal drive in RAID mode

### 3. Installing Proxmox VE
- Booted from USB using UEFI boot mode
- Installed Proxmox to internal 256GB NVMe SSD
- Configured static IP: 10.0.0.100
- Set gateway: 10.0.0.1
- Set DNS: 8.8.8.8

### 4. Network Setup
- Connected TP-Link TL-SG108E managed switch
- Router connected to switch port 1
- Alienware connected to switch port 2
- ZBook connected via USB-C ethernet adapter to switch port 3
- Accessed Proxmox web UI at https://10.0.0.100:8006 from ZBook browser

### 5. Creating the Windows Server 2022 VM
- Downloaded Windows Server 2022 evaluation ISO from Microsoft
- Downloaded VirtIO drivers ISO from Fedora
- Uploaded both ISOs to Proxmox local storage
- Created VM with these specifications:
  - CPU: 2 cores
  - RAM: 4GB
  - Storage: 60GB
  - BIOS: OVMF (UEFI)
  - Network: VirtIO
- Installed VirtIO SCSI driver during Windows setup to allow disk detection
- Installed VirtIO network driver after Windows installation
- Installed QEMU Guest Agent for Proxmox integration

### 6. Active Directory Setup
- Installed Active Directory Domain Services role via Server Manager
- Promoted server to Domain Controller
- Created new forest: homelab.local
- Configured DNS server during promotion

### 7. Active Directory Configuration
- Created Organizational Unit: IT Department
- Created domain users: jsmith (John Smith) and jdoe (Jane Doe)
- Moved users into IT Department OU
- Created Group Policy Object: IT Security Policy
- Linked GPO to IT Department OU
- Configured password policies:
  - Minimum password length: 8 characters
  - Maximum password age: 90 days
  - Password complexity: Enabled
  - Password history: 5 passwords remembered

## Troubleshooting
| Problem | Cause | Fix |
|---|---|---|
| Proxmox frozen on boot | Secure Boot enabled | Disabled Secure Boot in BIOS |
| Black screen after Proxmox menu | NVIDIA GPU conflict | Added nomodeset to kernel parameters |
| No hard disk found in installer | SATA controller in RAID mode | Changed SATA mode to AHCI in BIOS |
| No hard disk in Windows installer | Missing VirtIO SCSI driver | Loaded vioscsi driver from VirtIO ISO |
| No network in Windows | Missing VirtIO network driver | Installed NetKVM driver from VirtIO ISO |

## Screenshots
(Add your screenshots here)

## Skills Demonstrated
- Bare metal server deployment
- Type-1 hypervisor installation and configuration
- Virtual machine creation and management
- Windows Server 2022 administration
- Active Directory design and deployment
- Organizational Unit structure
- Domain user account management
- Group Policy Object creation and configuration
- Hardware troubleshooting and BIOS configuration
- Network configuration and static IP assignment
