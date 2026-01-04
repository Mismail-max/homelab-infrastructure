# Nextcloud Service Runbook

## 1. Overview

**Service Name:** Nextcloud  
**Service Type:** Self-hosted file, photo, and document storage  
**Primary Purpose:** Replacement for iCloud and other cloud storage providers

Nextcloud is deployed as a core internal service to provide file synchronization,
photo backups, and remote access to personal data while maintaining full control
over storage, security, and backups.

---

## 2. Architecture

### Network Placement
- **VLAN:** 20 (SERVERS)
- **IP Address:** 10.10.20.30 (static)
- **Access Method:**
  - Internal LAN access
  - Remote access via WireGuard VPN
  - Optional HTTPS access via reverse proxy

### Dependencies
- Internal DNS service
- Proxmox host storage
- Reverse proxy (for HTTPS termination)
- Backup target (external or secondary storage)

### High-Level Flow
Client → (VPN or LAN) → Reverse Proxy → Nextcloud VM → Storage

---

## 3. Infrastructure Details

### Virtual Machine
- **Hypervisor:** Proxmox VE
- **OS:** Ubuntu Server LTS
- **CPU:** 2 vCPUs
- **Memory:** 4 GB RAM
- **Disk:**
  - OS disk: 32 GB
  - Data disk: mounted from Proxmox storage pool

### Storage Layout
- Application data stored outside the OS disk
- Data volume mounted at `/var/www/nextcloud/data`
- Designed to allow storage expansion without OS reinstallation

---

## 4. Security Model

### Authentication
- User authentication handled by Nextcloud
- Strong passwords enforced
- 2FA planned (TOTP)

### Network Security
- Service not exposed directly to the internet
- External access only via:
  - WireGuard VPN, or
  - Reverse proxy in DMZ with HTTPS

### TLS / Encryption
- HTTPS enabled via reverse proxy
- TLS certificates managed centrally
- Data at rest protected via filesystem permissions

---

## 5. Backups and Recovery

### Backup Strategy
- Nightly Proxmox VM backups
- Weekly off-host backup to external storage
- Critical data prioritized over media content

### Restore Process (High Level)
1. Restore VM from Proxmox backup
2. Verify data volume integrity
3. Validate service availability via web UI

### Known Risks
- Single-disk storage currently lacks redundancy
- Mitigation: frequent backups and planned disk expansion

---

## 6. Monitoring and Health

### Monitored Metrics
- VM uptime
- Disk usage
- HTTP service availability

### Alerts
- Disk usage > 80%
- VM unreachable
- Service port not responding

---

## 7. Operational Procedures

### Common Tasks

**Restart service**
```bash
systemctl restart apache2
