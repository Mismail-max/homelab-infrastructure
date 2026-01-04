# IP & VLAN Plan

## VLAN Overview

| VLAN | Name    | Subnet           | Purpose |
|-----:|---------|------------------|---------|
| 10   | MGMT    | 10.10.10.0/24    | Network & hypervisor management |
| 20   | SERVERS | 10.10.20.0/24    | Application VMs |
| 30   | USERS   | 10.10.30.0/24    | Trusted user devices |
| 40   | DMZ     | 10.10.40.0/24    | Public-facing services |
| 99   | TRANSIT | 10.10.99.0/30    | Switch-router link |

## Routing
- Inter-VLAN routing performed on Catalyst 3560
- Default route points to Cisco 1800 via transit VLAN
- Cisco 1800 performs NAT and internet access

## Security Model
- DMZ isolated from MGMT
- IOT/GUEST restricted from SERVERS
- MGMT VLAN permitted to all for administration
