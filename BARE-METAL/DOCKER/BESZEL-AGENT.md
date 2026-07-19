<p align="center">
  <img src="https://cdn.jsdelivr.net/gh/selfhst/icons@main/png/beszel.png" width="80">
</p>

<h1 align="center">BESZEL AGENT</h1>

## 📦 Container

| Item | Details |
|------|---------|
| Name |beszel-agent |
| Image |henrygd/beszel-agent:latest|
| Version |LATEST|
| Network Mode |host|

---

## ⚙️ Environment

```env
KEY=EXAMPLE
LISTEN=45876
TOKEN=EXAMPLE
HUB_URL=http://EXAMPLE:8090
```

---

## 💾 Volumes / Mounts

| Host Path | Container Path |
|-----------|----------------|
|/mnt/external-hhd|/extra-filesystems/sdb1|
|/docker-files/beszel-agent|/var/lib/beszel-agent|
|/var/run/docker.sock|/var/run/docker.sock|

---

## 🔗 Networks

| Network | Purpose |
|---------|---------|
| 192.168.1.0/24 | Main LAN Network |
---