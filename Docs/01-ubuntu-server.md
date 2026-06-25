# Phase 1 - Ubuntu Server Deployment

## Objective

Deploy and configure an Ubuntu Server virtual machine on Proxmox to serve as the foundation for the Elastic SIEM.

## VM Configuration

- OS: Ubuntu Server 24.04.4 LTS
- vCPU: 4
- RAM: 8 GB
- Disk: 100 GB
- BIOS: OVMF (UEFI)
- SCSI Controller: VirtIO SCSI
- Network: VirtIO
- Hostname: soc01

## Server Configuration

- Updated system packages
- Installed OpenSSH Server
- Installed QEMU Guest Agent

## Verification

The following checks were completed to verify the server was ready for the Elastic Stack:

- Verified internet connectivity
- Verified DNS resolution
- Verified QEMU Guest Agent communication
- Created a baseline snapshot

## Key Takeaways

- Modern virtual hardware matters. I chose UEFI (OVMF) and the q35 machine type because they provide better compatibility with modern operating systems and are the recommended configuration for new virtual machines.
- VirtIO improves VM performance. Using VirtIO drivers for storage and networking allows the guest operating system to communicate more efficiently with the Proxmox host than emulated hardware.
- Guest integration improves management. Installing the QEMU Guest Agent allows Proxmox to retrieve the VM's IP address, perform smoother shutdowns, and improve backup and snapshot operations.
