# VM Layout

This document describes the current and planned virtual machine layout
within the Proxmox environment.

The design follows **service isolation by function**, with the flexibility
to split services into dedicated VMs as the lab scales.

---

## Proxmox Host

- Acts as the **virtualization layer** only
- No application services run directly on the host
- Linux bridge (`vmbr0`) provides LAN connectivity to VMs
- VM networking designed to support future VLAN segmentation

---

## Current Virtual Machines

| VM Name           | Role / Services                                    | Notes |
|-------------------|----------------------------------------------------|-------|
| ubuntu-services   | Docker host running core infrastructure services   | Primary services VM |

### Services running on `ubuntu-services`
- Nginx Proxy Manager (reverse proxy, access control)
- Pi-hole (DNS resolver, ad blocking)
- Supporting Docker runtime and networking

This VM represents a **consolidated services node**, suitable for:
- Early-stage homelab
- Managed-network environments
- Rapid iteration and learning

---

## Planned Virtual Machines (Expansion)

| VM Name   | VLAN | Purpose                          |
|----------|------|----------------------------------|
| dns01    | 20   | Dedicated internal DNS (Pi-hole) |
| vpn01    | 20   | WireGuard VPN endpoint           |
| cloud01  | 20   | Nextcloud (self-hosted storage)  |
| media01  | 20   | Jellyfin (media services)        |
| proxy01  | 40   | Reverse proxy / DMZ ingress      |

These VMs will be introduced as:
- Network segmentation is expanded
- Firewall rules (pfSense) are enforced per VLAN
- Services require stricter isolation or scaling

---

## Design Notes

- Initial consolidation reduces operational complexity
- Clear migration path from **single services VM → multi-VM architecture**
- Reverse proxy acts as the controlled ingress point
- DNS, VPN, and application services are intentionally separable
- Layout mirrors real-world progression from small to scaled environments

---

## Future Improvements

- Move public-facing services into a dedicated DMZ VM
- Enforce inter-VLAN firewall rules via pfSense
- Apply per-service monitoring and resource limits
- Introduce high-availability or backup strategies
