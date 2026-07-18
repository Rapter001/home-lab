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
NONECRON=*/1 * * * *
RUN_ON_START=true
PRINT_CONFIG_ONLY=false
CONTINUE_ON_ERROR=true
HTTP_CLIENT_TIMEOUT=30s
API_PORT=16568
API_DARK_MODE=true

ORIGIN_URL=https://192.168.1.185:8853
ORIGIN_WEB_URL=https://192.168.1.185:8853
ORIGIN_USERNAME=Rapter
ORIGIN_PASSWORD=Foreverus12
ORIGIN_INSECURE_SKIP_VERIFY=true
ORIGIN_AUTO_SETUP=true

# Replica 1
REPLICA1_URL=https://192.168.1.26:8853
REPLICA1_WEB_URL=https://192.168.1.26:8853
REPLICA1_USERNAME=Rapter
REPLICA1_PASSWORD=Foreverus12
REPLICA1_INSECURE_SKIP_VERIFY=true
REPLICA1_AUTO_SETUP=true

# Features
FEATURES_DNS_ACCESS_LISTS=true
FEATURES_DNS_SERVER_CONFIG=true
FEATURES_DNS_REWRITES=true
FEATURES_DHCP_SERVER_CONFIG=true
FEATURES_DHCP_STATIC_LEASES=true
FEATURES_GENERAL_SETTINGS=true
FEATURES_PROTECTION_STATUS=true
FEATURES_QUERY_LOG_CONFIG=true
FEATURES_STATS_CONFIG=true
FEATURES_CLIENT_SETTINGS=true
FEATURES_SERVICES=true
FEATURES_FILTERS_BLACKLIST=true
FEATURES_FILTERS_WHITELIST=true
FEATURES_FILTERS_USER_RULES=true
FEATURES_THEME=true
FEATURES_TLS_CONFIG=true
```

---

## 🔗 Networks

| Network | Purpose |
|---------|---------|
| 192.168.1.0/24 | Main LAN Network |
---