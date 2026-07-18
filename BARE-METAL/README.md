# 🐳 Docker Host

## 📖 Overview

This machine is a bare metal Docker host running Ubuntu Server 24.04 LTS.

It provides a self-hosted platform for running applications, infrastructure services, monitoring tools, and internal services using Docker containers.

---

## 🖥️ System Information

| Item | Details |
|------|---------|
| Host Type | Bare Metal Server |
| Operating System | Ubuntu Server 24.04 LTS |
| CPU | Intel(R) Core(TM) i5-3470S CPU @ 2.90GHz |
| Memory | 12 GB RAM |
| Storage | 128 GB SSD + 256GB External HHD For Backup|
| Container Runtime | Docker Engine |
| Management | Portainer |
| Monitoring | Beszel + Uptime Kuma |
| Updates | Watchtower (Docker Containers) + Automatic Update (Linux)|

---

## 🚀 Purpose

This Docker host runs:

- 🌐 Web applications
- 🔐 Security services
- 📊 Monitoring tools
- 🏠 Homelab services
- 🤖 AI applications
- 📁 File and document management

---

## 🏗️ Architecture

```mermaid
flowchart TD

Host[Ubuntu Server 24.04<br/>Bare Metal]

Docker[Docker Engine]

Apps[Applications]
Security[Security Services]
Monitor[Monitoring]
Data[Databases]

Host --> Docker

Docker --> Apps
Docker --> Security
Docker --> Monitor
Docker --> Data