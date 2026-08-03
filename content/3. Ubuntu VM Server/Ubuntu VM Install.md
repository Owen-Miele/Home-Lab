---
title: Ubuntu Server Installation
---

## Objective

 Create an Ubuntu Server virtual machine in Proxmox VE to host an all-in-one Wazuh SIEM deployment.

## Environment

| Component               | Configuration                   |
| ----------------------- | ------------------------------- |
| Operating System        | Ubuntu Server 26.04 LTS         |
| Hostname                | SIEM                            |
| Ubuntu Server IP        | 192.168.8.128                   |
| Wazuh Dashboard         | https://192.168.8.128:443       |
| SIEM Platform           | Wazuh                           |
| Wazuh Website           | [wazuh.com](https://wazuh.com/) |
| Virtualization Platform | Proxmox VE                      |
| Virtual Network         | Proxmox bridge vmbr0            |
| Lab Subnet              | 192.168.8.0/24                  |
| Default Gateway         | 192.168.8.1                     |
| DNS Server              | 192.168.8.1                     |
| Virtual CPUs            | 4 vCPUs                         |
| Memory                  | 8 GB                            |
| Virtual Disk            | 70 GB                           |
| Network Adapter         | VirtIO                          |

## Prequisites

- Proxmox

# Procedure

1.  Download the Ubuntu 64-bit  AMD64 Ubuntu Server ISO
2. Upload the ISO file to Proxmox
3. Click 'Create VM'
4. I named it 'SIEM' because it will function as my host for Wazuh
5. Click 'Next', and in 'OS' choose the Linux server ISO and make the 'guest OS Type' Linux. Make the version 'recent Linux kernel'. Click 'Next'.
6. In 'System', keep the defaults and click 'Next'.
7. For 'Disk', I used 70 GiB and checked 'Discard'. Click 'Next'.
8. For 'CPU', use 1 socket, 4 Cores, 4 VCPUs, CPU limit 4, and the 'Type' should be HOST. Click 'Next'
9. In 'Memory', I used 8192 MiB for the memory and disabled ballooning so 8GB of RAM would always be available to the server. Click 'Next'.
10. For 'Network', leave all defaults and click 'Finish'.
11. When done installing, start the VM and open the console.
12. Select English and Ubuntu Server for the installation type. We do not want the minimized version. Leave search for third-party drivers unchecked.
13. If the server detects the VirtIO adapter, select Done for the network configuration and proxy configuration.
14. Accept the automatically accepted archive mirror.
15. For the storage configuration, use an entire disk, set up this disk as an LVM group, and ensure LUKS and custom storage layout are disabled. Select 'Done'.
16. Set up your user profile.
17. Skip Ubuntu pro for now.
18. Enable the installation of the OpenSSH server and allow password authentication over SSH. Leave all optional snaps unchecked. Do not install any other services and select 'Done'.
19. When prompted, select 'Reboot Now'.
20. Attempt to SSH from username@ipaddress or just log in to the Ubuntu box with your credentials normally.
21. Update with these commands
    sudo apt update
    sudo apt upgrade -y
    sudo apt install -y curl
