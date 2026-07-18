# Home Lab Documentation

## Table of Contents

1. [Overview](#overview)
2. [Hardware Inventory](#hardware-inventory)
3. [Software Stack](#software-stack)
4. [Network Architecture](#network-architecture)
5. [Storage Setup](#storage-setup)
6. [Power & Cooling](#power--cooling)
7. [Security](#security)
8. [Monitoring & Maintenance](#monitoring--maintenance)
9. [Backup Strategy](#backup-strategy)
10. [Troubleshooting](#troubleshooting)

---

## Overview

**Purpose**: Documenting My home lab infrastructure and configurations for easy reference and management.

**Last Updated**: 7/18/2026
**Maintained By**: Rapter
**Total Systems**: 4 nodes

### Key Goals

- [ ] Continuous learning environment
- [ ] Testing and development platform
- [ ] Service hosting and experimentation
- [ ] High availability exploration

---

## Hardware Inventory

### Compute Nodes

| Hostname | CPU | RAM | Storage | OS | Role | Status |
|----------|-----|-----|---------|----|----|--------|
| node-01 |4 Core|12G|128G|Ubuntu Server 24.04|Bare Metal|Online|
| node-02 |4 Cores|16G|120G|Ubuntu Server 24.04|VM-DOCKER|Online|
| node-03 | | | | | | |

### Network Equipment

| Device | Model | Location | IP Address | Notes |
|--------|-------|----------|------------|-------|
| Router | | | | |
| Switch | | | | |
| Firewall | | | | |
| Access Point | | | | |

### Storage Devices

| Device | Capacity | Type | Connection | Location | Notes |
|--------|----------|------|-----------|----------|-------|
| | | HDD/SSD | | | |
| | | HDD/SSD | | | |

### Other Equipment

- **PDU (Power Distribution Unit)**: 
- **UPS (Uninterruptible Power Supply)**: 
- **Monitor**: 
- **KVM Switch**: 
- **Cables & Accessories**: 

---

## Software Stack

### Operating Systems

| System | Version | Purpose | Node(s) |
|--------|---------|---------|---------|
| Ubuntu Server | 24.04 LTS | Base OS | |
| Proxmox VE | | Hypervisor | |
| TrueNAS | | Storage | |

### Container & Orchestration

- **Docker**: Container runtime
  - Configuration: `/etc/docker/daemon.json`
  - Compose files: `docker-compose.yml`
  
- **Kubernetes** (if applicable):
  - Cluster type: 
  - Version: 
  - ETCD backups location: 

### Core Services

#### Virtualization
- **Proxmox VE** / **KVM** / **Hyper-V**: Virtual machine hypervisor

#### Networking
- **Pi-hole**: DNS & ad blocking
- **Unbound**: DNS resolver

#### Media & Storage
- **Plex / Jellyfin**: Media server
- **Nextcloud**: File storage & sync
- **Samba**: File sharing

#### Monitoring & Logging
- **Prometheus**: Metrics collection
- **Grafana**: Metrics visualization
- **ELK Stack** / **Loki**: Log aggregation

#### Other Services
- **Home Assistant**: Home automation
- **Nginx / Apache**: Reverse proxy & web server
- **Portainer**: Docker management UI

### Development Tools

- Git
- Python
- Node.js
- Go
- Docker CLI

---

## Network Architecture

### Network Topology

```
┌─────────────────────────────────────────┐
│          ISP / WAN                      │
└──────────────────┬──────────────────────┘
                   │
        ┌──────────▼──────────┐
        │   Router/Firewall   │
        └──────────┬──────────┘
                   │
        ┌──────────▼──────────┐
        │  Network Switch     │
        └──────────┬──────────┘
           ┌───────┼───────┐
           │       │       │
        ┌──▼──┐ ┌──▼──┐ ┌──▼──┐
        │Node1│ │Node2│ │Node3│
        └─────┘ └─────┘ └─────┘
```

### IP Address Scheme

| Network | CIDR | Purpose | Gateway | DNS |
|---------|------|---------|---------|-----|
| Management | 192.168.1.0/24 | Admin & core services | 192.168.1.1 | 8.8.8.8 |
| Containers | 10.0.0.0/24 | Docker/K8s services | 10.0.0.1 | local |
| VM Guest | 10.1.0.0/24 | Virtual machines | 10.1.0.1 | local |
| Guest WiFi | 10.2.0.0/24 | Guest network | 10.2.0.1 | local |

### VLAN Configuration

| VLAN ID | Name | Purpose | Subnet |
|---------|------|---------|--------|
| 1 | Management | Admin access | 192.168.1.0/24 |
| 10 | Services | Container/service network | 10.0.0.0/24 |
| 20 | VMs | Virtual machine network | 10.1.0.0/24 |
| 99 | Guest | Guest/untrusted network | 10.2.0.0/24 |

### Port Mappings

| External Port | Internal Port | Service | Node | Notes |
|---------------|---------------|---------|------|-------|
| 80 | 8080 | Web UI | | HTTP redirect |
| 443 | 8443 | Web UI | | HTTPS |
| 8000 | 8000 | Service 1 | | |

---

## Storage Setup

### Local Storage

| Mount Point | Capacity | Filesystem | Device | Purpose |
|-------------|----------|-----------|--------|---------|
| / | | ext4 | | OS root |
| /mnt/storage | | ext4/btrfs | | Data storage |
| /mnt/media | | | | Media library |

### Network Storage

| Name | Type | Capacity | Protocol | IP Address | Mount Point |
|------|------|----------|----------|------------|-------------|
| NAS-01 | TrueNAS | | NFS/SMB | 192.168.1.100 | /mnt/nas |

### Backup Destinations

- **Local External**: `/backup/external/` - Weekly backups
- **Remote Cloud**: S3/B2 - Monthly backups
- **Offsite**: External HDD at secure location

### Partitioning Scheme

```bash
# Example: Ubuntu Server with /home on separate partition
/dev/sda1: EFI (500MB) - /boot/efi
/dev/sda2: Boot (2GB) - /boot
/dev/sda3: Root (30GB) - /
/dev/sda4: Home (remaining) - /home
```

---

## Power & Cooling

### Power Supply

- **Main PSU Capacity**: 
- **Redundancy**: Single / Dual PSU
- **UPS Model**: 
- **UPS Runtime**: ~10-15 minutes
- **PDU**: Outlets, current monitoring

### Cooling System

- **Ambient Temperature Range**: 15-25°C (ideal)
- **Ambient Humidity**: 40-60% (ideal)
- **CPU Cooling**: Air / Liquid
- **Case Fans**: (quantity & CFM)
- **Active Cooling Devices**: 

### Power Management

- **Wake-on-LAN**: Enabled for nodes
- **Power Scheduling**: Morning startup at 06:00, Shutdown at 22:00
- **Graceful Shutdown Automation**: UPS integration with monitoring

---

## Security

### Access Control

- **SSH Keys**: Stored in `/root/.ssh/authorized_keys`
- **SSH Port**: 22 (consider non-standard port)
- **Firewall Rules**: UFW/iptables configured
- **Default Deny**: All inbound, explicit allow rules

### Authentication

- [ ] SSH key-based auth only (no passwords)
- [ ] 2FA/MFA where applicable
- [ ] VPN access for remote administration
- [ ] Strong passwords for services (20+ characters)

### Network Security

- [ ] Separate VLANs for services
- [ ] Network segmentation by trust level
- [ ] Firewall rules documented
- [ ] Regular port scanning

### Data Protection

- [ ] Full disk encryption (LUKS)
- [ ] Regular backups verified
- [ ] Sensitive data encrypted at rest
- [ ] SSL/TLS certificates for all services

### Updates & Patches

- **Update Schedule**: Every 2 weeks (Tuesday)
- **Kernel Updates**: Automatic with reboot approval
- **Application Updates**: Manual after testing

---

## Monitoring & Maintenance

### Health Checks

| Item | Frequency | Method | Alert Threshold |
|------|-----------|--------|-----------------|
| CPU Temperature | Every 5 min | Prometheus | > 85°C |
| Memory Usage | Every 5 min | Prometheus | > 90% |
| Disk Usage | Every 1 hour | Prometheus | > 85% |
| Network Traffic | Every 30 sec | Prometheus | Custom |

### Maintenance Schedule

| Task | Frequency | Estimated Time | Last Completed |
|------|-----------|-----------------|-----------------|
| System updates | Monthly | 30 min | |
| Security patches | As needed | 15 min | |
| Log rotation | Weekly | 5 min | |
| Backup verification | Monthly | 1 hour | |
| Physical cleanup | Quarterly | 1 hour | |
| BIOS/Firmware updates | Annually | 1 hour | |

### Monitoring Tools

```bash
# Check system status
uptime
free -h
df -h
ps aux

# Monitor network
ss -tuln
netstat -i
iftop

# Container health
docker ps
docker logs <container>
```

### Log Locations

| Service | Log Path | Rotation |
|---------|----------|----------|
| System | `/var/log/syslog` | Daily |
| Docker | `/var/lib/docker/containers/` | Daily |
| Application | `/var/log/app/` | Weekly |

---

## Backup Strategy

### Backup Plan

**Frequency**: Daily  
**Retention**: 30 days local, 90 days cloud  
**Method**: Incremental daily, Full weekly

### Backup Destinations

1. **Local Attached Storage**: 4TB external HDD
2. **Network Storage**: NAS on separate subnet
3. **Cloud Storage**: B2 Backups (redundancy)

### Backup Verification

```bash
# Test restore monthly
# Verify checksums weekly
# Monitor backup logs daily
```

### Recovery Procedures

- **Full System Recovery**: Boot from recovery media, restore from snapshot
- **File Recovery**: Mount backup volume, recover individual files
- **Database Recovery**: Use database-specific restore tools

---

## Troubleshooting

### Common Issues

#### Network Connectivity

**Problem**: Node not reachable  
**Solution**:
1. Check IP address: `ip addr show`
2. Test gateway: `ping 192.168.1.1`
3. Check DNS: `nslookup google.com`
4. Review firewall: `sudo ufw status`

#### High CPU Usage

**Problem**: CPU consistently above 80%  
**Solution**:
1. Identify process: `top -b -n 1 | head -20`
2. Check for runaway processes
3. Review container resource limits
4. Consider scaling horizontally

#### Disk Space Issues

**Problem**: Disk nearly full  
**Solution**:
1. Find large files: `du -sh /* | sort -hr`
2. Check log files: `du -sh /var/log/*`
3. Cleanup old containers: `docker system prune`
4. Review docker images: `docker images`

#### Service Won't Start

**Problem**: Container fails to start  
**Solution**:
1. Check logs: `docker logs <container>`
2. Verify ports available: `ss -tuln | grep :port`
3. Check resource limits
4. Review configuration files

### Useful Commands

```bash
# System information
uname -a
lsb_release -a
systemctl status

# Network diagnostics
traceroute example.com
mtr example.com
iperf3 -c remote_host

# Disk & Storage
lsblk
mount
fstab verification

# Container management
docker ps -a
docker inspect <container>
docker stats
```

### Contact & Resources

- **Manufacturer Datasheets**: /docs/hardware/
- **Service Documentation**: /docs/services/
- **Configuration Backups**: /backups/configs/
- **Knowledge Base**: Wiki page URL

---

## Quick Reference

### Emergency Shutdown

```bash
# Graceful shutdown
sudo shutdown -h +5 "Maintenance in 5 minutes"

# Immediate shutdown
sudo shutdown -h now

# Cancel shutdown
sudo shutdown -c
```

### Service Restart

```bash
# Restart all docker containers
docker restart $(docker ps -q)

# Restart specific service
systemctl restart <service>
```

### System Diagnostics

```bash
# Full system health report
echo "=== CPU ===" && nproc && echo "=== RAM ===" && free -h && \
echo "=== DISK ===" && df -h && echo "=== UPTIME ===" && uptime
```

---

**Template Version**: 1.0  
**Last Updated**: 2024-07-18  
**Next Review Date**: 2024-08-18
