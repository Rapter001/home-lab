<p align="center">
  <img src="https://cdn.jsdelivr.net/gh/selfhst/icons@main/png/adguard-home.png" width="80">
</p>

<h1 align="center">ADGUARD HOME</h1>

## 📦 Container

| Item | Details |
|------|---------|
| Name |ADGUARD HOME|
| Image |adguard/adguardhome:latest|
| Version |LATEST|
| Network Mode |host|


---

## 🌐 Ports

> **Note:** When using `network_mode: host`, this section only documents the ports used by the service. Ports are not manually configured or mapped by Docker.

| Port | Protocol | Purpose |
|------|----------|---------|
| 53 | TCP/UDP | Standard DNS |
| 67 | UDP | DHCP Server |
| 68 | UDP | DHCP Client |
| 12517 | TCP | Web Interface (HTTP) |
| 8853 | TCP/UDP | HTTPS + HTTP/3 + DNS over HTTPS |
| 853 | TCP | DNS over TLS |
| 5443 | TCP/UDP | DNS over QUIC |
| 6060 | TCP | Debug / Profiling |

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