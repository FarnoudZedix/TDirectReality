# راه‌اندازی بهینه VLESS + REALITY + Vision  
### ساخته شده توسط Farnoud Hosseini

یک تنظیم حرفه‌ای و بهینه‌شده برای VLESS + REALITY با استفاده از xtls-rprx-vision و تنظیمات پیشرفته Sockopt جهت دستیابی به بیشترین سرعت، کمترین پینگ و بالاترین پایداری روی VPS.

---

# 📋 فهرست مطالب

- معرفی
- ویژگی‌ها
- پیش‌نیازها
- نصب سریع
- ساخت کلیدهای REALITY
- تنظیم پنل 3x-ui
- بهینه‌سازی Sockopt
- تنظیم کلاینت
- بهینه‌سازی سیستم
- لوکیشن‌های پیشنهادی VPS
- عیب‌یابی
- نکات امنیتی
- کانفیگ خام Xray
- دستورات کاربردی
- سازنده

---

# 🚀 معرفی

این کانفیگ برای کاربرانی طراحی شده که نیاز دارند:

- پینگ پایین
- سرعت بالا
- پایداری زیاد
- کمترین میزان افت سرعت
- مخفی‌سازی حرفه‌ای ترافیک

مشخصات اصلی:

| بخش | مقدار |
|---|---|
| پروتکل | VLESS |
| امنیت | REALITY |
| ترنسپورت | TCP |
| Flow | xtls-rprx-vision |
| پورت | 443 |

---

# ✨ ویژگی‌ها

- استفاده از REALITY
- بهینه‌سازی Vision Flow
- استفاده از TCP برای کمترین Overhead
- فعال بودن BBR
- فعال بودن TCP Fast Open
- بهینه‌سازی IPv4
- تنظیمات حرفه‌ای Sockopt
- مناسب برای مسیر ایران ↔ اروپا

---

# 📦 پیش‌نیازها

| مورد | توضیح |
|---|---|
| VPS | Vultr / Hetzner / OVH |
| سیستم عامل | Ubuntu 20.04+ یا Debian 10+ |
| پورت باز | TCP 443 |
| رم | حداقل 512MB |
| CPU | حداقل 1 هسته |

---

# ⚡ نصب

## 1. اتصال به سرور

```bash
ssh root@YOUR_VPS_IP
```

---

## 2. آپدیت سیستم

```bash
apt update && apt upgrade -y
```

---

## 3. نصب 3x-ui

```bash
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
```

پورت پیشنهادی پنل:

```text
2053
```

---

# 🔑 ساخت کلیدهای REALITY

ساخت کلید عمومی و خصوصی:

```bash
/usr/local/x-ui/bin/xray-linux-amd64 x25519
```

ساخت Short ID:

```bash
openssl rand -hex 8
```

---

# ⚙️ تنظیم پنل 3x-ui

ورود به پنل:

```text
http://YOUR_VPS_IP:2053
```

رفتن به:

```text
Inbounds → Add Inbound
```

---

## تنظیمات اصلی

| فیلد | مقدار |
|---|---|
| Protocol | vless |
| Port | 443 |
| Security | reality |
| Network | tcp |
| Header Type | none |

---

## تنظیمات REALITY

| فیلد | مقدار |
|---|---|
| Dest | www.microsoft.com:443 |
| SNI | www.microsoft.com |
| Fingerprint | chrome |
| Public Key | کلید عمومی |
| Private Key | کلید خصوصی |
| Short ID | شورت آیدی |

---

# 🧠 بهینه‌سازی Sockopt

تنظیمات پیشنهادی:

| گزینه | مقدار |
|---|---|
| tcpFastOpen | true |
| tcpCongestion | bbr |
| tcpKeepAliveIdle | 300 |
| domainStrategy | UseIPv4 |
| tcpWindowClamp | 1200 |
| tcpUserTimeout | 10000 |

---

## نمونه Sockopt

```json
"sockopt": {
  "tcpFastOpen": true,
  "tcpCongestion": "bbr",
  "tcpKeepAliveIdle": 300,
  "domainStrategy": "UseIPv4",
  "tcpWindowClamp": 1200,
  "tcpUserTimeout": 10000
}
```

---

# 📱 تنظیم کلاینت

نمونه لینک اتصال:

```text
vless://UUID@SERVER_IP:443?flow=xtls-rprx-vision&security=reality&sni=www.yahoo.com&fp=chrome&pbk=PUBLIC_KEY&sid=SHORT_ID&type=tcp&headerType=none#Reality
```

---

## کلاینت‌های پیشنهادی

| پلتفرم | برنامه |
|---|---|
| Android | v2rayNG / Hiddify |
| iPhone | Streisand / FoXray |
| Windows | v2rayN / Nekoray |
| Linux | Qv2ray |
| macOS | Nekoray |

---

# 🔥 فعال‌سازی BBR

```bash
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p
```

بررسی فعال بودن:

```bash
sysctl net.ipv4.tcp_congestion_control
```

---

# 🌍 بهترین لوکیشن‌های VPS

| اولویت | لوکیشن | پینگ تقریبی |
|---|---|---|
| 1 | Frankfurt | 100-130ms |
| 2 | Amsterdam | 110-140ms |
| 3 | London | 120-150ms |
| 4 | Paris | 120-160ms |

---

# 🛠 عیب‌یابی

## مشاهده لاگ‌ها

```bash
journalctl -u xray -f
```

---

## ری‌استارت Xray

```bash
systemctl restart xray
```

---

## بررسی باز بودن پورت

```bash
ufw status
```

---

# 🔒 نکات امنیتی

مزایای این کانفیگ:

- مخفی شدن کامل ترافیک
- جلوگیری از TLS Fingerprinting
- شبیه‌سازی مرورگر Chrome
- ترکیب شدن با ترافیک HTTPS روی پورت 443

---

## کارهایی که نباید انجام دهید

| اشتباه | دلیل |
|---|---|
| استفاده از WebSocket | افزایش Delay و Overhead |
| اشتراک کلید خصوصی | نابودی امنیت |
| استفاده از Flow اشتباه | قطع اتصال |
| استفاده از Cloudflare | افزایش Latency |

---

# 📄 کانفیگ خام Xray

```json
{
  "inbounds": [
    {
      "port": 443,
      "protocol": "vless",
      "streamSettings": {
        "network": "tcp",
        "security": "reality"
      }
    }
  ]
}
```

---

# ⚡ دستورات کاربردی

## ری‌استارت سرویس

```bash
systemctl restart xray
```

---

## مشاهده لاگ

```bash
journalctl -u xray -f
```

---

## تست پورت

```bash
nc -zv YOUR_VPS_IP 443
```

---

# 👨‍💻 سازنده

### Farnoud Hosseini

مستندسازی و بهینه‌سازی شده برای کانفیگ‌های حرفه‌ای VLESS + REALITY بر پایه Xray-core و 3x-ui.

---

آخرین بروزرسانی: 2026
