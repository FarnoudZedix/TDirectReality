# VLESS + REALITY + Vision Optimized Setup  
### By Farnoud Hosseini

A high-performance and production-grade **VLESS + REALITY** deployment using **xtls-rprx-vision** with advanced **Sockopt optimization** for maximum speed, low latency, and connection stability on VPS providers like Vultr.

---

# 📋 Table of Contents

- Overview
- Features
- Requirements
- Installation
- REALITY Key Generation
- 3x-ui Panel Configuration
- Sockopt Optimization
- Client Configuration
- System Performance Tuning
- Recommended VPS Locations
- Troubleshooting
- Security Notes
- Raw Xray Configuration
- Useful Commands
- Author

---

# 🚀 Overview

This setup is designed for users who need:

- Extremely low latency
- Stable international routing
- High throughput
- Minimal protocol overhead
- Maximum stealth against DPI systems

The configuration uses:

| Component | Value |
|---|---|
| Protocol | VLESS |
| Security | REALITY |
| Transport | TCP |
| Flow | xtls-rprx-vision |
| Port | 443 |

---

# ✨ Features

- VLESS + REALITY
- xtls-rprx-vision optimization
- TCP transport for lowest overhead
- BBR congestion control
- TCP Fast Open enabled
- IPv4 optimized routing
- Advanced socket optimization
- Optimized for Iran ↔ Europe routes
- Compatible with all modern Xray clients

---

# 📦 Requirements

| Requirement | Specification |
|---|---|
| VPS Provider | Vultr / Hetzner / OVH |
| OS | Ubuntu 20.04+ / Debian 10+ |
| Open Port | TCP 443 |
| RAM | 512MB+ |
| CPU | 1 vCore+ |

---

# ⚡ Installation

## 1. Connect to Your VPS

```bash
ssh root@YOUR_VPS_IP
```

## 2. Update System

```bash
apt update && apt upgrade -y
```

## 3. Install 3x-ui

```bash
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
```

Recommended panel port:

```text
2053
```

---

# 🔑 REALITY Key Generation

```bash
/usr/local/x-ui/bin/xray-linux-amd64 x25519
```

```bash
openssl rand -hex 8
```

---

# ⚙️ 3x-ui Panel Configuration

## Basic Settings

| Field | Value |
|---|---|
| Protocol | vless |
| Port | 443 |
| Security | reality |
| Network | tcp |
| Header Type | none |

---

# 🧠 Sockopt Optimization

| Option | Value |
|---|---|
| tcpFastOpen | true |
| tcpCongestion | bbr |
| tcpKeepAliveIdle | 300 |
| domainStrategy | UseIPv4 |
| tcpWindowClamp | 1200 |
| tcpUserTimeout | 10000 |

---

# 📱 Client Configuration

```text
vless://UUID@SERVER_IP:443?flow=xtls-rprx-vision&security=reality&sni=www.yahoo.com&fp=chrome&pbk=PUBLIC_KEY&sid=SHORT_ID&type=tcp&headerType=none#Reality
```

---

# 🔥 Enable BBR

```bash
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p
```

---

# 🌍 Recommended VPS Locations

| Priority | Location | Average Latency |
|---|---|---|
| 1 | Frankfurt | 100-130ms |
| 2 | Amsterdam | 110-140ms |
| 3 | London | 120-150ms |
| 4 | Paris | 120-160ms |

---

# 🛠 Troubleshooting

## View Logs

```bash
journalctl -u xray -f
```

## Restart Xray

```bash
systemctl restart xray
```

---

# 🔒 Security Notes

- REALITY prevents TLS fingerprinting
- Port 443 blends with HTTPS traffic
- Chrome fingerprint mimics real browsers
- Vision flow improves stealth behavior

---

# 👨‍💻 Author

### Farnoud Hosseini

Optimized and documented for high-performance VLESS + REALITY deployments using Xray-core and 3x-ui.

---

Last Updated: 2026
