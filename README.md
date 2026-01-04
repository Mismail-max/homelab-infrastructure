# Homelab Infrastructure

This repository documents a production-style homelab built to practice
real-world networking, virtualization, storage, and service operations.

## Goals
- Replace paid cloud services (storage, media, VPN)
- Practice enterprise networking (VLANs, routing, NAT)
- Build hands-on SRE / Network experience
- Operate services with monitoring, backups, and documentation

## High-Level Architecture
- Cisco 1800 router (WAN, NAT, DHCP)
- Cisco Catalyst 3560 (VLANs, inter-VLAN routing)
- Proxmox VE as private cloud
- Segmented network (MGMT, SERVERS, USERS, DMZ)

## Key Skills Demonstrated
- Layer 2/3 networking (DNS, NAT, VLANs, SVIs, routing)
- Virtualization with Proxmox VE
- Firewall configuration and traffic control (pfSense)
- Docker-based service deployment and isolation
- Reverse proxy and access control (Nginx Proxy Manager)
- Secure remote access via SSH (PowerShell → Linux)
- Cisco IOS configuration
- Linux CLI administration and troubleshooting
- DNS architecture and analysis (Pi-hole query inspection)
- Self-hosted services (Nextcloud, Jellyfin, WireGuard)
- Infrastructure documentation and operational design
- Monitoring and operational documentation

See subdirectories for detailed design and configs.
