---
title: Proxmox Installation
---

## Objective

Install and configure Proxmox on a Dell OptiPlex 7010 to serve as the virtualization platform for the home lab. The Proxmox host will run the Ubuntu-based Wazuh SIEM and Windows Server 2025 virtual machines.

## Envirmonment

| Component                       | Configuration                                         |
| ------------------------------- | ----------------------------------------------------- |
| Hypervisor                      | Proxmox VE                                            |
| Physical Host                   | Dell OptiPlex 7010                                    |
| Processor                       | Intel x86-64 processor with virtualization enabled    |
| Physical Memory                 | 16 GB RAM                                             |
| Physical Storage                | 250 GB internal drive                                 |
| Installation Media              | 4 GB microSD card with USB adapter                    |
| Boot Mode                       | UEFI                                                  |
| Secure Boot                     | Disabled during installation                          |
| Intel Virtualization Technology | Enabled                                               |
| Intel VT-d                      | Enabled                                               |
| Hostname                        | proxmox.home.arpa                                     |
| Management IP Address           | 192.168.8.50/24                                       |
| Default Gateway                 | 192.168.8.1                                           |
| DNS Server                      | 192.168.8.1                                           |
| Management URL                  | https://192.168.8.50:8006                             |
| Management Account              | root                                                  |
| Authentication Realm            | Linux PAM                                             |
| Network Interface               | Physical Ethernet adapter                             |
| Virtual Network Bridge          | vmbr0                                                 |
| Lab Subnet                      | 192.168.8.0/24                                        |
| Router                          | GL.iNet Opal                                          |
| Switch                          | Managed NETGEAR Ethernet switch                       |
| Planned Virtual Machines        | Ubuntu Server with Wazuh SIEM and Windows Server 2025 |

## Prerequisites

- Fresh computer with hardware virtualization support, 16 GB of RAM, and at least 250 GB of storage.

## Procedure
 1. Download the Proxmox VE ISO, insert a 4 GB minimum USB drive, open balenaEtcher, select the Proxmox ISO, select the USB drive, and flash the ISO to the drive. This process will erase all data stored on the USB drive.
 2. Insert the installer into the Dell OptiPlex, turn on the computer, and press 'F2' to enter BIOS Setup. Set Boot Mode to UEFI, disable Secure Boot, enable Virtualization Technology, and enable VT for Direct I/O. Save the changes, restart the computer, press F12 to open the one-time boot menu, and select the USB storage device. 
 3. At the Proxmox installation menu, select 'Install Proxmox VE (Graphical)'. Choose the internal 250 GB drive as the installation target and verify that the USB installer is not selected. Set the country to United States, the time zone to America/New_York, and the keyboard layout to U.S. English. Create a strong root password and enter a valid administrative email address. 
 4. Configure the Proxmox network settings with the hostname proxmox.home.arpa, IP address 192.168.8.50/24, gateway 192.168.8.1, and DNS server 192.168.8.1. Review the installation summary, confirm that the correct internal drive and network settings are selected, and begin the installation. When installation finishes, remove the USB installer, reboot the OptiPlex, and allow it to boot from the internal drive. 
 5. From another computer connected to the same network, open https://192.168.8.50:8006. Accept the browser certificate warning and log in with the username 'root', the Linux PAM authentication realm, and the root password created during installation. Open the Proxmox shell and run
    bash 
    apt update 
    apt full-upgrade -y dpkg --configure -a 
    apt-get -f install
