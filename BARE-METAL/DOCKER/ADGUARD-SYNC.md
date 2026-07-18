<p align="center">
  <img src="https://cdn.jsdelivr.net/gh/selfhst/icons@main/png/adguardhome-sync.png" width="80">
</p>

<h1 align="center">ADGUARD SYNC</h1>

## 📦 Container

| Item | Details |
|------|---------|
| Name |ADGUARD SYNC|
| Image |ghcr.io/bakito/adguardhome-sync:latest|
| Version |LATEST|
| Network Mode |bridge|


---

## 🌐 Ports

> **Note:** When using `network_mode: host`, this section only documents the ports used by the service. Ports are not manually configured or mapped by Docker.

| Port | Protocol | Purpose |
|------|----------|---------|
| 16568 | TCP | Web Interface (HTTP) |

---

## ⚙️ Environment

```env
NONE
```

---

## 💾 Volumes / Mounts

| Host Path | Container Path |
|-----------|----------------|
|/docker-files/adguardhome/work|/opt/adguardhome/work|
|/docker-files/adguardhome/conf|/opt/adguardhome/conf|

---

## 🔗 Networks

| Network | Purpose |
|---------|---------|
| 192.168.1.0/24 | Main LAN Network |
---